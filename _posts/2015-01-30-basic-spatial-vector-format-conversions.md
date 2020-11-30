---
title: Basic Spatial Vector Format Conversions
layout: post
---

For converting between vector formats (shapefile, Mapinfo etc) you can use the
command line tool [ogr2ogr](https://www.gdal.org/ogr2ogr.html) as an alternative
to Universal Translator in Mapinfo. It's really easy to use. Here's how to
convert from shapefile to Mapinfo tab file:

    ogr2ogr -f "MapInfo File" data.tab data.shp

Make a KML for use in Google Earth:

    ogr2ogr -f KML data.kml data.shp

Back to shapefile from the KML:

    ogr2ogr -f "ESRI Shapefile" data.shp data.kml

You get the hang of it. There's a lot of formats, you can see the whole list by
typing `ogr2ogr --formats`. ogr2ogr can also do other things like reprojecting
and clipping vector data. As an example, for using Google Earth you probably
want to use WGS84 instead of the usual MGA56. From doing way too much
converting between projections I know that the EPSG numbers for these are 4326
and 28356. So:

    ogr2ogr -f KML -a_srs EPSG:28356 -t_srs EPSG:4326 data.kml data.shp

Note that converting from Mapinfo to shapefile can cause some grief since
Mapinfo files can have points/lines/polygons in the same file whereas
shapefiles can only have a single type of geometry. You're probably better off
sticking with Universal Translator for this use case.

There's also a tool for converting between raster formats ([gdal_translate](https://www.gdal.org/gdal_translate.html)) but
it's slightly harder to use (tends to mess up nodata values if you don't
specify correctly).
