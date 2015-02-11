#Extraction of Administrative Boundaries in OSM
The following flow of extraction is based on what i have done to create the individual osm country files. The reason for the lengthy conversion is due to my experience of the inability of some direct conversion. Also, the poly files which i have use are correct but somehow the conversion/extraction loses out some data. So by doing it this manner i was able to get countries osm data.

1. I first extract out the country location from the planet file to a pbf file.
```
osmconvert planet-latest.osm.pbf -B=singapore.poly -o=singapore.pbf
```

2. I next convert my pbf file to an o5m file
```
osmconvert singapore.pbf singapore.o5m
```

3. I next filter out only the administrative boundaries on the map(Two things note: 1.When you extrat out administrative boundaries it will extract out even the waters which belong to the country. If you want to be more specific you have to make sure that natural=coastline is also observed. 2. osmfilter do not support pbf files for filtering, so i have to convert to o5m first then to osm data.)
```
osmfilter singapore.o5m --keep="boundary=administrative">singapore.osm
```

