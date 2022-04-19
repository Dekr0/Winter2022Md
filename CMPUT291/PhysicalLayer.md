# Physical Layer

- Better understanding of the overhead and the cost
- How data is organized outside DBMS
- Not every data management problem is best solved using a DBMS
  - Example : NoSQL databases
    - Not limited to SQL
  - Limited queries (don't need the full power of SQL)

- Organizing files on disk (Secondary Storage)
- Structuring data in the files
  - What type file structures we can have
- Creating and maintaining indexes for quick access
  - What type of indexes can be build and how

---

## Computer memory hierarchy

---

- Fastest to the slowest
- Processor registers : very fast, very expensive, very small, volatile
- Processor cache : similar to CPU registers
- Main memory : fast, affordable, volatile
- Secondary Storage : non-volatile - suited for database
  - SSD
  - HHD : slow, very cheap
- Typical setting : Data is stored on disk and fetched to main memory when needed

---

## Disk

---

- There are two heads for top and bottom surface of one platter for read and write.
  - One head for each surface
- All heads move together.
- Tracks
- Sectors - smallest units that can be read and write on the disks
- Cylinder (Virtual) - tracks that are stack up together from different surface (platters)
- ***Page*** - smallest units for most program to read / write.
  - OS operates on pages.
- Access Time Calculation - Check ECE 311 Notes

---

## Reducing I/O costs

---

- Software solution : 
  - arrange blocks of a file sequentially on disk
  - read / write in bigger chunks
  - buffering
- Sequential Access
  - Store pages containing related information close together on disk.

---

