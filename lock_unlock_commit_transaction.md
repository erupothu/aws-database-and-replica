##### 1. By default, MySQL runs in autocommit mode. This means that as soon as you execute an update, MySQL will store the update on disk.

```
BEGIN;
SELECT @A:=SUM(salary) FROM table1 WHERE type=1;
UPDATE table2 SET summmary=@A WHERE type=1;
COMMIT;
```
##### 2. LOCK TABLES/UNLOCK TABLES Syntax
###### LOCK TABLES locks tables for the current thread. UNLOCK TABLES releases any locks held by the current thread. All tables that are locked by the current thread are automatically unlocked when the thread issues another LOCK TABLES, or when the connection to the server is closed.

```
LOCK TABLES tbl_name [AS alias] {READ | [READ LOCAL] | [LOW_PRIORITY] WRITE}
            [, tbl_name {READ | [LOW_PRIORITY] WRITE} ...]
...
UNLOCK TABLES
```

#### Read vs. Write locks
Read locks are “shared” locks which prevent a write lock is being acquired but not other read locks.
Write locks are “exclusive ” locks that prevent any other lock of any kind.
In this tutorial, you have learned how to lock and unlock tables for cooperating with the table accesses between sessions.
```
mysql> LOCK TABLES trans READ, customer WRITE;
mysql> SELECT SUM(value) FROM trans WHERE customer_id=some_id;
mysql> UPDATE customer SET total_value=sum_from_previous_statement
    ->        WHERE customer_id=some_id;
mysql> UNLOCK TABLES;
```

#### SET TRANSACTION Syntax
```
SET [GLOBAL | SESSION] TRANSACTION ISOLATION LEVEL
{ READ UNCOMMITTED | READ COMMITTED | REPEATABLE READ | SERIALIZABLE }
```

