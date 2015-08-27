
---


## **NOTE: This project has been migrated to [Github](https://github.com/GeospatialPython/pyshp).  This google code site will be available indefinitely.  As of June 16, 2014, the source and some wiki pages have been migrated over.** ##


---


# Overview #
This library reads and writes ESRI Shapefiles in _pure_ Python.  You can read and write shp, shx, and dbf files with all types of geometry.  Everything in the public ESRI shapefile specification is implemented.  This library is compatible with Python versions 2.4 to 3.x.

## _Get Started Instantly_ ##
  1. Download [shapefile.py](http://pyshp.googlecode.com/svn/trunk/shapefile.py)
  1. Start Python
  1. `import shapefile`
  1. Try one of the examples below

OR

Just run:
`easy_install pyshp`

OR

`pip install pyshp`

If you are looking for information on .sbn and .sbx file formats some documentation is available [here](http://geospatialpython.com/2011/10/your-chance-to-make-gis-history.html).

## Latest News ##
8/8/2013 - Please upgrade to PyShp 1.1.9 which fixes issues with polylines, polygons, as well as some z-value corner cases.  This update resolves ([Issue 54](https://code.google.com/p/pyshp/issues/detail?id=54)), ([Issue 55](https://code.google.com/p/pyshp/issues/detail?id=55)), and ([Issue 56](https://code.google.com/p/pyshp/issues/detail?id=56)).


6/23/2013 - Released PyShp 1.1.7! This release fixes several bugs including ([Issue 40](https://code.google.com/p/pyshp/issues/detail?id=40)), ([Issue 37](https://code.google.com/p/pyshp/issues/detail?id=37)), ([Issue 25](https://code.google.com/p/pyshp/issues/detail?id=25)), and ([Issue 22](https://code.google.com/p/pyshp/issues/detail?id=22)). Other improvements include:

  * Added Python geo\_interface convention to export shapefiles as GeoJSON.

  * Used is\_string() method to detect file names passed as unicode strings.

  * Added Reader.iterShapes() method to iterate through geometry records for parsing large files efficiently.

  * Added Reader.iterRecords() method to iterate through dbf records efficiently in large files.

  * Modified shape() method to use iterShapes() if shx  file is not available.

  * Fixed bug which prevents writing the number 0 to dbf fields.

  * Updated _shape() method to calculate and seek the start of the next record. The shapefile spec does not require the content of a geometry record to be as long as the content length defined in the header.  The result is you can delete features without modifying the record header allowing for empty space in records._

  * Added enforcement of closed polygons in the Writer.poly() method.

  * Added unique file name generator to use if no file names are passed to a writer instance when saving (ex. w.save()).  The unique file name is returned as a string.

  * Updated "bbox" property documentation to match Esri specification.

5/20/2013 - Christian Ledermann created a fork adding the  [\_\_geo\_interface\_\_](https://gist.github.com/sgillies/2217756) community standard for better compatibility to other tools.  His code is [here](https://github.com/cleder/pyshp).  He also created some data format conversion samples [here](https://github.com/cleder/geo_file_conv).  The intent is to roll these changes into the main trunk ASAP.  UPDATE - this feature has been added in version 1.1.7 (June 23, 2013).


## License ##

This library is released under the [MIT license](http://www.opensource.org/licenses/mit-license.php) allowing it to be used for both commercial and non-commercial use.  If your organization requires a different license for legal or policy reasons please contact the author through [GeospatialPython.com](http://www.geospatialpython.com).

## Usage ##
The "Source" tab contains the SVN trunk with the latest release. Tagged releases representing relatively stable versions are also in the repository.  The python module "shapefile.py" contains the complete library.

Detailed documentation and examples can be found in the Wiki as well as the "Download" tab.  These files are different formats for the same information.

Below are minimal examples to give you a quick idea of what using the library "feels" like. More examples can also be found on [GeospatialPython.com](http://geospatialpython.com).

Important: For information about map projections, shapefiles, and Python please visit: [http://code.google.com/p/pyshp/wiki/MapProjections](http://code.google.com/p/pyshp/wiki/MapProjections)

### Reading Shapefiles ###

#### Reading Points in Shapes ####
```
>>> import shapefile
>>> sf = shapefile.Reader("shapefiles/blockgroups")
>>> shapes = sf.shapes()
>>> # Read the bounding box from the 4th shape
>>> shapes[3].bbox
[-122.485792, 37.786931000000003, -122.446285, 37.811019000000002]
>>>#  Read the 8th point in the 4th shape
>>> shapes[3].points[7]
[-122.471063, 37.787402999999998]
```

#### Reading Database Attributes ####
```
>>> # Read the field descriptors for the database file
>>> sf.fields
[("DeletionFlag", "C", 1, 0), ["AREA", "N", 18, 5], 
... ["BKG_KEY", "C", 12, 0], ["POP1990", "N", 9, 0], ["POP90_SQMI", "N", 10, 1], 
... ["HOUSEHOLDS", "N", 9, 0], 
... ["MALES", "N", 9, 0], ["FEMALES", "N", 9, 0]]
>>> # Read the 2nd and 3rd field values of the 4th database record
>>> sf.records[3][1:3]
['060750601001', 4715]
```

#### Writing Shapefiles ####
```
>>> import shapefile
>>> # Make a point shapefile
>>> w = shapefile.Writer(shapefile.POINT)
>>> w.point(90.3, 30)
>>> w.point(92, 40)
>>> w.point(-122.4, 30)
>>> w.point(-90, 35.1)
>>> w.field('FIRST_FLD')
>>> w.field('SECOND_FLD','C','40')
>>> w.record('First','Point')
>>> w.record('Second','Point')
>>> w.record('Third','Point')
>>> w.record('Fourth','Point')
>>> w.save('shapefiles/test/point')
>>> # Create a polygon shapefile
>>> w = shapefile.Writer(shapefile.POLYGON)
>>> w.poly(parts=[[[1,5],[5,5],[5,1],[3,3],[1,1]]])
>>> w.field('FIRST_FLD','C','40')
>>> w.field('SECOND_FLD','C','40')
>>> w.record('First','Polygon')
>>> w.save('shapefiles/test/polygon')
```

## Tests ##
The above examples are very simple.  There are many other shortcuts/features listed in the longer usage examples.

The file "README.txt" is a doctest module containing  basic tests which are called if you run "shapefile.py" directly instead of importing it.

The sample shapefile used in the test and the output directory structure are in the "shapefiles" directory in the [trunk](http://code.google.com/p/pyshp/source/browse/#svn%2Ftrunk).

**Bug reports, fixes, improvements are welcome**

Commercial support is available from [NVision Solutions](http://www.NVisionSolutions.com)