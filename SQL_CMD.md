######Create Table
```
CREATE TABLE table_name (column1 datatype1, column2 datatype2);
eg. CREATE TABLE my_table (id int, name varchar(60),mydate timestamp);
```

######Search for data
```
SELECT * FROM table_name WHERE column1='';
SELECT * FROM table_name WHERE column1='' ORDER BY column1 [asc/desc];
SELECT DISTINCT column1 FROM table_name WHERE column1 is not null GROUP BY column1;
SELECT COUNT(*) FROM table_name WHERE column1 is not null;
SELECT DISTINCT column1, COUNT(column1) WHERE column1 is not null GROUP BY column1;
```

######Insert data
```
INSERT INTO table_name VALUES (value1,value2,value3);
INSERT INTO table_name (column1,column2,column3) VALUES (value1,value2,value3);
```

######Transfer data from Table1 to Table2
```
table1(id, name, timechanged);
table2(id, name);
INSERT INTO table1
 SELECT id, name, now() FROM table2;
```

######Update table data
```
UPDATE table_name SET column1=value1,column2=value2 WHERE some_column=some_value;
``` 
