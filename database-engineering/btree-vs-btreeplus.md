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

- B-tree can have key and value in every nodes
- (k-1) (read: k minus one). Lest say we save b-tree with max degree of 3, parent node could only have 2 nodes in total and 3 nodes for the child.

## B-tree limitation

- Element in all nodes store both the key and the value
- Internal nodes take more spaces, because we have key and value
- Slow range queries, because you need to jump between nodes

## B-tree Plus

- Only stores the keys on internal nodes
- Values onlu stored on leaf nodes (the one that on very bottom nodes)
- Can fit many keys on internal nodes (because value are on the leaf nodes)
- Leaf nodes are linked on key
- Great for range queries because you can get range from leaf nodes only

## Consideration

- UUID (non number data type) in MySQL/PostgreSQL will bloated the data and slow the queries

