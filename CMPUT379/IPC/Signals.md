# Signals

## Definition

------

- viewed as software *interrupts* :  they provide a way of handling *asynchronous* events.

  - synchronous is relative to the execution of the process that is receiving the signal
  - asynchronous event is an event 

- Every signal has a name, and a default action:

  - T = terminate

  - TC = terminate and core dump 

    [core file]: https://en.wikipedia.org/wiki/Core_dump

  - I = ignore

  - S = stop

- *keyboard generated*

  - SIGSTP => [ctrl-z] keyboard stop signal => S
  - SIGINT => [ctl-c] interrupt => T
  - SIGQUIT => [ctl-\ ] quit signal => TC

- *hardware exceptions*

  - SIGSEGV => segmentation fault => TC
  - SIGFPE => floating point exception => TC
  - SIGBUS => bus error => TC

- *software conditions*

  - SIGCHLD => change in child status => I
  -  SIGALARM => timer alarm => T 
  - SIGHUP => hangup => T

------

## Terminology 

------

- *posted* (generated, or sent ) if the event that causes
  the signal has occurred,
- *delivered* (or caught ) if the associated action is taken,
- *pending* if it has been posted but not delivered, or blocked,
- *blocked* if it is pending because the target process does not want it delivered
- Signal disposition (APUE 10.2) :
  - Let the default apply
  - Ignore the signal (except SIGKILL and SIGSTOP )
  - Catch it by a user defined function (signal handler).

------

## Traditional System-V Signal Environment

------

- Easy interface : signal(), pause(), SIG_DFL, SIG_IGN
- Unreliable behavior:
  - Signal can be lost
  - signal handlers (some functions handle a signal when a signal occurs) are reset to SIG_DFL after a signal is received
    - There is a windows of time where the signal handler is not associated with the signal
    - Example : cannot interrupt more than once
  - ”slow” system calls are interrupted (causing error return) when a signal is delivered (reading input from keyboard)
    - the signal interrupts the system calls and cause error
  - no support for blocking

------

## Experiments with signal()

------

```c
#include <sdio.h>
#include <unistd.h>
#include <signal.h>

int i;

void quit ( int code ) {
    fprintf( stderr, "\nInterrupt (code= %d, i= %d)\n", code,i );
}

int main (void) {
    signal( SIGQUIE, quit );
    
    for ( i = 0; i < 9e7; i++ )
        if ( i % 100000 == 0 ) putc( '.', stderr );
    
    return 0;
}
```

- Notes
  - use `kill -QUIT pid_number`
  - interrupt several times ? Yes, signal handler does not reset to `SIG_DFL` like in the traditional implementation
  - signal handler is called by the kernel

```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <setjmp.h>

jump_buf return_pt;
int i;

void quit ( int code ) {
    char answer;
    fputs( "\n restart the loop?", stdout );
    answer = fgetc(stdin);
    
    if ( answer == 'y' )
        longjump( return_pt, 1 );
}

int main ( void ) {
    if ( setjmp(return_pt) == 0 )
        signal( SIGQUIT, quit );
    
    prinf( "\nloop begins:\n" );
    for ( i = 0; i < 9e7; i++ )
        if ( i % 10000 == 0 ) {
            putchar('.');
            fflush(stdout);
        }
    
    puts( "\nFinished!" );
    
    return 0;
}
```

- `setjump(return_pt)` store the information of current stack (e.g, caller locations, etc.) into `struct jump_buf return_pt`.
  - After store the information, it return 0 and then kernel installs signal handler `quit` when `SIGQUIT` is invoked.
- When `SIGQUIT` is invoked, `quit` is invoked and if `answer` is "y"
  - After `longjump`, program will directly jump to the location where `setjmp` was called before instead return normally by popping function stack
  - but with return value `1` instead of `0` to prevent reinstallation of signal handler.
- If `answer` is not "y", then the signal handler will return normally back to main loop instead of restarting the loop.
- ***Issue***: the program only catch the signal once
  - The `signal()` is implemented by `sigaction()`
  - Once a signal handler is installed, the signal handler remains in effect
  - `sigaction()` maintain a signal mask. A mask that mute other signal when the signal handler is called.
  - When a signal `SIGQUIT` is invoked, `SIGQUIT` is added into signal mask before signal handler is called
    - prevent signal handler being called multiple times if another `SIGQUIT` occurs
  - When a signal handler returns normally, `SIGQUIT` is subtracted from signal mask such that the mask for signal is muted again.
  - Use `sigsetjmp` and `siglongjmp` to solve this issue.

------

### Experiment with POSIX.1 `sigaction()`

------

- Check APUE 10.13

```c
struct sigaction {
    int sa_flags; // OR'd bits : SA.SIGINFO
    void (*sa_handler)(int); // int -> signal # to catch
    sigset_t sa_mask;
    void (*sa_sigaction)( int, siginfo_t *, void *);
    // int -> signal # to catch
    // a pointer to struct siginfo_t, filled in by the
    // kernel
    // optional information a handler can return, void *
    
    /*
    A choice between two handlers depending on flags.
    If SIGINFO is 1, use the fourth field
    */
}
```

- `sa_mask` is used whenever signals need to be **blocked** when a signal handler is called
  - added to blocked signals on entry to the handler
  - subtract handler return
  - prevent handler being interrupt by other signals

```c
struct siginfo_t {
	int si_signo // signal number
	int si_errno // error number
	int si_code // signal code, additional information about the reason of the signal being genereated
	pid_t si_pid // sending process ID 
	uid_t si_uid // sending user ID
    // can detect the sender
}
```

- On entry to the handler, 
  - `sa_mask` is added to the to the set of signals already being blocked when the signal is delivered.
  - In addition, the signal that caused the handler to be executed will also be blocked.

- If `sa_flags[SA_SIGINFO] = 1` the sender’s `si_pid` is returned in a `siginfo_t` structure.

------

#### Example

------

```c
#include <stdio.h>, <unistd.h>, <signal.h>

int i;
struct sigaction oldAct, newAct;

// no struct siginfo_t is declared since handler is called
// by the kernel, and siginfo_t is filled by kernel
void quitHandler ( int sigNo, siginfo_t *sigInfo ) {
	fprintf ( stderr, "\n signo= %d, sender= %d, i= %d)\n",
	sigNo, sigInfo->si_pid, i );
}

int main (void) {
    newAct.sa_handler = quitHandler;
    newAct.sa_flags |= SA_SIGINFO; // omit error checking now
    
    /* install signal handlder
    * newAct is installed
    * oldAct is returned, information about the previous
    * handler
    */
    sigaction ( SIGQUIT, &newAct, &oldAct );
    for ( i= 0; i < 9e7; i++ )
    
        if ( i % 10000 == 0 ) 
        putc( ’.’, stderr );
    
    sigaction( SIGQUIT, &oldAct, &newAct );
    
    return(0);
}
```

