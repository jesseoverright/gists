## Sql Gists
### Select

Conditional statements

    SELECT
        CASE WHEN column2 is null THEN 'All' ELSE column2 END results
        COALESCE(column4, column3) as date      # column4 if not null, otherwise column 3
    FROM schema.table

Get count

    SELECT a.column, count(*) FROM table a
    WHERE a.column2 IN (
        SELECT b.column FROM table b
        WHERE b.column = a.column3 AND b.column2 LIKE '%items.'
    )
    GROUP BY 1

### Insert

    INSERT INTO table a (a.column, a.column2) VALUES (1, "Etc")

### Update

    UPDATE schema.table SET column1 = 'value', column2 = 1 WHERE column3 = 'value'

### Upsert

    UPSERT

### Delete

    DELETE FROM schema.table WHERE column = 'value'

### Basic Joins

    SELECT a.column1, a.column2, b.column1 FROM schema.table a
    JOIN schema.other_table b
    ON a.column3 = b.column2

## Additional Examples

### Alter a table

    ALTER TABLE schema.table ADD COLUMN columnname varchar(255);
    ALTER TABLE schema.table ADD COLUMN columnname integer;

### Backup a table

    CREATE TABLE new_table AS (SELECT * FROM old_table)

### Windowing