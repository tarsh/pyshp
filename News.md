# Pyshp News #

This page serves as the project news archive and change log.

5/20/2013 - Christian Ledermann created a fork adding the  [\_\_geo\_interface\_\_](https://gist.github.com/sgillies/2217756) community standard for better compatibility to other tools.  His code is [here](https://github.com/cleder/pyshp).  He also created some data format conversion samples [here](https://github.com/cleder/geo_file_conv).  The intent is to roll these changes into the main trunk ASAP.

5/01/2012 - Pre-release of pyshp 1.1.6-beta is available in the Downloads section. This release fixes some serious issues with reading/writing 3D shapefiles.  Download it [here](http://pyshp.googlecode.com/files/shapefile-1.1.6-b.py).

2/28/2012 - Added a brief description of the Reader.shapeRecords() method in the [Wiki](http://code.google.com/p/pyshp/wiki/ShapeRecords)

10/01/2011 - Thanks to a lot of work from memedough, pyshp now has a single code base for Python 2 and 3.  I haven't tested Jython and IronPython yet but they should be covered.  More about this topic is in ([Issue 19](https://code.google.com/p/pyshp/issues/detail?id=19)).

9/27/2011 - You can now read shapefiles from file-like objects in the Python 2 version as well as write to file-like objects.  The documentation has been updated to reflect this change.  There is also a proposal in place to create a common version of the library that runs in both Python 2 and Python 3.  The "usage.py" file has been moved to a restructured text README.txt file for a cleaner installation from pypi.  For now the Python 3 version is a separate branch in subversion and lags behind the Python 2 version in both features and bug fixes.  This difference will be remedied soon one way or another.

9/4/2011 - Significant bug related to blank dbf attributes fixed ([Issue 15](https://code.google.com/p/pyshp/issues/detail?id=15)).  Please upgrade to at least 1.0.6 because sooner or later this bug _will_ bite you.

9/2/2011 - Thanks to prodding and assistance from several users pyshp is now registered on PyPi using setuptools.  So you can install it using any of the setuptools methods (i.e. easy\_install).  The setup.py script is also in the subversion respository.

8/26/11 - Added a fix which robustly handles blank dbf values.  Available in the latest version (1.0.4).

8/20/11 - The latest subversion revision allows you to save shapefiles to file-like objects. Also the Python 3 version has been separated as a branch. As of right now it is several versions behind the Python 2 version and will continue to change at a slower rate until Python 3 reaches critical mass.

5/20/11 - A [pre-release version](http://code.google.com/p/pyshp/downloads/detail?name=shapefile.py) for a new feature allowing you to save to file-like objects instead of just files is available in the Downloads section until it is added to the source tree. The download description provides basic usage.

2/24/11 - A [Geospatial Python Discussion Group](http://groups.google.com/group/geospatialpython) is now available for issues and questions.

2/23/11 - Critical updates regarding measure values, elevation values, and multiple-part polygons have been added to the source tree as version 1.0.  These updates are for the Python 2 version only and not compatible with Python 3 yet.

1/31/11 - There is now a port for Python 3 which has not been well tested. Bug reports are welcome.  The code is available in the Subversion trunk and the documentation is in the Downloads section.