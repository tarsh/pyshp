# Introduction #

Elevation values, known as "Z" values allow you to create 3-dimensional shapefiles.  Working with elevation values in the Python Shapefile Library is easy but requires a step which hasn't been well documented until now.  Make sure you are working with at least version 1.0 ([revision 24](https://code.google.com/p/pyshp/source/detail?r=24) in the repository) as previous versions have a bug that prevents elevation values from being written properly as well as another bug which occurs when creating certain polygon .

# Details #

The shapefile specification allows for three types of 3-dimensional shapefiles:

**PointZ - a 3D point shapefile** PolylineZ - a 3D line shapefile
**PolygonZ - a 3D polygon shapefile**

The most important thing to remember is to explicitly set the shape type of each record to the correct shape type or it will default to a 2-dimensional shape. Eventually the library will automatically detect the elevation type.

Here is a brief example of creating a PolygonZ shapefile:

```
import shapefile
w = shapefile.Writer(shapeType=shapefile.POLYGONZ)
# OR you can type
# w = shapefile.Writer(shapeType=15)
w.poly([[[-89.0, 33, 12], [-90, 31, 11], [-91, 30, 12]]], shapeType=15)
w.field("NAME")
w.record("PolyZTest")
w.save("MyPolyZ")
```

When you read 3D shapefiles the elevation values will be stored separately:

```
>>> import shapefile
>>> r = shapefile.Reader("MyPolyZ")
>>> r.shapes()[0].points
[[-89.0, 33.0], [-90.0, 31.0], [-91.0, 30.0]]
>>> r.shapes()[0].z
[12, 11, 12]
```