# File Organization

- DBMS will use all types of file structures for different situations.

---

## Heap File

------

- with or w/o gaps and no ordering
- operations
  - insert : O(1)
    - find the last page and insert it
    - if the last page is full, create a new page
  - delete and search : O(N)
    - N = # pages
- good performance for insert and full scan
- bad performance for searches and deletes (need a search first)

---

## Sorted File

---

- with or w/o gaps
- operations
  - insert : O($\log_2N$)
    - search for location and insert
    - instead of pushing everything down after insertion
    - create an overflow page, 
      - insert the new record in the overflow page, 
      - and link it to the page where previously searched.
      - sort the entire files if there are too many overflow pages.
  - delete : O($\log_2N$)
  - search : O($\log_2N$)
    - search operates on pages
- good for searches (binary search), deletes (tagging!)
- bad for inserts (difficult to keep the file sorted)
- full scan is the same as in a heap file

---

## Indexed Files

------

- To provide a fast access to data
  - sorting (dictionary, phone book)
  - indexing (booking index)
- hash indexes
- tree-structured indexes

---

### Sorting

---

- **Internal sort** : Data is in the main memory and is ready for sorted.
  - Example, how can you sort a list of 10 numbers ?
    - Quick sort, Merge Sort, Bubble Sort
- **External sort** : 
  - Data is not in the main memory instead of disk. 
  - Data is in pages.
  - Data is usually too large to fit into the main memory.

---

#### External Sort

---

- Split each page into segment that are small enough to be transferred into the main memory.
- Sort those segment using internal sort algorithm
  - Sorted segment as output
  - Each segment is a file output (can be found in /tmp folder in Unix system).
- Merge the output file

---

### Indexing

---

- Efficiently locate rows without searching the entire table
- Search key for building index (id, name, title)
  - can have duplicate values
  - keys with the same values are stored together

- Index entry
  - < search key, full record > (results in an integrated index)
    - example entries in a phone book or a dictionary
    - One thing to notice is that 
    - it's unnecessary to sort the full record second time since full record is part of the index entry.
  - or < search key, id or address > (separate index and data files)
    - address example : page id, a key, location address

---

#### Clustered vs. Unclustered Index

---

- Ordering of the index entries and data records are the same
  - Index entries and data records are ordered on the same columns.
  - ***Clustered index***
  - Example, index entries are sorted by student id and data records are also sorted by student id.
  - At most one clustered index.
    - Multiple clustered index create redundancy on data records. 
    - Avoid redundancy
      - Issue of redundancy (example) : one place change, other place need change as well.
- Index entries and data records are not ordered on the same columns.
  - ***Unclustered index***
  - Any number of unclustered index are possible.

---

#### Dense vs Sparse

---

- Dense index : index entry for each data record.
- Sparse index : index entry for each data page in the data file.
  - can be built on sorted data.
  - must be clustered

---

#### Index overhead

---

- Building one index based on one column is not going to work
  - `select * from students where name 'joe'`
  - but index is built based on student Id.
- accessing the data
  - building index on the columns that are helpful for query
    - columns that are very frequently
- updating the data
  - also need to update the indices as well
