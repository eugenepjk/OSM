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
 psql --dbname DB_NAME -c "$1" -U postgres -> Where $1 is the SQL statement
```

######Entering database
```
 psql -U postgres $DB_NAME
```

######Making a spatial database
```
 psql -U postgres -d $DB_NAME -f /usr/share/postgresql/9.3/contrib/postgis-2.1/postgis.sql 
 psql -U postgres -d $DB_NAME -f /usr/share/postgresql/9.3/contrib/postgis-2.1/spatial_ref_sys.sql
```
