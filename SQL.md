## Sql Gists
### Select

    SELECT a.column, count(*) FROM table a WHERE a.column2 IN ( SELECT array_to_string(array_arg(b.column), ',') ) FROM table b WHERE b.column = a.column3 AND b.column2 LIKE '%items.')

### Insert

    INSERT INTO table a (a.column, a.column2) VALUES (1, "Etc")
### Update

    UPDATE table a
### Upsert

    UPSERT
### Delete

    DELETE