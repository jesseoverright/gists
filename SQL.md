# Sql Gists

The following examples use postgres syntax. Some examples may not work in Mysql or Oracle.

## Basics

### Insert

    INSERT INTO table a (a.column, a.column2) VALUES (1, "Etc")

Insert using data from another table

    INSERT INTO table (column, column2)
    SELECT column3, column4 FROM table2    

### Update

    UPDATE schema.table SET column1 = 'value', column2 = 1 WHERE column3 = 'value'

### Select

    SELECT * from schema.table WHERE column1 in (1,2,3)

Get row count by column

    SELECT column, count(*) FROM table GROUP BY 1

Get distinct results

    SELECT DISTINCT a.column1, a.column2 FROM schema.table a

Where clause using results from another table

    SELECT a.column, a.column3
    FROM table a
    WHERE a.column2 IN (
        SELECT b.column FROM table b
        WHERE b.column = a.column3 AND b.column2 LIKE '%items.'
    )

Rename a column

    SELECT a.column as new_name
    FROM table a
    WHERE a.column2 in (1,2,3)


### Delete

    DELETE FROM schema.table WHERE column = 'value'

## Joining Tables

### Basic Join

Join two tables based on one or more common values.

    SELECT a.column1, a.column2, b.column1 FROM schema.table a
    JOIN schema.other_table b
        ON a.column3 = b.column2
            AND a.column5 = b.column5

Alternatively, if the column names to join on are identical:

    SELECT a.column1, a.column2, b.column1 FROM schema.table a
    JOIN schema.other_table b
        USING (column3)

### Left Join

Left join will keep all data in left table regardless of data being present in the right table

    SELECT a.column1, a.column2, b.column1 
    FROM schema.table a
    LEFT JOIN schema.other_table b
        ON a.column3 = b.column2

Can be used to select values where a column does not exist

    SELECT a.column1, a.column2
    FROM schema.table a
    LEFT JOIN schema.other_table b
      ON a.column3 = b.column2
    WHERE b.column1 IS NULL

## Advanced Queries

### Conditional Statements

    SELECT
        CASE WHEN column2 is null THEN 'All' ELSE column2 END results
        COALESCE(column4, column3) as date      # column4 if not null, otherwise column 3
    FROM schema.table

    SELECT column FROM schema.table WHERE column2 <> 'test'   --- NOT EQUAL

### Subqueries

    WITH subquery AS (
        SELECT column1 as name, count(*)
        FROM schema.table
        GROUP BY column1
    )
    SELECT name FROM subquery WHERE count > 50

### Date & Time

#### Dates

    SELECT * FROM schema.table
    WHERE edit_date > date('2015-05-30') and edit_date < date(now())

Using date intervals (week, day, minute etc.)

    SELECT * FROM schema.table
    WHERE edit_date BETWEEN date(now()) - interval '1 week' AND date(now())

#### Time

### Upsert

    UPSERT

Insert into table if entry doesn't exist

    INSERT INTO table a (a.column, a.column2) 
    SELECT 1, "Etc"
    WHERE NOT EXISTS (
        SELECT 1 FROM table a WHERE a.column = 1 AND a.column2 = "Etc"
    )

### Windowing

## Table Management

### Create a table

    CREATE TABLE schema.new_table
    (
        column1 numeric,
        column2 text,
        column3 character varying(255)
    )

Assigning defaults and constraints

    CREATE TABLE schema.new_table
    (
        column1 numeric DEFAULT nexval('schema.id_sequence'),
        column2 text NOT NULL,
        column3 character varying(255),
        CONSTRAINT unique_id UNIQUE (column3)
    )

### Empty a table

    TRUNCATE schema.table

### Alter a table

    ALTER TABLE schema.table ADD COLUMN columnname VARCHAR(255);
    ALTER TABLE schema.table ADD COLUMN columnname INTEGER;
    ALTER TABLE schema.table ADD COLUMN columnname TEXT;

### Backup a table

    CREATE TABLE new_table AS (SELECT * FROM old_table)

### Delete a table

    DROP TABLE schema.table

## User Management

### Add a user to a database

    GRANT ALL ON schema.table TO username    