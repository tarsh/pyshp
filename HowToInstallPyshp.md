**Update 09/04/11: The Python Shapefile Libray is now available on the Python Package Index via setuptools.**

The package location is:
[http://pypi.python.org/pypi/pyshp](http://pypi.python.org/pypi/pyshp)

So now you can run:

` easy_install pyshp `

Pypi also lets other developers create dependencies for pyshp to include it in the distribution of other packages.

Thanks to the users who helped make this feature a priority.


# Quick Installation #

The Python Shapefile is completely contained in a single file named "shapefile.py".  You can download it for Python 2.x by going [here](http://pyshp.googlecode.com/svn/trunk/Python2/shapefile.py) and choosing "File->Save Page As" in your browser.

You should put this file in your working directory or your Python distribution's "site-packages" directory.  Either way next time you run Python you should be able to successfully execute:
```
import shapefile
```

One file. Pure Python. That's it.  One day I'll make it compatible with disutils but it's really simple now.