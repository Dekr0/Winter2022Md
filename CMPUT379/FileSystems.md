# File Systems

## Disk Scheduling

---

- Improve disk access time and disk bandwidth via scheduling
  - Order in which disk I/O requests are serviced.
- Required information and procedure to service a request (Page 473)
- Type of disk-scheduling algorithms
  - FCFS scheduling (Page 473)
  - SSTF scheduling (Page 474 -475)
  - SCAN scheduling (Page 475)
  - CSCAN scheduling (Page 476)
  - LOOK scheduling (Page 477)
- Selection of disk-scheduling algorithm (Page 477)
  - SSTF is common
  - Selection depends on numbers factor
  - Bundle a set of algorithms into OS and use for different scenarios
    - computation cost for finding which algorithm to use

---

## File Concept

---

- Abstraction => logical storage unit, **file** (Page 504)
  - abstract data type


---

### File Attributes (Page 504)

---

- Name
- Identifier
- Type
- Location
- Size
- Protection
- Time, date, and user identification

---

### File Operations (Page 506)

---

- Creating a file
  - space in the file system
  - an entry for the new file must be made in the directory
- Writing a file
  - system call (filename and information to be written)
  - write pointer
- Reading a file
  - system call
- Repositioning within a file
- Deleting a file
- Truncating a file
- Information are associated with an open file (Page 508).
