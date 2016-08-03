
GIS in Python
================

There are two sets of tools for using GIS in Python: the first is by using python scripts to control ArcGIS, a popular (but expensive) commercial platform; the second is using native python tools.


GeoPandas:
^^^^^^^^^^^
The all-in-one GIS platform for Python is `GeoPandas`, which extends the popular `Pandas` library to also support spatial data. GeoPandas recently released version 0.2, and you can find `docs for 0.2 here <http://www.geopandas.org>`_ .  Hopefully, they're pretty good (full disclosure, I wrote many of them!)

You can also find a `a full course of geospatial analysis using GeoPandas <http://darribas.org/gds15/>`_ .

And a short stand-alone `tutorial here <https://gist.github.com/jorisvandenbossche/7b30ed43366a85af8626>`_ .


Native Python GIS Tools
-------------------------
GeoPandas bundles a lot of separate libraries, but if you don't want to use GeoPandas, you are welcome to use these libraries on their own. But for context, here are the main python GIS libraries:

* `Fiona <https://pypi.python.org/pypi/Fiona>`_: Tools for importing and exporting vector data from various formats like shapefile.

*  `Rasterio <https://pypi.python.org/pypi/rasterio>`_: Tools for importing and exporting raster data from various formats

* `PyProj <https://pypi.python.org/pypi/pyproj>`_: Tools for defining and transforming the datum and projections of spatial data

* `Shapely <https://pypi.python.org/pypi/Shapely>`_: Tools for spatial analytics, like testing for intersections, measuring areas, etc. Note that this is basically a tool for analyzing 2-dimensional cartesian shapes -- it has no facilities for managing projections. That you have to do with PyProj before you start manipulations with shapely.

* `RTree <https://pypi.python.org/pypi/Rtree/>`_: Spatial analytics (like intersections) can be relatively computationally difficult and thus slow. For example, if you want to do something like a spatial join of millions of points to a shapefile of polygons, you want to use what's called a "Spatial Index" tool like RTree. Basically, for each point, RTree will very quickly identify a list of polygons with which that point ''might'' intersect (this list will always include the polygon that the point intersects with, but also some others. In other words, it has no false negatives, but lots of false positives). You then use a slower but more accurate tool like Shapely to check more accurately whether your point lies in each of these candidates to find the one true intersecting polygon.

* `CartoPy <http://scitools.org.uk/cartopy/>`_ and `Descartes <https://pypi.python.org/pypi/descartes>`_: Cartography tools for making pretty maps. Cartopy is basically the successor to Basemap, which you may also read about on some forums.

(Side note: most of which are actually just Python interfaces for extremely fast C / C++ libraries published by the OSGeo collective that back most geo-spatial tools, regardless of the language you're using.)

Here's a `good tutorial on all major libraries and GeoPandas <https://www.youtube.com/watch?v=HzPSVwyP2Y0>`_. The only problem is that the presenter (who actually started GeoPandas) doesn't get to GeoPandas till 2 hours 32 minutes (`direct link to that point <https://youtu.be/HzPSVwyP2Y0?t=2h32m39s>`_). The whole tutorial is great if you want to really understand the eco-system, but there's much to be said for jumping to the GeoPandas section.


ArcPy: Controlling ArcGIS using Python
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To use ArcPy -- the Python module for manipulating ArcGIS -- you first need an ArcGIS license.

If you have ArcGIS and are familiar with it's use through the normal point-and-click interface, you can find an `arcpy tutorial here <http://www.nickeubank.com/gis-in-python/>`_ I wrote a few years ago. It assumes no real knowledge of Python so it may be a little slow and it's a little old and clunky, but should cover what you need to know.
