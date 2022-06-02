# Database Indexing Notes

Indexing, is a form of grouping so it's more easy to find something. Indexing on databases usually use B-Tree or B-Tree+ data structure.

Column that had index, are more faster to search on because it's already grouped. 

- [B-Tree+](https://wlbf.github.io/2021/05/09/b-plus-tree-index-1/) 

## Explain Keyword, SQL Query Planner and Optimizer

SQL Had keyword `EXPLAIN` and `ANALYZE` it will print the query planner for the database and report it to us.

To use it you can append the word `EXPLAIN` / `ANALYZE` as prefix for your sql

```txt
EXPLAIN ANALYZE SELECT * from users where id > 1000
```

## Index Scan vs Index Only Scan

Index Scan : Using index to search value, but the value fetch aren't the index so the engine will fetch the other data from table.

Index Only Scan :  Using index to search value, and only return the index value on index table.

On index table we can also include the table value

```sql
create index <index_name> on <table_name>(<column_that_indexed>) include (<column_we_save_the_value>)
```

Example

```sql
create index id_index on users(id) include (name, age)
```

Remember every time we create an index, we will accumulate more space for the database.

## Key Vs Non-Key Database Indexing

A key column is the column(s) that the index is created on, the non-key column are included columns

```
index index idx1 on table (col1, col2) include (col3, col4)
```

In the above example, `col1` `col2` are key columns, `col3` and `col4` are non-key columns

```
create index cidx on table1 (col1)
```

In the above example `col1` is the key column, and all other columns in the table are classed as non-key columns, as the clustered index is the table.

## Combining Database Indexing

Combining Index

```sql
create index on test (a,b)
```

In can also include some non-key value


```sql
create index on test (a,b) include (c)
```

## How database decide to use index

Database keeping a lot of statistic to use, some statistic are :

- How large are the table
- How large are the index
- How many row that we will fetch etc.

Statistic are just guesses the value, it might not correct. Imagine if you only have 3 column on your table and you already indexed the ID. Database will just use table full scan, since we are going to fetch it all any way.

## Bitmap Index Scan vs Index Scan vs Table Scan

## Create index without slowing down database

https://www.2ndquadrant.com/en/blog/create-index-concurrently/

```
create index concurrently index_name on table_name(column_name)
```

## Bloom filters

A Bloom filter is a data structure designed to tell you, rapidly and memory-efficiently, whether an element is present in a set.

https://llimllib.github.io/bloomfilter-tutorial/
