# Creating a .prj file #

The shapefile format does not allow for specifying the map projection of the data.  As a workaround ESRI invented another file extension called ".prj" which is short for projection.  The prj file contains a WKT (Well-Known Text) string which has all the parameters for the map projection.  So the format is quite simple and was created by the Open GIS Consortium.

But there are several thousand "commonly-used" map projections which were standardized by the European Survey Petroleum Group (EPSG).  And there's no way to accurately detect the projection from the coordinates in the shapefile.  For these reasons the Python Shapefile Library does not currently handle prj files.

If you need a prj file the easiest thing to do is write one yourself.  The following example creates a simple point shapefile and then the corresponding prj file using the WGS 84 "unprojected" WKT.

I've thought about adding the ability to optionally write prj files but the list of "commonly-used" WKT strings is over .5 megs and would be bigger than the shapefile library itself.

The easiest thing to do right now is just figure out what WKT string you need for your data and quickly write a file:

```
import shapefile as sf
filename = 'test/point'

# create the shapefile
w = sf.Writer(sf.POINT)
w.point(37.7793, -122.4192)
w.field('FIRST_FLD')
w.record('First','Point')
w.save(filename)

# create the PRJ file
prj = open("%s.prj" % filename, "w")
epsg = 'GEOGCS["WGS 84",DATUM["WGS_1984",SPHEROID["WGS 84",6378137,298.257223563]],PRIMEM["Greenwich",0],UNIT["degree",0.0174532925199433]]'
prj.write(epsg)
prj.close()
```