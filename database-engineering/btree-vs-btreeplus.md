# B-Tree vs B-Tree Plus

Understanding data structure of an index in database can lead you to create more performant query.

## Full table scan

It's mean that in order to fetch the data DB needs to read all values from the disks/pages

- Reading large table is slow
- Requires many IO to read all pages
- Should be reduced

## Original B Tree

Balanced data structure for search traversal (jump between nodes).

Element had key and values, value could be pointer to a value (row). Data pointer can point to primary key or tuple.

https://www.cs.usfca.edu/~galles/visualization/BTree.html

## Original B-tree Benefit for a database

B-tree help by simply having sorted key and separating values by each group.

- B-tree can have key and value

## B-tree limitation


## B-tree Plus


