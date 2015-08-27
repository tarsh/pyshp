# Introduction #

The shapefile.Reader.shapeRecords() method is a simple convenience method which allows you to simultaneously loop through both the geometry and records of a shapefile.

# Details #

Here’s a simple usage example followed by a detailed explanation.

Let’s say you have a simple point-location address shapefile named “addr.shp” with the following structure:

```
GEOMETRY (POINT)          ADDRESS		CITY		STATE		ZIP

[-89.522996, 34.363596]	  718 South 8th		Oxford	        MS		38655
[-89.520695, 34.360863]	  1195 South 11th	Oxford	        MS		38655
[-89.520927, 34.362924]	  805 Fillmore Ave	Oxford	        MS		38655
```


You could then use the shapeRecords method like this:

```
>>> import shapefile
>>> r = shapefile.Reader(“addr”)
>>> sr = r.shapeRecords()
>>> # get the first shaperecord
>>> sr_test = sr[0]
>>> # Look at the geometry of the shape
>>> sr_test.shape.points
[[-89.522996, 34.363596]]
>>> # Look at the attributes of the dbf record
>>> sr_test.record
[‘718 South 8’,’Oxford’,’MS’,’38655’]
>>> # Now let’s iterate through all of them
>>> for sr in r.shapeRecords():
...    print “x: “, sr.points[0][0]
...    print “y: “, sr.points[0][1]
...    # Output just the address field
...    print “Address: “, sr.record[0]
x: -89.522996
y: 34.363596
Address: 718 South 8th
x: -89.520695
y: 34.360863
Address: 1195 South 11th
x: -89.520927
y: 34.362924
Address: 805 Fillmore Ave
```

Here’s how it works.

The shapeRecords() method returns a list.

Each entry in that list is a _ShapeRecord object instance._

A _ShapeRecord object has two attributes: shape, record_

_ShapeRecord.record contains a simple list of the attributes._

_ShapeRecord.shape contains a_Shape object instance.

A _Shape object has, at a minimum, two attributes: shapeType, points_

If the _Shape instance contains a polygon a “parts” attribute will appear.  This attribute contains the index in the point list of the beginning of a “part”.  Parts let you store multiple shapes in a single record._

The shapeType attribute provides a number telling you if the shapefile is  a point, polygon, line, etc. file.  These constants are listed in the shapefile spec document as well as near the top of the source code.

The points is just a list containing lists of the point coordinates.  Two things to note:  If the geometry has multiple parts, such as multiple polygons, the points for all parts are just lumped together.  You must separate them by referencing the parts index list.  Some shape types allow for z and m values which may appear in addition to the x,y pairs.

This method is really just a clumsy convenience method that basically zips up the results of the shapes() and records() methods you are already using.

I have a few blog posts where I call this method as well:

http://geospatialpython.com/2011/02/changing-shapefiles-type.html

http://geospatialpython.com/2011/01/point-in-polygon.html

http://geospatialpython.com/2010/12/dot-density-maps-with-python-and-ogr.html  (in the comments)