# Data Storage Structures

## Key Concepts (Textbook)

------

- Magnetic Disks (Page 563) and Block Structured Access (Page 577)

### File Organization (Page 588)

------

- Overview
- Fixed-Length Records
  - How to arrange in a block
  - Deletion
- Variable-Length Records
  - Two types of attributes
    - fixed-length
    - variable-length
      - offset-length pair
      - null bitmap
  - How to arrange in a block
    - slotted-page structure
      - insertion
      - deletion

------

### Organization of Records in Files

------

#### Heap File (Page 596)

------

- any record can be placed anywhere
- no ordering
- insertion
- deletion => free-space map

------

#### Sequential File (Page 597)

------

- records are stored in sequential order based on "search key"
- 

------

#### Multi-table Clustering File

- records of several different relations are stored in the same file

- B+ Tree
  - B+ Tree index structure
  - Search key
- Hashing 
  - Hash function is computed on some attribute of each record
  - Result of the hash  function specifies the block placement