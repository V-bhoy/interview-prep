## How table data is actually stored?
- The tables that we see is just a logical representation of the data.
- Actual Data is not stored in this way
- DBMS creates DATA PAGES (generally KB, depends on DB)
- Each Data Page stores multiple table rows in it.
- Data Page consists
    - header (page no, free space, checksum etc.), 96 bytes
    - data records (actual data), 8060 bytes
    - offset (array, each index holds a pointer corresponding to data in records), 36 bytes, it is unordered as of now.
- DBMS creates and manages these data pages. So creating one table, is creating and managing multiple data pages.
- A data page is stored in a data block which is a physical memory like disc.
### What is a data block?
- Data block is the minimum amount of data which can be read/write by an I/O operation.
- managed by underlying storage system like disc.
- Its size can range from 4kb to 32kb (common size is 8kb)
- So based on the block size, it can hold 1 or many data pages
- DBMS has no control over which data page is stored in which data block, so it maintains the mapping of data page and data block. Data blocks can ve scattered over the disc.

## What is indexing?
- used to increase the performance of database query. So data can be fetched faster.
- Without indexing, DBMS has to iterate each and every table row to find the requested data i.e O(n) which is too much time if there are millions of rows.

## Which data structure provides better complexity than O(n)?
- B+ tree (B tree -> Balanced tree), provides O(log N) time complexity for insertion, searching and deletion.
### How does Balanced Tree work?
- Sorted Data → Keys inside a node are stored in sorted order.
- Order M B-Tree → A node can have at most M children and M-1 keys.
   - Example: Order 3 → max 3 children, 2 keys per node.
- Balancing Property → All leaf nodes remain at the same depth.
- Splitting Rule → When a node overflows (more than M-1 keys), split at the median key, push median up to parent.
```
3-order B tree
each node can have 3 children and 2 keys
we need to store data --> 9, 33, 75, 41, 98, 214, 126, 55, 72
a node --> Pointer|key1|Pointer|key2|Pointer
- The left most pointer will point to data < key 1
- The middle pointer will point to data >= key 1 and < key 2
- The right most pointer will point to data >= key 2
|_|_| -> the line is the pointer and the slot is the key

1. Insert 9
|9|_| --> one empty key slot

2. Insert 33 → fits in same node
|9|33| --> now both keys are full, the pointers are pointing to nothing

3. Insert 75 → overflow (3 keys: 9, 33, 75).
Split at median (33), push up.
it create a new parent node from the mid child
     |33|_|
   /     \
 |9|_|     |75|_|

4. Insert 41 → goes to right child (since > 33, < 75).
     |33|_|
   /     \
 |9|_|  |41|75|

5. Insert 98 → goes to right child (> 75).
Right child full (41, 75, 98) → split at 75, push to parent.
      |33|75|
    /    |    \
 |9|_|  |41|_|  |98|_|

6. Insert 214 → goes to rightmost node.
      |33|75|
    /    |      \
 |9|_|   |41|_|   |98|214|

7. Insert 126 → goes to rightmost (98, 126, 214).
- Split at mid i.e 126, push to parent.
- But parent already full (33, 75, 126).
- So split parent at mid i.e 75 → new root.
         |75|_|
        /    \
   |33|_|      |126|_|
  /    \       /    \
|9|  |41|_|  |98|_|  |214|_|

8. Insert 55 → goes to left subtree (since < 75).
- Left child (33) has 2 children (9, 41). Insert 55 into right leaf.
         |75|
      /       \
   |33|     |126|
  /    \    /    \
|9| |41|55| |98| |214|

9. Insert 72 → goes to left subtree (since < 75).
- Goes to right child of 33 (41, 55). Insert 72.
- (Still okay since max 2 keys allowed).
         |75|
      /        \
   |33|55|      |126|
  /   /   \     /    \
|9| |41| |72| |98| |214|    
```
### ⚡ Key Idea
- Binary Search inside node → to pick correct child pointer.
- Splits keep tree balanced → median promotes upward.
- Search = O(log n) → fewer disk reads.
- B+ tree is same as balanced tree, but has a feature that child nodes are also linked to each other.
- DBMS uses B+ tree to manage its data pages and rows within the pages.
- When a column(s) is indexed, B+ tree is generated out of the column values
- The root and intermediary nodes of the tree holds the values for fast searching, possibility that it might have deleted from DB, but used for sorting the tree.
- The leaf nodes actually holds all the indexed column values.
- Whenever we insert a row in table, first it finds the position of the column index value in the balanced tree, determine the page to store the record based on the page of the nearest key. If the page is full, page splitting takes place (new page is created, data is splitted among both the pages), along with the key the pointer points to the address of the page that maps to a block, the pointer is updated if the record is stored in a new page.

## How Index Works?
- An index is an additional data structure (usually a B-Tree or Hash Table) that stores sorted values of one or more columns and pointers to the actual rows in the table.
- An index is created on one or more columns of a table.
- DBMS maintains an index file separate from the actual data file.
- Index file contains search keys + pointers to the data rows.
- Index file is always sorted.
``` sql
-- Suppose we have a table:
CREATE TABLE Students (
  StudentID INT PRIMARY KEY,
  Name VARCHAR(50),
  Age INT,
  City VARCHAR(50)
);

SELECT * FROM Students WHERE Name = 'Vaishali';
-- Queries Without Index
-- DBMS scans all rows.

CREATE INDEX idx_name ON Students(Name);
-- Queries With Index
-- DBMS jumps directly to ‘Vaishali’ using B+ Tree.

-- If you create index on one column → It stores that column’s values for all rows.
-- 	If you create composite index (multiple columns) → It stores combinations of those column values.
CREATE INDEX idx_emp_dept_salary
ON Employee(Department, Salary);
-- Then the index will store (Department, Salary) pairs in sorted order + row pointers.
```
## Types of Indexing
## Clustered Indexing (Primary Indexing)
- order of rows inside the data pages, match with the order of the index values (could be primary key or non-primary key).
- Leaf nodes of the B+ Tree = actual table rows.
- Rows in the table are physically stored in the order of the index key.
- Only one clustered index per table, because data can only be ordered one way.
- Dense Index
    - The dense index contains an index record for every search key value in the data file.
    - The index record contains the search-key value and a pointer to the first data record with that search-key value.
    - The rest of the records with the same search-key value would be stored sequentially after the first record.
    - It needs more space to store index record itself. The index records have the search key and a pointer to the actual record on the disk.
2. Sparse Index
    - An index record appears for only some of the search-key values.
    - Sparse Index helps you to resolve the issues of dense Indexing in DBMS. In this method of indexing technique, a range of index columns stores the same data block address, and when data needs to be retrieved, the block address will be fetched.
- Primary Indexing can be based on Data file is sorted w.r.t Primary Key attribute or non-key attributes.
- Based on Key attribute
     - Data file is sorted w.r.t primary key attribute.
     - PK will be used as search-key in Index.
     - Sparse Index will be formed i.e., no. of entries in the index file = no. of blocks in datafile.
     - no need of dense index.
- Based on Non-Key attribute
     - Data file is sorted w.r.t non-key attribute.
     - No. Of entries in the index = unique non-key attribute value in the data file.
     - This is dense index as, all the unique values have an entry in the
index file.
- E.g., Let’s assume that a company recruited many employees in
various departments. In this case, clustering indexing in DBMS
should be created for all employees who belong to the same
dept.
- Multi-level Index
    - Index with two or more levels.
    - If the single level index become enough large that the binary search it self would take much time, we can break down indexing into multiple levels.

## Secondary Index (Non-Clustering Index)
- Datafile is unsorted. Hence, Primary Indexing is not possible.
- Can be done on key or non-key attribute.
- Called secondary indexing because normally one indexing is already
applied.
- No. Of entries in the index file = no. of records in the data file.
- It's an example of Dense index.
- Here although the rows in the table is unsorted but the index table is sorted where we can find the corresponding block address woth binary search and then search in the given block.

## NOTE
- By default, DBMS only creates:
	•	A primary key index (automatically, since primary keys must be unique).
	•	Any unique constraints also get indexes automatically.
- For anything else, you manually decide which columns to index based on your query patterns.

## Where to use indexing 
- for read intensive database.
- tables having very large no of rows.

## Advantages of Indexing

- ✅ Faster SELECT queries.
- ✅ Efficient range queries and sorting.
- ✅ Reduces I/O operations.

## Disadvantages of Indexing

- ❌ Extra space needed for index file.
- ❌ Slows down INSERT, UPDATE, DELETE because index must be updated.
- ❌ Too many indexes = overhead.
