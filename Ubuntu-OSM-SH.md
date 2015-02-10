######Installing PostgreSQL/PostGIS on Ubuntu
I had some trouble installing Postgresql/Postgis on my virtual ubuntu. I research around and found out the osm site have the
best way to install both at the same time on ubuntu. This works perfectly as i require Postgis to allow my database to import the require geospatial data. The website is as follows:
http://wiki.openstreetmap.org/wiki/PostGIS/Installation#Ubuntu_14.04_LTS
```
sudo apt-get install postgresql postgresql-contrib postgis postgresql-9.3-postgis-2.1
```
######Installing osm2pgsql to allow style.lua usage
if you use the normal command as such: 
```
sudo apt-get install osm2pgsql
```
you will notice that you aren't allow to use the argument --tag-transform-script. But by using this method of installing osm2pgsql will allow you to install osm2pgsql directly from the osm2pgsql github which enable --tag-transform-script straight away :
```
sudo apt-get install git <- ensure git is installed
git clone git://github.com/openstreetmap/osm2pgsql.git
sudo apt-get install autoconf automake libtool make g++ libboost-dev libboost-system-dev libboost-filesystem-dev libboost-thread-dev libxml2-dev libgeos-dev libgeos++-dev libpq-dev libbz2-dev libproj-dev protobuf-c-compiler libprotobuf-c0-dev lua5.2 liblua5.2-dev libboost-all-dev
cd /osm2pgsql
sudo ./autogen.sh
sudo ./configure --with-boost-libdir=/usr/lib/x86_64-linux-gnu
sudo make
sudo make install
```
To see if it have been installed try to use this command
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
