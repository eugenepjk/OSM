Use: I wanted to transfer data from the main tables(e.g. osm_point)
PostgreSQL/PostGIS adding of column for 'way' in other tables. I was trying to find out how to create a column for a new table with the way data that we get when we extract out the data from the osm files. Using the following code in the database command line (if you have entered into the database to type the command) we can add a new column for geometry data type for 'way'.

*bold* SELECT AddGeometryColumn ('my_table','column_name',int_srid,'type',dimension);

my_table: Give a designated table name
column_name: Give a designated column name
int_srid: Give the srid of the geometry that it will reproduce on given command.
          Example: 4623, 900913
type: This refers to the geometric type of the table you are using
      Example: POINT, POLYGON, MULTISTRING, LINES, etc.
dimension: This refers to the coordinate type simply(x,y,z)
            2 - refers to using coordinate x, y
            3 - refers to using coordinate x, y, z
