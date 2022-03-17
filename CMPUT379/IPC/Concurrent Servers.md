## Concurrent Servers

- An *iterative* server serves one client to completion before  switching to another client.
- A *concurrent* server uses time division multiplexing to  serve a number of clients.
  - time slicing, switch client really fast

------

## **Q**: How does one design a concurrent server?

------

- To start, here is a simple framework
  - at any time, the server knows N (the # of clients), and  the *file descriptors* *fd[0], fd[1], ..., fd[N-1]* used in the communications
  - *listening* to a client, and *reading* the incoming requests can be done using some kind of `read( fd[i] )` operation
- Pictures
  - A server, *n* clients
  - all clients establishes communication channel with that server
  - that server tracks all the channels with `fd` for read and write

------

## Q: What are the possible design options?

------

### Solution 1

------

- fork N copies of the server; assign each copy to a  specified client.
  - expensive to copy a new process
- What if the server needs to collect data sent from all clients in a shared buffer (e.g,  X Windows updates the display from ( possibly remote ) clients ( widgets, button, etc. ) ) ?
  - Assign a thread of control to each client.
  - Q: Is it OK to use out-of-kernel threads ?
    - If a thread of a process is block, the entire process is block (check OSS pg. 167)

------

### Solution 2 : I/O in the polling loop

------

#### Blocking

------

- Repeatedly poll the file descriptors using a (high level)  Standard I/O Library function (e.g., `fread()`), or even a low-level I/O function (e.g., `read()`)

-  Typically (and by default) such a function blocks until it gets some input.

```C
#include <unistd.h>

int main ( int argc, char *argv[] ) {
    int fd[4], buffsize = 100, buff[buffsize];
    ssize_t length;
    fd[0] = STDIN_FILENO;
    ... // start of poll loop
        length = read( fd[0], buff, buffsize ); // block
    ... // end of poll loop, go back to the start
}
```

------

#### Non-Blocking

------

```C
#include <fcntl.h>

int fcntl ( int FILEDS, int CMD, /* int ARG */ ... );
```

- FILEDS: a file descriptor to operate on
- CMD: one (or more) operation(s) on the descriptor, or its associated flags
- ARG: argument(s) specific to the CMD

```c
#include <unistd.h>, <errno.h>, <fcntl.h>
int main (int argc, char **argv) {
	int fd[4], buffsize= 100, buff[buffsize];
	ssize_t length;
    
	fd[0]= STDIN_FILENO;
	fcntl(fd[0], F_SETFL, O_NONBLOCK);
	... start of loop
        // loop to poll several file descriptors
	length= read(fd[0], buff, buffsize);
	printf ("length= %d, errno= %d\n", length, errno);
	... end of loop 
}
```

- Here, `read()` returns -1, with `errno` ≥ 0 if the source has no data

- wastes CPU time

- to improve performance, we may have to guess how long to wait each time around the loop

------

### Kernel-Supported I/O Multiplexing

------

- `NFDS` is the number `fd` for polling
  - size of `FDS[]`

```c
struct pollfd { // check APUE 14.4
	int fd;
	short events; // requested events
	short revents; // returned events
    // used for examine which event is occur
}
```

- *timeout* == 0, `poll` function will execute without waiting. `poll` is going to switch to the kernel, go to `FDS[]` and iterate all elements to do the following :
  - check whether if `events` interested in occur
  - if so, set the corresponding bit in the `revents` to `1`
  - then examine `revents` to see which event occur

------

#### Example

------

- The main process (a ready-only server) forks *N* children (write-only clients), and communicates via pipes

  

- Each client loops a number of times writing a unique ***id*** to a specific pipe, and then **sleeps** for a while. At the  end, the client closes the connection (sends ’***-1***’).

```c
#include<stdio.h>, <stdlib.h>, <unistd.h>, <poll.h>
#define N 3
#define MAXBUF 80

int fd[N][2], pid[N];

// fd[i][0] is the read end of the pipe between client i and server
// fd[i][1] is the write end of the pipe between client i and server

int fork_and_write (int id) {
    int i;
    char buf[1];
    pid_t pid;
    
    if ((pid = fork()) < 0) {
        perror("fork error \n");
        exit(1);
    }
    
    if (pid > 0) return pid;
    buf[0] = '0' + id;
    close (fd[id][0]); // child won't read
    
    for (i = 0; i < 10; i++) { // loops ten times;
        if (write(fd[id][1], buf, 1) < 0) { // write id
            perror("pipe write error\n");
            exit(1);
        }
        sleep(1);
    }
    
    buf[0] = -1;
    write(fd[id][1], buf, 1);
    exit(0);
}


```



- The server (read-only) maintains a done flag for each client. The main loop polls each client, and concurrently does something else (writes a dot)

```C
int main (int argc, char *argv[]) {
    int i, len, rval, writerId, n_writers;
    int dotCount, timeout, done[N];
    char buf[MAXBUF];
    struct pollfd pollfd[N];
    
    for (i = 0; i < N; i++)
        if (pipe(fd[i]) < 0) {
            perror("pipe error \n");
            exit(1);
        }
    
    for (i = 0; i < N; i++) pid[i] = fork_and_write(i);
    
    // parent keep tracks of each individual pipe line of 
    // each client (child process)
    for (i = 0; i < N; i++) { // parent won't write
        close(fd[i][1]);
        done[i] = 0;
        pollfd[i].fd = fd[i][0];
        pollfd[i].events = POLLIN;
        pollfd[i].revents = 0;
    }
    
    timeout = 0;
    n_writers = N;
    dotCount = 0;
    
    while (n_writers > 0) {
        rval = poll(pollfd, N, timeout);
        for (writerid = 0; writerId < N; writerid++) {
            if (done[writerId] == 0 && // client writerId
                // has not yet finish writiting
               (pollfd[writerId].revents & POLLIN) ) {
                // bit wise and of revents with POLLIN
                // if they equal 1, there is something to 
                // be read from the pipe
                len = read(fd[writerId][0], buf, MAXBUF);
                
                for (i = 0; i < len; i ++) {
                    if (buf[i] == -1) {
                        n_writers--;
                        // child id received
                        done[writerid] = 1;
                        break;
                    } else
                        printf("[%c]", buf[0]);
                }
            }
        }
        if ( ++dotCount % 10000 == 0 ) putc('.', stderr);
    }
    printf("\n");
}
```

