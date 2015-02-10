######Installing PostgreSQL/PostGIS on Ubuntu
I had some trouble installing Postgresql/Postgis on my virtual ubuntu. I research around and found out the osm site have the
best way to install both at the same time on ubuntu. This works perfectly as i require Postgis to allow my database to import the require geospatial data. The website is as follows:
http://wiki.openstreetmap.org/wiki/PostGIS/Installation#Ubuntu_14.04_LTS
```
sudo apt-get install postgresql postgresql-contrib postgis postgresql-9.3-postgis-2.1
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
