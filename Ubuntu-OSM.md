######Installing PostgreSQL/PostGIS on Ubuntu
source: http://wiki.openstreetmap.org/wiki/PostGIS/Installation#Ubuntu_14.04_LTS  
I want to have both PostgreSQL/PostGIS to be installed in a way so that i can create a spatial database later in my program. To do so i use the following which is found on the osm wiki website
```
sudo apt-get install postgresql postgresql-contrib postgis postgresql-9.3-postgis-2.1
```

######Installing osm2pgsql to allow style.lua usage
if you use the normal command as such: 
```
sudo apt-get install osm2pgsql
```
you will notice that you aren't allow to use the argument --tag-transform-script. I use the following installation procedure instead which allows the direct installation from osm github site. This allows me to use the arguement --tag-transform-script immediately.
```
git clone git://github.com/openstreetmap/osm2pgsql.git
sudo apt-get install autoconf automake libtool make g++ libboost-dev libboost-system-dev libboost-filesystem-dev libboost-thread-dev libxml2-dev libgeos-dev libgeos++-dev libpq-dev libbz2-dev libproj-dev protobuf-c-compiler libprotobuf-c0-dev lua5.2 liblua5.2-dev libboost-all-dev
cd /osm2pgsql
sudo ./autogen.sh
sudo ./configure --with-boost-libdir=/usr/lib/x86_64-linux-gnu
sudo make
sudo make install
```
to see if the --tag-transform-script is avaliable give the following command:
```
osm2pgsql -v -h
```

######Creating database
``` 
createdb -U postgres $DB_NAME
```

######Droping database
``` 
dropdb -U postgres $DB_NAME
```

######Execute Command without logging into database
``` 
psql --dbname $DB_NAME -c "$1" -U postgres -> Where $1 is the SQL statement
```

######Entering database
``` 
psql -U postgres $DB_NAME
```

######Making a spatial database
Do take note of the postgresql/postgis version number. The location of the file will defer from there.
```
 psql -U postgres -d $DB_NAME -f /usr/share/postgresql/9.3/contrib/postgis-2.1/postgis.sql 
 psql -U postgres -d $DB_NAME -f /usr/share/postgresql/9.3/contrib/postgis-2.1/spatial_ref_sys.sql
```

######Allow SQL to handle hstore datatype
In PostgreSQL database we have to create an extension for hstore before we can assign it as a datatype for tags.
```
CREATE EXTENSION hstore;
```

######Adding of Geometry datatype in SQL
source:http://postgis.net/docs/AddGeometryColumn.html  
I would like to spilt my data from the bulk of osm table to more comprehensive table in another database. To allow my table to accept geometry as a datatype we have to ensure that you have a spatial database(Making a spatial database). After that we can enter the following in a SQL commandline:
```
SELECT AddGeometryColumn ('my_table','column_name',int_srid,'type',dimension);
  my_table: Give a designated table name
  column_name: Give the column a name (eg. 'way' is geometry of osm database)
  int_srid: this supplies the geometry type of the column(eg. 900913, 4623)
  type: this is to define the column is what type of geomtery(eg. POINT, LINESTRING, POLYGON)
  dimension: this refers to the coordinate type(2-[x,y] /3-[x,y,z])
```
An example:
```
SELECT AddGeometryColumn ('barrier','way',4623,'POLYGON',2);
```

######Cannot select natural issues
When i try to do the following commnad in SQL command line:
```
SELECT * FROM osm_point WHERE natural is not null;
```
It will give the following error
>ERROR:  syntax error at or near "is"  
>LINE 1: SELECT * FROM osm_point where natural is not null;  
>                                              ^  

the problem with this command is that natural is part of the Postgresql functions so instead osm have create natural as "natural". So by doing the following command:
```
SELECT * FROM osm_point WHERE "natural" is not null;
```
This should display only the natural where it is not null

######Conversion of PostgreSQL/PostGIS data to Shapefiles
source:http://gis.stackexchange.com/questions/55206/how-can-i-get-a-shapefile-from-a-postgis-query
```
pgsql2shp -f <path to output shapefile> -h <hostname> -u <username> -P <password> databasename "<query>"
```
