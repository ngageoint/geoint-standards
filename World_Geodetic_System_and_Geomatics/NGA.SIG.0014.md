

NGA.SIG.0014_v0.1_PROJRAS






NATIONAL GEOSPATIAL-INTELLIGENCE AGENCY (NGA) 
STANDARDIZATION DOCUMENT
Implementation Practice

Map Projections for Tiled Raster Graphics


2015-01-09

Version 0.1



OFFICE OF GEOMATICS


 
Table of Contents

1.	Scope	  1
2.	Authority	  1
3.	References	  1
4.	Background	  2
5.	Tiled Mercator 	  4
6.	Tiled Transverse Mercator	  6
7.	Tiled Polar Stereographic 	  7
8.	Summary	  10




Appendices 
A1.	Scale	  A-1
A2.	Tiled Mercator zoom-levels scale sets	  A-1
A3.	Tiled transverse Mercator zoom-levels scale sets	  A-2
A4.	Tiled polar stereographic zoom-levels scale sets	  A-2
A5.	The universal zoom-levels scale set	  A-2
A6.	Tiled Mercator, again	  A-4
A7.	Tiled transverse Mercator, again	  A-6
A8.	Tiled polar stereographic, again	  A-6



List of Tables
Table 1 – Universal zoom-levels scale set	  A-3
Table 2 – Tiled Mercator zoom-levels scale set	  A-8
Table 3 – Tiled transverse Mercator zoom-levels scale set	  A-13
Table 4 – Tiled polar stereographic zoom-levels scale set	  A-24


 
1. Scope 

This document specifies the map-projections and tile-pyramids that are authorized for maps and imagery produced as zoom-able tiled raster-graphics.  Formerly, the “web-Mercator” and Plate Carrée projections were considered appropriate for this purpose.  This document specifies what should be used instead.  These terms are explained below.

This document treats raster-graphics exclusively.  Vector graphics (feature data) are not covered.  This document assumes that the raster graphics conform to one of the commonly used device-independent formats, such as PNG, JPEG, JPEG2000, BMP, etc. 

This document is written especially for the developers of data and software for mobile and hand-held devices (e.g. “smart phones”) who will be adopting the OGC GeoPackage Encoding Standard (see 3.10) and the related implementation interoperability standard (see 3.11), but is not limited to those devices, applications, and software environments.


2. Authority 

The National Geospatial-Intelligence Agency (NGA) serves as the Functional Manager for GEOINT to the National System of Geospatial-Intelligence (NSG).  As such, NGA is responsible for specifying coordinate systems and map-projections that are consistent with the World Geodetic System of 1984 and suitable for the broad range of NSG usages, including navigation, targeting, simulations, mission planning, and geographic analysis.  

As the NSG Functional Manager for GEOINT, NGA issued NGA.SIG.0011_1.0_WEBMERC, “Web Mercator Map Projection” forbidding the use of “web-Mercator” (also called pseudo-Mercator and other names) “for the acquisition, visualization, exploitation, and exchange of any GEOINT data for the NSG”.  By the same authority, this document now specifies what should be used in place of web-Mercator for tiled raster graphics. 

NGA.SIG.0011_1.0_WEBMERC was adopted by the Department of Defense (DoD) Information Technology Standards and Profile Registry (DISR) in August, 2014.


3. References

	3.1 Department of Defense Directive 5105.60 (DoDD 5105.60), “Subject:  National Geospatial-Intelligence Agency (NGA)”, July 29, 2009 

	3.2 MIL-STD-2401, Department of Defense Standard Practice “Department of Defense World Geodetic System (WGS)”, 11 January 1994

	3.3 CJCSI 3900.01C, “Position (Point and Area) Reference Procedures”, 30 June 2007

	3.4 CJCSI 6130.01E, “2013 CJCS Master Positioning, Navigation, and Timing Plan (MPNTP)”, 1 May 2013

	3.5 NGA.STND.0036_1.0_WGS84, "Department of Defense World Geodetic System 1984, Its Definition and Relationships With Local Geodetic Systems", Fourth Edition [formerly NIMA Technical Report TR8350.2]

	3.6 NGA.SIG.0011_1.0_WEBMERC, “Web Mercator Map Projection”

	3.7 NGA.SIG.0012_2.0.0_UTMUPS, “The Universal Grids and the Transverse Mercator and Polar Stereographic Map Projections”

	3.8 USGS Professional Paper:1395, “Map Projections: A Working Manual”, Snyder, John P., 1987

	3.9 OGP Publication 373-7-2 – Geomatics Guidance Note number 7, part 2 – June 2013

	3.10 OGC GeoPackage Encoding Standard, OCG 12-128r10, approval date 2014-01-19.

	3.11 NGA.IP.xxxx_x.x, National System for Geospatial Intelligence (NSG) GeoPackage Encoding Standard 1.0 Implementation Interoperability Standard (DRAFT)


4. Background

	4.1 All modern display devices are, in simple terms, raster devices.  The display portion of a television, computer, tablet, or smart-phone is organized as rows and columns of square dots called pixels or rasters.  The file formats, PNG, JPEG, etc., are device-independent abstractions of the display hardware.  The mapping of pixels in the file to pixels of the display hardware is an important engineering problem, but is outside the scope of this document.  This document pertains to the raster graphics file.

	4.2 Rasters and vectors are different ways to organize the same graphical information.  There are many graphical elements; a line segment will illustrate the difference.  In vector graphics, a line segment consists of the  coordinates of the endpoints, a code (typically an integer) for the line style (solid, dashed, dash-dotted etc.), a code (typically an integer or short list of integers) for the color, and a code or number for the line thickness.  In raster graphics, a line segment is the collection (subset) of all the pixels that depict it.  The set of pixels may be colorized or monochrome; they won’t be contiguous if the line is not solid.  

	4.3 Raster graphics and vector graphics (feature data) may be included together in a geopackage.  A geopackage is a container format analogous to the way a ZIP file is a container for files of disparate formats.  References 3.10 and 3.11 specify the required and allowed contents of a geopackage.  This document is concerned solely with the raster graphics components of geopackages.

	4.4 Raster graphics can be tiled or untiled.  NGA’s program to scan paper maps and charts and make them available digitally yields untiled raster graphics – typically one large JPEG2000 file for the entire sheet.  Internet-accessible road maps such as Google Maps are tiled raster graphics.  Mouse-ing over an area of interest in Google Maps and performing Save As will yield a PNG file for the tile that contains the point selected.   There is no entire sheet.  There are many tiles.  This document pertains exclusively to tiled raster graphics.

	4.5 The operation of selecting a portion of a tiled raster graphic, and re-displaying it at larger scale is called “zooming-in”.  The reverse is “zooming-out”.  Zooming-in can happen two ways:  (i) Using the same file (PNG, JPEG, other), the file pixels are mapped to a greater number of device pixels than before.  The same symbols and labels are shown, enlarged; feature selection is unchanged.  Or, (ii) using another file (PNG, JPEG, other), new detail is portrayed; symbols and labels are changed or re-sized relative to the features.  In this document, zooming, zoom-able, and zoom levels refer to the latter process, i.e. (ii).    

4.6 In accordance with References 3.10 and 3.11, a tile is 256 pixels wide by 256 pixels tall, making all tiles are square in shape.  This is true for every zoom-level.  Columns of pixels and columns of tiles are numbered from left to right.  Rows of pixels and rows of tiles are numbered from top to bottom.  

	4.7 Also in accordance with References 3.10 and 3.11, there are at least 25 zoom levels, numbered 0, 1, 2, 3, … 24.  Zoom level 0 is the extreme of zooming-out.   Zoom level   has  tiles across and  tiles up (or down).  Zoom level   covers the same portion of the Earth as zoom level   but with twice as many tiles (in each direction) and therefore, presumably, twice as much detail.  The collection of all tiles for all zoom-levels is called the tile pyramid.

4.8 A map, chart, or piece of imagery requires a map-projection.  A map-projection is the procedure, usually mathematical, by which points on an ellipsoid model of the Earth are either (i) assigned to pixels in a raster-graphics product, or (ii) assigned to rectangular coordinates in a plane.  The number pairs   can be utilized in vector-graphics and grid coordinates, as well as ingredients to procedure (i).  This document is concerned mainly with (i) and partly with (ii) as a means to accomplish (i).

4.9 Web-Mercator is a map-projection based on the controversial idea that the proper formulas for the Mercator projection of the WGS 84 ellipsoid should be shortened (modified) in a particular way for (i) ease of implementation and (ii) efficiency of the early primitive hand-held devices.  It should not be used for either raster or vector graphics.  See Reference 3.6.  Web-Mercator has code EPSG::3857 and is also called pseudo-Mercator.

4.10 Plate Carrée is a map projection based on the simple idea that   should be the longitude (in decimal degrees, say) and   should be the latitude in the same units.  ESRI’s ArcGIS software calls this scheme “Unprojected” indicating that it is merely the option by default (“I didn’t think about choosing a map-projection”).  This document allows Plate Carrée for vector graphics (feature data), but prohibits it for tiled raster graphics.  Plate Carrée has the code EPSG::4326.
 

5. Tiled Mercator

This section specifies “tiled Mercator”.  It is the (standard) ellipsoidally-correct Mercator projection modified slightly for zoom-able tiled raster graphics.  The modifications – scale and origins – reflect the fact that Mercator as raster graphics is a different species than Mercator as paper map or Mercator as world-wide grid coordinates.

The details are divided into several subsections:  ellipsoid parameters, forward mapping equations, and inverse mapping equations.

	5.1 Ellipsoid parameters

The WGS 84 ellipsoid shall be employed, and its parameters shall be computed as follows:

 	

The names of these constants are:  semi-major axis ( ), inverse flattening ( ), flattening ( ), eccentricity-squared ( ), and eccentricity ( ).  It is unfortunate that the eccentricity and the base of the natural logarithms use the same letter  .  In this document, the latter usage,  , will be notated  .  

	5.2 Forward mapping equations

For zoom level  , the equations to convert longitude ( , in radians) and latitude ( , in radians) to pixel column number ( , counting from the left) and pixel row number ( , counting down from the top) are:

 
 
Notes:

One radian is  degrees.   (“lambda”) is required to lie in the interval  , which in degrees is the interval from   to  .    (“phi”) is required to lie in the interval defined by the inequality,  .  In degrees, this works out to  as the extremes of allowed latitude.   The function  is the inverse hyperbolic tangent.   is the greatest integer less than or equal to  .    is the leftmost pixel column and   is the rightmost pixel column, counting continuously across tile boundaries, which occur every 256 pixels.     is the topmost pixel row and   is the bottommost pixel row, counting continuously across tile boundaries, which occur every 256 pixels.   


	5.3 Inverse mapping equations

For zoom level  , the equations to convert pixel column number ( ) and pixel row number ( ) to longitude ( ) and latitude ( )  are:

 
 

where
 

Notes:  

A pixel is not a geometric point.  In the above procedure, its center is adopted as its pinpoint position.    is the inverse sine (“arcsin”);  is the hyperbolic tangent; and  is the exponential function to the base given by Euler’s number,    
6. Tiled transverse Mercator

This section specifies “tiled transverse Mercator”.  It is the (standard) ellipsoidally-correct transverse Mercator projection modified slightly for zoom-able tiled raster graphics.  The modifications – scale and origins – reflect the fact that transverse Mercator as raster graphics is a different species than transverse Mercator as paper map (e.g. TLM50’s) or transverse Mercator as grid coordinates (e.g. UTM coordinates).

The details are divided into several subsections:  ellipsoid parameters, transverse Mercator constants, central meridian, forward mapping equations, and inverse mapping equations. 

	6.1 Ellipsoid parameters 

See Section 5.1, above.

	6.2 Transverse Mercator constants

See section 3.2 of NGA.SIG.0012_2.0.0_UTMUPS for the values of constants   and see Section 3.5 of the same document for the values of constants  .  

	6.3 Central meridian 

Let  be the longitude (in radians) of the central meridian.  Its degree equivalent must be an integer that is divisible by 3 but not by 2.  In other words, it must be one of the values allowed for Universal Transverse Mercator (UTM) coordinates.

	6.4 Forward mapping equations

Let   and   be the functions defined in Section 3.2 of NGA.SIG.0012_2.0.0_UTMUPS.  For zoom level  , the equations to convert longitude ( , in radians) and latitude ( , in radians) to pixel column number ( , counting from the left) and pixel row number ( , counting down from the top) are:
 
 
Notes:

One radian is  degrees.  Consistent with the Notes to Section 5.2,   is the greatest integer less than or equal to  ,    is the leftmost pixel column, and   is the rightmost pixel column counting continuously across tile boundaries, which occur every 256 pixels.   Also consistent with the Notes to Section 5.2,   is the topmost pixel row and   is the bottommost pixel row, counting continuously across tile boundaries, which occur every 256 pixels.

 (“lambda”) is required to lie in the interval  , and   (“phi”) is required to lie in the interval   but there is a further restriction.  It is required that at least one of the following must be true:    must be within  radians (i.e.  ) of either the central meridian ( ) or the anti-central meridian ( ) , or   must be within  radians (i.e.  ) of either the North Pole or the South Pole.   This is discussed also in Section 3.7 of NGA.SIG.0012_2.0.0_UTMUPS.  

	6.5 Inverse mapping equations

Let   and   be the functions defined in Section 3.5 of NGA.SIG.0012_2.0.0_UTMUPS.  For zoom level  , the equations to convert pixel column number ( ) and pixel row number ( ) to longitude ( ) and latitude ( )  are:

 

 
Notes:  

A pixel is not a geometric point.  In the above procedure, its center is adopted as its pinpoint position.  For ease of reading the above formulas, note that functions   and   take the same two arguments in the same order.  


7. Tiled polar stereographic

This section specifies “tiled polar stereographic”.  It is the (standard) ellipsoidally-correct polar stereographic projection modified in a particular way for zoom-able tiled raster graphics.  The modifications – scale and origins – reflect the fact that polar stereographic as raster graphics is a different species than polar stereographic as paper maps (e.g. some aeronautical charts) or polar stereographic as grid coordinates (e.g. UPS coordinates).  This section gives the north polar stereographic.  

The details are divided into several subsections:  ellipsoid parameters, polar stereographic constants, polar stereographic parameters, forward mapping equations, and inverse mapping equations. 

	7.1 Ellipsoid parameters  

These are the same as those as in Section 5.1, above.

	7.2 Polar stereographic constants

See section 8.1 of NGA.SIG.0012_2.0.0_UTMUPS for the value of the constant  .  

	7.3 Polar stereographic parameters

The allowed values for the central meridian ( , in radians) are  .  The degree equivalents are   There will be two special latitudes. The first is a standard parallel chosen to be  radians (i.e.  ).  From this is obtained the following scale reduction factor:

  

where function  is defined in Section 8.1 of NGA.SIG.0012_2.0.0_UTMUPS.  The second special latitude will refer to the parallel circle that is tangent to the boundaries of the level-0 tile.  This is discussed later.

	7.4 Forward mapping equations

Let   and   be the functions defined in Section 8.1 of NGA.SIG.0012_2.0.0_UTMUPS.  For zoom level  , the equations to convert longitude ( , in radians) and latitude ( , in radians) to pixel column number ( , counting from the left) and pixel row number ( , counting down from the top) are:

For the NORTH polar stereographic projection, 

 
 

For the SOUTH polar stereographic projection, 

 

 

Notes:

One radian is  degrees.  Consistent with the Notes to Section 5.2,   is the greatest integer less than or equal to  ,    is the leftmost pixel column, and   is the rightmost pixel column counting continuously across tile boundaries, which occur every 256 pixels.   Also consistent with the Notes to Section 5.2,   is the topmost pixel row and   is the bottommost pixel row, counting continuously across tile boundaries, which occur every 256 pixels.

The arithmetic indicated in the above formulas can be performed, as follows:
 
 

 

 (“lambda”) is required to lie in the interval  , and   (“phi”) is required to lie in the interval  , and these further restrictions apply:

 
 

Note that the inequalities for   and   are strict in a different place.


	7.5 Inverse mapping equations

Let   and   be the functions defined in Section 8.2 of NGA.SIG.0012_2.0.0_UTMUPS.  For zoom level  , the equations to convert pixel column number ( ) and pixel row number ( ) to longitude ( ) and latitude ( )  are:


For the NORTH polar stereographic projection, 

 

 

For the SOUTH polar stereographic projection, 

 
 

Notes:  

A pixel is not a geometric point.  In the above procedures, its center is adopted as its pinpoint position.  For ease of reading the above formulas, note that for NORTH and separately for SOUTH, the functions   and   take the same two arguments in the same order.  

For NORTH polar stereographic, the parallel circle tangent to the boundaries of the level-0 tile is 25.0560°S, computed by the expression,  .   For SOUTH, it is 25.0560°N

8. Summary

NGA and DoD require that mobile and hand-held devices employ a tiled map-projection within a short list of options.  The specifications above, namely tiled Mercator, tiled transverse Mercator and tiled polar stereographic, are that short list.

The forgoing sections make a complete specification.  The appendices that follow are informative.













(This page is intentionally blank) 



NGA.SIG.0014_v0.1_PROJRAS






NATIONAL GEOSPATIAL-INTELLIGENCE AGENCY (NGA) 
STANDARDIZATION DOCUMENT
Implementation Practice

Map Projections for Tiled Raster Graphics


Appendices


 
A1. Scale

Beginning here, several sections are devoted to the subject of scale; they provide information about the scale of the tiled map-projections (raster graphics) specified above.  Scale is as important to raster graphics as it is to paper maps or grid coordinates, but, of necessity, it is specified differently for raster graphics than for the others.

A1.1 The scale of raster graphics is typically stated as a number of meters/pixel (“meters per pixel”).  For example, tiled Mercator, at zoom level 10 and latitude 11° has the value 150.084 meters/pixel, found in Table 2.  This means that one pixel on the map corresponds to 150.084 meters on the ground at that latitude.

A1.2 Strictly speaking, the number 150.084 meters/pixel is reciprocal scale not scale.  This is explained by an analogy with paper maps.  One cm on the map corresponds to 50,000 cm on the ground, in the case of NGA’s product “TLM50”.  The scale is  , not 50,000.  The number 50,000 is the reciprocal scale.  Scale is always  and reciprocal-scale is always the inverse ratio.  In the case of raster graphics, the unit of “map distance” is the pixel.  Also, “on the ground” means “on the Earth” and this is short for “on the ellipsoid model of the Earth”.

A1.3 Meters/pixel is reciprocal scale.  Understanding this will make the tables more intuitive.  In Table 2, heading north to Greenland, where the scale is understood to be larger, corresponds to smaller values for meters/pixel.

A1.4 The scale and reciprocal scale depend on the zoom-level and the location on Earth.  For tiled Mercator and tiled polar stereographic, the location needs only the latitude; the longitude can be ignored.  For tiled transverse Mercator, the location needs both the latitude and the longitude.

A1.5 A zoom-levels scale set is the listing of meters/pixel for every zoom-level at a particular point (or relatively small area containing the point).  It is location dependent.  Said another way, specifying a zoom-levels scale set always begs the question of where the zoom-levels scale set is true.


A2. Tiled Mercator zoom-levels scale sets

Meters/pixel for tiled Mercator are tabulated in Table 2 for every zoom level n and every degree of latitude (within range).  The latitudes,   and   have the same value for meters/pixel; it suffices to publish tables for the northern hemisphere only.

The tables were computed using this formula:

reciprocal scale   meters/pixel

where 
 


A3. Tiled transverse Mercator zoom-levels scale sets

Meters/pixel for tiled transverse Mercator are tabulated in Table 3 for every zoom level n, every 5° of latitude from the Equator to 85°N and every 1° of longitude from the central-meridian to central-meridian plus 10°.  Because of symmetry, it suffices to publish tables for one quadrant only (East of the central meridian; north of the Equator).

The tables were computed using this formula:

reciprocal scale   meters/pixel

where 
f3 refers to the function defined in section 6.3 of NGA.SIG.0012_2.0.0_UTMUPS, and

 

Note that   here has a close but different value than for tiled Mercator in the previous section.  The fact that they are different is due to the ellipsoidal shape of the Earth.  The fact that they are close is due to the nearly spherical shape of the ellipsoid.
 

A4. Tiled polar stereographic zoom-levels scale sets

Meters/pixel for the tiled polar stereographic projection are tabulated in Table 4 for every zoom level and every 1° of latitude from the Pole to the Equator.  Because of symmetry, it suffices to publish the tables for the NORTH polar stereographic only.

The tables were computed using this formula:

reciprocal scale   meters/pixel

where
 f3 refers to the function in section 8.1 of NGA.SIG.0012_2.0.0_UTMUPS, and

	 


A5. The universal zoom-levels scale set

This section restates the scale properties of the tiled map-projections defined in this document.  

A5.1 Paper maps offer a helpful analogy.  Without changing the scale, there is more than one way to report the scale.  On the walls of NGA hang copies of a world map on the Mercator projection.  The stated scale is 1:22,000,000 at the Equator, appropriate for a world map showing both hemispheres.  Yet, it would be equally valid to state the scale as 1:11,000,000 at latitude 60° (because  and few decimals are specified).  The scale could be so restated; only the margin note would change; no rework by the cartographer would be required.

A5.2 In the summer and fall of 2014, the DoD inter-agency discussions that led to the specifications in this document formulated the following loose requirement.  If possible, a zoom-level should have the same meaning across all map-projections and over the entire globe.  This is impossible on both counts, but it did lead to the idea of a universal zoom-levels scale set, which roughly meets this requirement to some extent.

A5.3 The universal zoom-levels scale set is stated below.  The specification of where it is true for each tiled map-projection will follow.

Zoom Level	Meters/pixel
0	134217.728
1	67108.864
2	33554.432
3	16777.216
4	8388.608
5	4194.304
6	2097.152
7	1048.576
8	524.288
9	262.144
10	131.072
11	65.536
12	32.768
13	16.384
14	8.192
15	4.096
16	2.048
17	1.024
18	0.512
19	0.256
20	0.128
21	0.064
22	0.032
23	0.016
24	0.008
Table 1.  Universal zoom-levels scale set

The meters/pixel value for zoom level   is  .  The numbers in the above table are exact.  In millimeters, they are powers of two, i.e.  millimeters for zoom level n.  At zoom level 27, if the table were extended that far, the (reciprocal) scale would be one millimeter per pixel, appropriate to make an image of a survey marker’s inscriptions.

A5.4 For tiled Mercator (Section 5), the localities where the universal zoom-levels scale set (Section A5.3) is true are latitudes ±31.0606963703645°

A5.5 For tiled transverse Mercator (Section 6), the locality where the universal zoom-levels scale set (Section A5.3) is true is not simple.  There is no curve of constant latitude or constant longitude that defines it.  Instead two accurate points are given along with the approximate principle that the locality of true scale is found at points the same distance from the central meridian as these two points.  

Point 1 lies on the Equator at 30.700524332812° of longitude east of the central meridian.

Point 2 lies on the meridian 90° east of the central meridian at co-latitude 31°. (FIXME) 

The above points lie in the quadrant north of the Equator and east of the central meridian.  The other quadrants have symmetrically placed points of true scale.

A5.6 For the tiled polar stereographic projection (Section 7), the locality where the universal zoom-levels scale set (Section A5.3) is true is 31° of latitude from the Pole, exactly.  For the NORTH polar stereographic, this means latitude 59°N.   For the SOUTH, this means latitude 59°S.

A5.7 The universal zoom-levels scale set serves another purpose.  It provides (at every zoom level) a discretization of the map-projection plane in a manner independent of the choice of the map-projection.  Let zoom level 24 be an example.  The plane is discretized as little squares, 0.008 meters on a side.  The squares become the pixels and all tiling details are decided by this.  Choice of map-projection and its parameters, within classical treatments like John P. Snyder’s Map Projections: A Working Manual or NGA’s NGA.SIG.0012_2.0.0_UTMUPS, would be the only remaining matters for the construction of new (or the above) tiled map-projections.  


A6. Tiled Mercator, again

This section re-states the forward mapping equations for tiled Mercator, taking inspiration from the universal zoom-levels scale set.  Previously given equations (Section 5) were unencumbered by intermediate grid coordinates  , i.e. the conversion was simply from   to  . Here we introduce  and re-arrange some constants (multipliers) so that   to   conforms to classical treatments (see section A5.7) and  to  is generically given, i.e. independent of the map-projection and its parameters (again see section A5.7).  

	A6.1 The forward mapping equations are:

 
 

 
 

	where 
  and n is the zoom level.
	
	A6.2 The EPSG operation-method-code for the above   to   conversion is EPSG::9804 with these values for its required parameters:
•	 
•	 
•	  is the above  
•	FE 
•	FN 

	A6.3 The current Well-Known-Text format (as of 2014 December) for the above EPSG parameters, copied from NGA.IP.xxxx_x.x, National System for Geospatial Intelligence (NSG) GeoPackage Encoding Standard 1.0 Implementation Interoperability Standard (DRAFT), is the following:

•	PROJECTION["Mercator_variant_A", AUTHORITY["EPSG","9804"]],
•	PARAMETER["Latitude of natural origin",0],
•	PARAMETER["Longitude of natural origin",0],
•	PARAMETER["Scale factor at natural origin", 0.857385503731176],
•	PARAMETER[“False easting”,0],
•	PARAMETER[“False northing”,0],		

	A6.4 The new proposed Well-Known-Text format for the above EPSG parameters, copied from the same document, is the following:

•	METHOD[“Mercator (variant A)”,ID[“EPSG”,”9804”]],
•	PARAMETER[“Latitude of natural origin”,0, ANGLEUNIT[“degree”,0.0174532925199433]],
•	PARAMETER[“Longitude of natural origin”,0,
ANGLEUNIT[“degree”,0.0174532925199433]],
•	PARAMETER[“Scale factor at natural origin”, 0.857385503731176,
SCALEUNIT[“unity”,1.0]],
•	PARAMETER[“False easting”,0,LENGTHUNIT[“metre”,1.0]],
•	PARAMETER[“False northing”,0,LENGTHUNIT[“metre”,1.0]],

	A6.5 The constant   was found by computing:  

A7. Tiled transverse Mercator, again

This section re-states the forward mapping equations for tiled transverse Mercator, for the same reasons given in the introduction to Section A6 for re-stating tiled Mercator.

	A7.1 The forward mapping equations are:

 
 
 
 
	where 
 ,
n is the zoom level,
  and   are defined in Section 3.2 of NGA.SIG.0012_2.0.0_UTMUPS.
	
	A7.2 The EPSG operation-method-code for this is EPSG::9807 with these parameters:

•	  is the above  
•	 
•	 (central meridian) is a longitude whose degree value is an odd integer divisible by 3.
•	FE 
•	FN 
	
	A7.3 The Well-Known-Text formats for the above EPSG parameters are found in NGA.IP.xxxx_x.x, National System for Geospatial Intelligence (NSG) GeoPackage Encoding Standard 1.0 Implementation Interoperability Standard (DRAFT), and are not repeated here.

	A7.4 The constant   was found by computing  .


A8. Tiled polar stereographic, again

This section re-states the forward mapping equations for tiled polar stereographic for the same reasons given in the introduction to Section A6 for re-stating tiled Mercator.

	A8.1 The forward mapping equations are:

	For the NORTH polar stereographic projection, 
 
 
	For the SOUTH polar stereographic projection, 
 
 

	For the both NORTH and SOUTH polar stereographic projections, 
 
 
	where 
		 
n is the zoom level,
  and   are defined in Section 8.1 of NGA.SIG.0012_2.0.0_UTMUPS.
	
	A8.2 The EPSG operation-method-code for this is EPSG::9810 with these parameters:

•	  is the above  
•	 , i.e. the radian equivalent of ±90°
•	 (central meridian) is a longitude whose degree value is a multiple of 90.
•	FE 
•	FN 
	
	A8.3 The Well-Known-Text formats for the above EPSG parameters are found in NGA.IP.xxxx_x.x, National System for Geospatial Intelligence (NSG) GeoPackage Encoding Standard 1.0 Implementation Interoperability Standard (DRAFT), and are not repeated here.

	A8.4 The constant   was found by computing  , where   is a defined constant (in radians) equivalent to 59°, and f3 refers to the function defined in section 8.1 of NGA.SIG.0012_2.0.0_UTMUPS.





 
Table 2: Tiled Mercator zoom-levels scale sets

n	0°	1°	2°	3°	4°	5°	6°	7°	8°	9°
0	156543	156519	156448	156330	156164	155951	155691	155384	155030	154628
1	78271.5	78259.7	78224.2	78165.0	78082.1	77975.7	77845.6	77692.0	77514.8	77314.2
2	39135.8	39129.8	39112.1	39082.5	39041.1	38987.8	38922.8	38846.0	38757.4	38657.1
3	19567.9	19564.9	19556.0	19541.2	19520.5	19493.9	19461.4	19423.0	19378.7	19328.5
4	9783.94	9782.46	9778.02	9770.62	9760.27	9746.96	9730.70	9711.49	9689.35	9664.27
5	4891.97	4891.23	4889.01	4885.31	4880.13	4873.48	4865.35	4855.75	4844.68	4832.14
6	2445.98	2445.61	2444.50	2442.66	2440.07	2436.74	2432.67	2427.87	2422.34	2416.07
7	1222.99	1222.81	1222.25	1221.33	1220.03	1218.37	1216.34	1213.94	1211.17	1208.03
8	611.496	611.404	611.126	610.664	610.017	609.185	608.169	606.968	605.584	604.017
9	305.748	305.702	305.563	305.332	305.008	304.592	304.084	303.484	302.792	302.009
10	152.874	152.851	152.782	152.666	152.504	152.296	152.042	151.742	151.396	151.004
11	76.4370	76.4255	76.3908	76.3330	76.2521	76.1481	76.0211	75.8711	75.6981	75.5021
12	38.2185	38.2127	38.1954	38.1665	38.1260	38.0740	38.0105	37.9355	37.8490	37.7511
13	19.1093	19.1064	19.0977	19.0832	19.0630	19.0370	19.0053	18.9678	18.9245	18.8755
14	9.55463	9.55318	9.54885	9.54162	9.53151	9.51851	9.50263	9.48388	9.46226	9.43777
15	4.77731	4.77659	4.77442	4.77081	4.76575	4.75926	4.75132	4.74194	4.73113	4.71888
16	2.38866	2.38830	2.38721	2.38541	2.38288	2.37963	2.37566	2.37097	2.36556	2.35944
17	1.19433	1.19415	1.19361	1.19270	1.19144	1.18981	1.18783	1.18549	1.18278	1.17972
18	0.597164	0.597074	0.596803	0.596351	0.595719	0.594907	0.593915	0.592743	0.591391	0.589861
19	0.298582	0.298537	0.298401	0.298176	0.297860	0.297454	0.296957	0.296371	0.295696	0.294930
20	0.149291	0.149268	0.149201	0.149088	0.148930	0.148727	0.148479	0.148186	0.147848	0.147465
21	0.0746455	0.0746342	0.0746004	0.0745439	0.0744649	0.0743634	0.0742393	0.0740928	0.0739239	0.0737326
22	0.0373228	0.0373171	0.0373002	0.0372720	0.0372325	0.0371817	0.0371197	0.0370464	0.0369619	0.0368663
23	0.0186614	0.0186586	0.0186501	0.0186360	0.0186162	0.0185908	0.0185598	0.0185232	0.0184810	0.0184331
24	0.00933069	0.00932928	0.00932505	0.00931799	0.00930811	0.00929542	0.00927992	0.00926160	0.00924049	0.00921657
										
n	10°	11°	12°	13°	14°	15°	16°	17°	18°	19°
0	154180	153686	153144	152557	151923	151243	150517	149746	148929	148067
1	77090.2	76842.8	76572.2	76278.3	75961.4	75621.4	75258.6	74872.8	74464.4	74033.4
2	38545.1	38421.4	38286.1	38139.2	37980.7	37810.7	37629.3	37436.4	37232.2	37016.7
3	19272.5	19210.7	19143.0	19069.6	18990.4	18905.4	18814.6	18718.2	18616.1	18508.4
4	9636.27	9605.35	9571.52	9534.79	9495.18	9452.68	9407.32	9359.11	9308.06	9254.18
5	4818.14	4802.68	4785.76	4767.40	4747.59	4726.34	4703.66	4679.55	4654.03	4627.09
6	2409.07	2401.34	2392.88	2383.70	2373.79	2363.17	2351.83	2339.78	2327.01	2313.55
7	1204.53	1200.67	1196.44	1191.85	1186.90	1181.58	1175.91	1169.89	1163.51	1156.77
8	602.267	600.334	598.220	595.925	593.448	590.792	587.957	584.944	581.753	578.386
9	301.134	300.167	299.110	297.962	296.724	295.396	293.979	292.472	290.877	289.193
10	150.567	150.084	149.555	148.981	148.362	147.698	146.989	146.236	145.438	144.597
11	75.2834	75.0418	74.7775	74.4906	74.1811	73.8491	73.4947	73.1180	72.7192	72.2983
12	37.6417	37.5209	37.3888	37.2453	37.0905	36.9245	36.7473	36.5590	36.3596	36.1491
13	18.8208	18.7605	18.6944	18.6226	18.5453	18.4623	18.3737	18.2795	18.1798	18.0746
14	9.41042	9.38023	9.34719	9.31132	9.27263	9.23113	9.18683	9.13975	9.08990	9.03729
15	4.70521	4.69011	4.67359	4.65566	4.63632	4.61557	4.59342	4.56988	4.54495	4.51864
16	2.35261	2.34506	2.33680	2.32783	2.31816	2.30778	2.29671	2.28494	2.27247	2.25932
17	1.17630	1.17253	1.16840	1.16392	1.15908	1.15389	1.14835	1.14247	1.13624	1.12966
18	0.588151	0.586264	0.584199	0.581958	0.579539	0.576946	0.574177	0.571235	0.568119	0.564830
19	0.294076	0.293132	0.292100	0.290979	0.289770	0.288473	0.287089	0.285617	0.284059	0.282415
20	0.147038	0.146566	0.146050	0.145489	0.144885	0.144236	0.143544	0.142809	0.142030	0.141208
21	0.0735189	0.0732830	0.0730249	0.0727447	0.0724424	0.0721182	0.0717721	0.0714043	0.0710148	0.0706038
22	0.0367595	0.0366415	0.0365125	0.0363723	0.0362212	0.0360591	0.0358861	0.0357022	0.0355074	0.0353019
23	0.0183797	0.0183208	0.0182562	0.0181862	0.0181106	0.0180296	0.0179430	0.0178511	0.0177537	0.0176509
24	0.00918987	0.00916038	0.00912811	0.00909309	0.00905530	0.00901478	0.00897152	0.00892554	0.00887685	0.00882547
Table 2: Tiled Mercator zoom-levels scale sets

n	20°	21°	22°	23°	24°	25°	26°	27°	28°	29°
0	147160	146208	145212	144172	143088	141961	140791	139577	138321	137023
1	73580.0	73104.2	72606.2	72086.2	71544.2	70980.5	70395.3	69788.6	69160.7	68511.7
2	36790.0	36552.1	36303.1	36043.1	35772.1	35490.3	35197.6	34894.3	34580.3	34255.9
3	18395.0	18276.0	18151.5	18021.5	17886.1	17745.1	17598.8	17447.1	17290.2	17127.9
4	9197.50	9138.02	9075.77	9010.77	8943.03	8872.57	8799.41	8723.57	8645.09	8563.97
5	4598.75	4569.01	4537.89	4505.38	4471.51	4436.28	4399.70	4361.79	4322.54	4281.98
6	2299.37	2284.51	2268.94	2252.69	2235.76	2218.14	2199.85	2180.89	2161.27	2140.99
7	1149.69	1142.25	1134.47	1126.35	1117.88	1109.07	1099.93	1090.45	1080.64	1070.50
8	574.844	571.126	567.236	563.173	558.939	554.535	549.963	545.223	540.318	535.248
9	287.422	285.563	283.618	281.587	279.470	277.268	274.982	272.612	270.159	267.624
10	143.711	142.782	141.809	140.793	139.735	138.634	137.491	136.306	135.079	133.812
11	71.8555	71.3908	70.9045	70.3966	69.8674	69.3169	68.7454	68.1529	67.5397	66.9060
12	35.9277	35.6954	35.4522	35.1983	34.9337	34.6585	34.3727	34.0765	33.7699	33.4530
13	17.9639	17.8477	17.7261	17.5992	17.4668	17.3292	17.1863	17.0382	16.8849	16.7265
14	8.98193	8.92385	8.86306	8.79958	8.73342	8.66462	8.59317	8.51912	8.44247	8.36325
15	4.49097	4.46193	4.43153	4.39979	4.36671	4.33231	4.29659	4.25956	4.22123	4.18162
16	2.24548	2.23096	2.21577	2.19989	2.18336	2.16615	2.14829	2.12978	2.11062	2.09081
17	1.12274	1.11548	1.10788	1.09995	1.09168	1.08308	1.07415	1.06489	1.05531	1.04541
18	0.561371	0.557741	0.553941	0.549974	0.545839	0.541538	0.537073	0.532445	0.527654	0.522703
19	0.280685	0.278870	0.276971	0.274987	0.272920	0.270769	0.268537	0.266222	0.263827	0.261352
20	0.140343	0.139435	0.138485	0.137493	0.136460	0.135385	0.134268	0.133111	0.131914	0.130676
21	0.0701713	0.0697176	0.0692427	0.0687467	0.0682299	0.0676923	0.0671342	0.0665556	0.0659568	0.0653379
22	0.0350857	0.0348588	0.0346213	0.0343734	0.0341149	0.0338462	0.0335671	0.0332778	0.0329784	0.0326689
23	0.0175428	0.0174294	0.0173107	0.0171867	0.0170575	0.0169231	0.0167835	0.0166389	0.0164892	0.0163345
24	0.00877142	0.00871470	0.00865533	0.00859334	0.00852874	0.00846154	0.00839177	0.00831945	0.00824460	0.00816723
										
n	30°	31°	32°	33°	34°	35°	36°	37°	38°	39°
0	135684	134303	132881	131419	129916	128374	126793	125173	123514	121818
1	67841.9	67151.4	66440.5	65709.3	64958.1	64187.0	63396.3	62586.3	61757.2	60909.2
2	33921.0	33575.7	33220.2	32854.6	32479.0	32093.5	31698.2	31293.2	30878.6	30454.6
3	16960.5	16787.9	16610.1	16427.3	16239.5	16046.7	15849.1	15646.6	15439.3	15227.3
4	8480.24	8393.93	8305.06	8213.66	8119.76	8023.37	7924.54	7823.29	7719.65	7613.65
5	4240.12	4196.96	4152.53	4106.83	4059.88	4011.69	3962.27	3911.65	3859.82	3806.82
6	2120.06	2098.48	2076.27	2053.42	2029.94	2005.84	1981.14	1955.82	1929.91	1903.41
7	1060.03	1049.24	1038.13	1026.71	1014.97	1002.92	990.568	977.911	964.956	951.706
8	530.015	524.621	519.066	513.354	507.485	501.461	495.284	488.956	482.478	475.853
9	265.007	262.310	259.533	256.677	253.742	250.730	247.642	244.478	241.239	237.927
10	132.504	131.155	129.767	128.338	126.871	125.365	123.821	122.239	120.620	118.963
11	66.2519	65.5776	64.8833	64.1692	63.4356	62.6826	61.9105	61.1195	60.3098	59.4816
12	33.1259	32.7888	32.4416	32.0846	31.7178	31.3413	30.9552	30.5597	30.1549	29.7408
13	16.5630	16.3944	16.2208	16.0423	15.8589	15.6707	15.4776	15.2799	15.0774	14.8704
14	8.28148	8.19720	8.11041	8.02115	7.92945	7.83533	7.73881	7.63993	7.53872	7.43520
15	4.14074	4.09860	4.05521	4.01058	3.96472	3.91766	3.86941	3.81997	3.76936	3.71760
16	2.07037	2.04930	2.02760	2.00529	1.98236	1.95883	1.93470	1.90998	1.88468	1.85880
17	1.03519	1.02465	1.01380	1.00264	0.991181	0.979416	0.967351	0.954992	0.942340	0.929400
18	0.517593	0.512325	0.506901	0.501322	0.495591	0.489708	0.483676	0.477496	0.471170	0.464700
19	0.258796	0.256162	0.253450	0.250661	0.247795	0.244854	0.241838	0.238748	0.235585	0.232350
20	0.129398	0.128081	0.126725	0.125331	0.123898	0.122427	0.120919	0.119374	0.117793	0.116175
21	0.0646991	0.0640406	0.0633626	0.0626653	0.0619488	0.0612135	0.0604595	0.0596870	0.0588963	0.0580875
22	0.0323495	0.0320203	0.0316813	0.0313326	0.0309744	0.0306067	0.0302297	0.0298435	0.0294481	0.0290438
23	0.0161748	0.0160101	0.0158406	0.0156663	0.0154872	0.0153034	0.0151149	0.0149217	0.0147241	0.0145219
24	0.00808739	0.00800507	0.00792032	0.00783316	0.00774360	0.00765169	0.00755743	0.00746087	0.00736203	0.00726094
Table 2: Tiled Mercator zoom-levels scale sets

n	40°	41°	42°	43°	44°	45°	46°	47°	48°	49°
0	120085	118315	116509	114667	112790	110878	108933	106954	104942	102898
1	60042.6	59157.6	58254.4	57333.5	56395.0	55439.2	54466.4	53476.9	52471.0	51448.9
2	30021.3	29578.8	29127.2	28666.7	28197.5	27719.6	27233.2	26738.4	26235.5	25724.5
3	15010.6	14789.4	14563.6	14333.4	14098.7	13859.8	13616.6	13369.2	13117.7	12862.2
4	7505.32	7394.69	7281.81	7166.69	7049.37	6929.90	6808.30	6684.61	6558.87	6431.11
5	3752.66	3697.35	3640.90	3583.34	3524.69	3464.95	3404.15	3342.30	3279.43	3215.56
6	1876.33	1848.67	1820.45	1791.67	1762.34	1732.47	1702.07	1671.15	1639.72	1607.78
7	938.165	924.337	910.226	895.836	881.172	866.237	851.037	835.576	819.859	803.889
8	469.082	462.168	455.113	447.918	440.586	433.119	425.519	417.788	409.929	401.945
9	234.541	231.084	227.556	223.959	220.293	216.559	212.759	208.894	204.965	200.972
10	117.271	115.542	113.778	111.979	110.146	108.280	106.380	104.447	102.482	100.486
11	58.6353	57.7710	56.8891	55.9897	55.0732	54.1398	53.1898	52.2235	51.2412	50.2431
12	29.3177	28.8855	28.4446	27.9949	27.5366	27.0699	26.5949	26.1118	25.6206	25.1215
13	14.6588	14.4428	14.2223	13.9974	13.7683	13.5350	13.2975	13.0559	12.8103	12.5608
14	7.32941	7.22138	7.11114	6.99872	6.88415	6.76748	6.64873	6.52794	6.40515	6.28039
15	3.66471	3.61069	3.55557	3.49936	3.44208	3.38374	3.32436	3.26397	3.20257	3.14019
16	1.83235	1.80535	1.77778	1.74968	1.72104	1.69187	1.66218	1.63198	1.60129	1.57010
17	0.916177	0.902673	0.888892	0.874840	0.860519	0.845935	0.831091	0.815992	0.800643	0.785048
18	0.458088	0.451336	0.444446	0.437420	0.430260	0.422967	0.415546	0.407996	0.400322	0.392524
19	0.229044	0.225668	0.222223	0.218710	0.215130	0.211484	0.207773	0.203998	0.200161	0.196262
20	0.114522	0.112834	0.111112	0.109355	0.107565	0.105742	0.103886	0.101999	0.100080	0.0981310
21	0.0572610	0.0564170	0.0555558	0.0546775	0.0537824	0.0528709	0.0519432	0.0509995	0.0500402	0.0490655
22	0.0286305	0.0282085	0.0277779	0.0273387	0.0268912	0.0264355	0.0259716	0.0254998	0.0250201	0.0245328
23	0.0143153	0.0141043	0.0138889	0.0136694	0.0134456	0.0132177	0.0129858	0.0127499	0.0125100	0.0122664
24	0.00715763	0.00705213	0.00694447	0.00683468	0.00672281	0.00660887	0.00649290	0.00637494	0.00625502	0.00613319
										
n	50°	51°	52°	53°	54°	55°	56°	57°	58°	59°
0	100822	98715.5	96578.5	94411.7	92215.9	89991.7	87739.8	85460.9	83155.6	80824.6
1	50411.1	49357.7	48289.2	47205.9	46108.0	44995.9	43869.9	42730.4	41577.8	40412.3
2	25205.5	24678.9	24144.6	23602.9	23054.0	22497.9	21935.0	21365.2	20788.9	20206.2
3	12602.8	12339.4	12072.3	11801.5	11527.0	11249.0	10967.5	10682.6	10394.4	10103.1
4	6301.38	6169.72	6036.15	5900.73	5763.50	5624.48	5483.74	5341.31	5197.22	5051.54
5	3150.69	3084.86	3018.08	2950.37	2881.75	2812.24	2741.87	2670.65	2598.61	2525.77
6	1575.35	1542.43	1509.04	1475.18	1440.87	1406.12	1370.93	1335.33	1299.31	1262.88
7	787.673	771.215	754.519	737.592	720.437	703.061	685.467	667.663	649.653	631.442
8	393.837	385.607	377.260	368.796	360.218	351.530	342.734	333.832	324.827	315.721
9	196.918	192.804	188.630	184.398	180.109	175.765	171.367	166.916	162.413	157.861
10	98.4591	96.4018	94.3149	92.1990	90.0546	87.8826	85.6834	83.4579	81.2066	78.9303
11	49.2296	48.2009	47.1575	46.0995	45.0273	43.9413	42.8417	41.7289	40.6033	39.4652
12	24.6148	24.1005	23.5787	23.0497	22.5137	21.9706	21.4209	20.8645	20.3017	19.7326
13	12.3074	12.0502	11.7894	11.5249	11.2568	10.9853	10.7104	10.4322	10.1508	9.86629
14	6.15370	6.02512	5.89468	5.76243	5.62841	5.49266	5.35521	5.21612	5.07541	4.93314
15	3.07685	3.01256	2.94734	2.88122	2.81421	2.74633	2.67761	2.60806	2.53771	2.46657
16	1.53842	1.50628	1.47367	1.44061	1.40710	1.37317	1.33880	1.30403	1.26885	1.23329
17	0.769212	0.753139	0.736835	0.720304	0.703552	0.686583	0.669402	0.652015	0.634427	0.616643
18	0.384606	0.376570	0.368418	0.360152	0.351776	0.343291	0.334701	0.326007	0.317213	0.308322
19	0.192303	0.188285	0.184209	0.180076	0.175888	0.171646	0.167350	0.163004	0.158607	0.154161
20	0.0961515	0.0941424	0.0921044	0.0900380	0.0879440	0.0858228	0.0836752	0.0815019	0.0793033	0.0770804
21	0.0480757	0.0470712	0.0460522	0.0450190	0.0439720	0.0429114	0.0418376	0.0407509	0.0396517	0.0385402
22	0.0240379	0.0235356	0.0230261	0.0225095	0.0219860	0.0214557	0.0209188	0.0203755	0.0198258	0.0192701
23	0.0120189	0.0117678	0.0115130	0.0112548	0.0109930	0.0107279	0.0104594	0.0101877	0.00991292	0.00963505
24	0.00600947	0.00588390	0.00575652	0.00562738	0.00549650	0.00536393	0.00522970	0.00509387	0.00495646	0.00481752
Table 2: Tiled Mercator zoom-levels scale sets

n	60°	61°	62°	63°	64°	65°	66°	67°	68°	69°
0	78468.8	76088.6	73685.0	71258.7	68810.3	66340.6	63850.4	61340.5	58811.5	56264.4
1	39234.4	38044.3	36842.5	35629.3	34405.1	33170.3	31925.2	30670.2	29405.8	28132.2
2	19617.2	19022.2	18421.3	17814.7	17202.6	16585.1	15962.6	15335.1	14702.9	14066.1
3	9808.59	9511.08	9210.63	8907.33	8601.28	8292.57	7981.30	7667.56	7351.44	7033.05
4	4904.30	4755.54	4605.31	4453.67	4300.64	4146.29	3990.65	3833.78	3675.72	3516.52
5	2452.15	2377.77	2302.66	2226.83	2150.32	2073.14	1995.33	1916.89	1837.86	1758.26
6	1226.07	1188.89	1151.33	1113.42	1075.16	1036.57	997.663	958.445	918.930	879.131
7	613.037	594.443	575.664	556.708	537.580	518.286	498.831	479.222	459.465	439.566
8	306.519	297.221	287.832	278.354	268.790	259.143	249.416	239.611	229.733	219.783
9	153.259	148.611	143.916	139.177	134.395	129.571	124.708	119.806	114.866	109.891
10	76.6296	74.3053	71.9580	69.5885	67.1975	64.7857	62.3539	59.9028	57.4331	54.9457
11	38.3148	37.1527	35.9790	34.7943	33.5988	32.3929	31.1770	29.9514	28.7166	27.4728
12	19.1574	18.5763	17.9895	17.3971	16.7994	16.1964	15.5885	14.9757	14.3583	13.7364
13	9.57871	9.28816	8.99475	8.69857	8.39969	8.09822	7.79424	7.48785	7.17914	6.86821
14	4.78935	4.64408	4.49738	4.34928	4.19985	4.04911	3.89712	3.74392	3.58957	3.43411
15	2.39468	2.32204	2.24869	2.17464	2.09992	2.02455	1.94856	1.87196	1.79479	1.71705
16	1.19734	1.16102	1.12434	1.08732	1.04996	1.01228	0.974280	0.935981	0.897393	0.858526
17	0.598669	0.580510	0.562172	0.543660	0.524981	0.506139	0.487140	0.467991	0.448696	0.429263
18	0.299335	0.290255	0.281086	0.271830	0.262490	0.253069	0.243570	0.233995	0.224348	0.214632
19	0.149667	0.145128	0.140543	0.135915	0.131245	0.126535	0.121785	0.116998	0.112174	0.107316
20	0.0748336	0.0725638	0.0702715	0.0679576	0.0656226	0.0632673	0.0608925	0.0584988	0.0560870	0.0536579
21	0.0374168	0.0362819	0.0351358	0.0339788	0.0328113	0.0316337	0.0304462	0.0292494	0.0280435	0.0268290
22	0.0187084	0.0181409	0.0175679	0.0169894	0.0164056	0.0158168	0.0152231	0.0146247	0.0140218	0.0134145
23	0.00935420	0.00907047	0.00878394	0.00849469	0.00820282	0.00790841	0.00761156	0.00731235	0.00701088	0.00670724
24	0.00467710	0.00453524	0.00439197	0.00424735	0.00410141	0.00395421	0.00380578	0.00365618	0.00350544	0.00335362
										
n	70°	71°	72°	73°	74°	75°	76°	77°	78°	79°
0	53699.8	51118.6	48521.6	45909.5	43283.2	40643.4	37991.1	35327.0	32651.9	29966.6
1	26849.9	25559.3	24260.8	22954.8	21641.6	20321.7	18995.5	17663.5	16325.9	14983.3
2	13425.0	12779.7	12130.4	11477.4	10820.8	10160.9	9497.77	8831.74	8162.97	7491.66
3	6712.48	6389.83	6065.20	5738.69	5410.40	5080.43	4748.89	4415.87	4081.48	3745.83
4	3356.24	3194.91	3032.60	2869.34	2705.20	2540.22	2374.44	2207.94	2040.74	1872.91
5	1678.12	1597.46	1516.30	1434.67	1352.60	1270.11	1187.22	1103.97	1020.37	936.457
6	839.060	798.728	758.150	717.336	676.300	635.054	593.611	551.984	510.185	468.229
7	419.530	399.364	379.075	358.668	338.150	317.527	296.805	275.992	255.093	234.114
8	209.765	199.682	189.537	179.334	169.075	158.763	148.403	137.996	127.546	117.057
9	104.882	99.8411	94.7687	89.6670	84.5375	79.3817	74.2014	68.9980	63.7732	58.5286
10	52.4412	49.9205	47.3844	44.8335	42.2687	39.6909	37.1007	34.4990	31.8866	29.2643
11	26.2206	24.9603	23.6922	22.4167	21.1344	19.8454	18.5503	17.2495	15.9433	14.6321
12	13.1103	12.4801	11.8461	11.2084	10.5672	9.92272	9.27517	8.62475	7.97165	7.31607
13	6.55515	6.24007	5.92304	5.60419	5.28359	4.96136	4.63759	4.31237	3.98582	3.65804
14	3.27758	3.12003	2.96152	2.80209	2.64180	2.48068	2.31879	2.15619	1.99291	1.82902
15	1.63879	1.56002	1.48076	1.40105	1.32090	1.24034	1.15940	1.07809	0.996456	0.914509
16	0.819394	0.780008	0.740381	0.700523	0.660449	0.620170	0.579698	0.539047	0.498228	0.457254
17	0.409697	0.390004	0.370190	0.350262	0.330224	0.310085	0.289849	0.269523	0.249114	0.228627
18	0.204849	0.195002	0.185095	0.175131	0.165112	0.155042	0.144925	0.134762	0.124557	0.114314
19	0.102424	0.0975010	0.0925476	0.0875654	0.0825561	0.0775212	0.0724623	0.0673808	0.0622785	0.0571568
20	0.0512121	0.0487505	0.0462738	0.0437827	0.0412781	0.0387606	0.0362311	0.0336904	0.0311392	0.0285784
21	0.0256061	0.0243753	0.0231369	0.0218914	0.0206390	0.0193803	0.0181156	0.0168452	0.0155696	0.0142892
22	0.0128030	0.0121876	0.0115684	0.0109457	0.0103195	0.00969015	0.00905778	0.00842260	0.00778481	0.00714460
23	0.00640152	0.00609381	0.00578422	0.00547284	0.00515976	0.00484508	0.00452889	0.00421130	0.00389241	0.00357230
24	0.00320076	0.00304691	0.00289211	0.00273642	0.00257988	0.00242254	0.00226445	0.00210565	0.00194620	0.00178615
Table 2: Tiled Mercator zoom-levels scale sets

n	80°	81°	82°	83°	84°	85°				
0	27272.1	24569.1	21858.4	19141.0	16417.6	13689.2				
1	13636.0	12284.5	10929.2	9570.51	8208.82	6844.59				
2	6818.02	6142.27	5464.61	4785.25	4104.41	3422.29				
3	3409.01	3071.14	2732.31	2392.63	2052.21	1711.15				
4	1704.51	1535.57	1366.15	1196.31	1026.10	855.573				
5	852.253	767.784	683.076	598.157	513.051	427.787				
6	426.126	383.892	341.538	299.078	256.526	213.893				
7	213.063	191.946	170.769	149.539	128.263	106.947				
8	106.532	95.9730	85.3846	74.7696	64.1314	53.4733				
9	53.2658	47.9865	42.6923	37.3848	32.0657	26.7367				
10	26.6329	23.9932	21.3461	18.6924	16.0329	13.3683				
11	13.3164	11.9966	10.6731	9.34620	8.01643	6.68417				
12	6.65822	5.99831	5.33653	4.67310	4.00821	3.34208				
13	3.32911	2.99916	2.66827	2.33655	2.00411	1.67104				
14	1.66456	1.49958	1.33413	1.16828	1.00205	0.835521				
15	0.832278	0.749789	0.667067	0.584138	0.501027	0.417760				
16	0.416139	0.374894	0.333533	0.292069	0.250513	0.208880				
17	0.208070	0.187447	0.166767	0.146034	0.125257	0.104440				
18	0.104035	0.0937236	0.0833833	0.0730172	0.0626283	0.0522200				
19	0.0520174	0.0468618	0.0416917	0.0365086	0.0313142	0.0261100				
20	0.0260087	0.0234309	0.0208458	0.0182543	0.0156571	0.0130550				
21	0.0130043	0.0117155	0.0104229	0.00912715	0.00782854	0.00652751				
22	0.00650217	0.00585773	0.00521146	0.00456357	0.00391427	0.00326375				
23	0.00325109	0.00292886	0.00260573	0.00228179	0.00195714	0.00163188				
24	0.00162554	0.00146443	0.00130286	0.00114089	0.000978568	0.000815938				

 
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	156281	156281	156281	156281	156281	156281	156281	156281	156281
1	78140.4	78140.4	78140.4	78140.4	78140.4	78140.4	78140.4	78140.4	78140.4
2	39070.2	39070.2	39070.2	39070.2	39070.2	39070.2	39070.2	39070.2	39070.2
3	19535.1	19535.1	19535.1	19535.1	19535.1	19535.1	19535.1	19535.1	19535.1
4	9767.54	9767.54	9767.54	9767.54	9767.54	9767.54	9767.54	9767.54	9767.54
5	4883.77	4883.77	4883.77	4883.77	4883.77	4883.77	4883.77	4883.77	4883.77
6	2441.89	2441.89	2441.89	2441.89	2441.89	2441.89	2441.89	2441.89	2441.89
7	1220.94	1220.94	1220.94	1220.94	1220.94	1220.94	1220.94	1220.94	1220.94
8	610.472	610.472	610.472	610.472	610.472	610.472	610.472	610.472	610.472
9	305.236	305.236	305.236	305.236	305.236	305.236	305.236	305.236	305.236
10	152.618	152.618	152.618	152.618	152.618	152.618	152.618	152.618	152.618
11	76.3089	76.3089	76.3089	76.3089	76.3089	76.3089	76.3089	76.3089	76.3089
12	38.1545	38.1545	38.1545	38.1545	38.1545	38.1545	38.1545	38.1545	38.1545
13	19.0772	19.0772	19.0772	19.0772	19.0772	19.0772	19.0772	19.0772	19.0772
14	9.53862	9.53862	9.53862	9.53862	9.53862	9.53862	9.53862	9.53862	9.53862
15	4.76931	4.76931	4.76931	4.76931	4.76931	4.76931	4.76931	4.76931	4.76931
16	2.38465	2.38465	2.38465	2.38465	2.38465	2.38465	2.38465	2.38465	2.38465
17	1.19233	1.19233	1.19233	1.19233	1.19233	1.19233	1.19233	1.19233	1.19233
18	0.596164	0.596164	0.596164	0.596164	0.596164	0.596164	0.596164	0.596164	0.596164
19	0.298082	0.298082	0.298082	0.298082	0.298082	0.298082	0.298082	0.298082	0.298082
20	0.149041	0.149041	0.149041	0.149041	0.149041	0.149041	0.149041	0.149041	0.149041
21	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205
22	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602
23	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301
24	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506
Longitude = Central Meridian
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	156281	156281	156281	156281	156281	156281	156281	156281	156281
1	78140.4	78140.4	78140.4	78140.4	78140.4	78140.4	78140.4	78140.4	78140.4
2	39070.2	39070.2	39070.2	39070.2	39070.2	39070.2	39070.2	39070.2	39070.2
3	19535.1	19535.1	19535.1	19535.1	19535.1	19535.1	19535.1	19535.1	19535.1
4	9767.54	9767.54	9767.54	9767.54	9767.54	9767.54	9767.54	9767.54	9767.54
5	4883.77	4883.77	4883.77	4883.77	4883.77	4883.77	4883.77	4883.77	4883.77
6	2441.89	2441.89	2441.89	2441.89	2441.89	2441.89	2441.89	2441.89	2441.89
7	1220.94	1220.94	1220.94	1220.94	1220.94	1220.94	1220.94	1220.94	1220.94
8	610.472	610.472	610.472	610.472	610.472	610.472	610.472	610.472	610.472
9	305.236	305.236	305.236	305.236	305.236	305.236	305.236	305.236	305.236
10	152.618	152.618	152.618	152.618	152.618	152.618	152.618	152.618	152.618
11	76.3089	76.3089	76.3089	76.3089	76.3089	76.3089	76.3089	76.3089	76.3089
12	38.1545	38.1545	38.1545	38.1545	38.1545	38.1545	38.1545	38.1545	38.1545
13	19.0772	19.0772	19.0772	19.0772	19.0772	19.0772	19.0772	19.0772	19.0772
14	9.53862	9.53862	9.53862	9.53862	9.53862	9.53862	9.53862	9.53862	9.53862
15	4.76931	4.76931	4.76931	4.76931	4.76931	4.76931	4.76931	4.76931	4.76931
16	2.38465	2.38465	2.38465	2.38465	2.38465	2.38465	2.38465	2.38465	2.38465
17	1.19233	1.19233	1.19233	1.19233	1.19233	1.19233	1.19233	1.19233	1.19233
18	0.596164	0.596164	0.596164	0.596164	0.596164	0.596164	0.596164	0.596164	0.596164
19	0.298082	0.298082	0.298082	0.298082	0.298082	0.298082	0.298082	0.298082	0.298082
20	0.149041	0.149041	0.149041	0.149041	0.149041	0.149041	0.149041	0.149041	0.149041
21	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205	0.0745205
22	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602	0.0372602
23	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301	0.0186301
24	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506	0.00931506
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 1°
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	156257	156257	156257	156258	156260	156261	156263	156265	156267
1	78128.4	78128.5	78128.7	78129.2	78129.8	78130.5	78131.4	78132.3	78133.3
2	39064.2	39064.2	39064.4	39064.6	39064.9	39065.3	39065.7	39066.2	39066.7
3	19532.1	19532.1	19532.2	19532.3	19532.4	19532.6	19532.8	19533.1	19533.3
4	9766.05	9766.06	9766.09	9766.15	9766.22	9766.32	9766.42	9766.54	9766.67
5	4883.02	4883.03	4883.05	4883.07	4883.11	4883.16	4883.21	4883.27	4883.33
6	2441.51	2441.51	2441.52	2441.54	2441.56	2441.58	2441.61	2441.64	2441.67
7	1220.76	1220.76	1220.76	1220.77	1220.78	1220.79	1220.80	1220.82	1220.83
8	610.378	610.379	610.381	610.384	610.389	610.395	610.401	610.409	610.417
9	305.189	305.189	305.190	305.192	305.194	305.197	305.201	305.204	305.208
10	152.594	152.595	152.595	152.596	152.597	152.599	152.600	152.602	152.604
11	76.2972	76.2973	76.2976	76.2980	76.2986	76.2993	76.3002	76.3011	76.3021
12	38.1486	38.1487	38.1488	38.1490	38.1493	38.1497	38.1501	38.1506	38.1510
13	19.0743	19.0743	19.0744	19.0745	19.0747	19.0748	19.0750	19.0753	19.0755
14	9.53716	9.53717	9.53720	9.53725	9.53733	9.53742	9.53752	9.53764	9.53776
15	4.76858	4.76858	4.76860	4.76863	4.76866	4.76871	4.76876	4.76882	4.76888
16	2.38429	2.38429	2.38430	2.38431	2.38433	2.38435	2.38438	2.38441	2.38444
17	1.19214	1.19215	1.19215	1.19216	1.19217	1.19218	1.19219	1.19220	1.19222
18	0.596072	0.596073	0.596075	0.596078	0.596083	0.596089	0.596095	0.596102	0.596110
19	0.298036	0.298036	0.298037	0.298039	0.298041	0.298044	0.298048	0.298051	0.298055
20	0.149018	0.149018	0.149019	0.149020	0.149021	0.149022	0.149024	0.149026	0.149028
21	0.0745090	0.0745091	0.0745094	0.0745098	0.0745104	0.0745111	0.0745119	0.0745128	0.0745138
22	0.0372545	0.0372546	0.0372547	0.0372549	0.0372552	0.0372555	0.0372559	0.0372564	0.0372569
23	0.0186273	0.0186273	0.0186273	0.0186274	0.0186276	0.0186278	0.0186280	0.0186282	0.0186284
24	0.00931363	0.00931364	0.00931367	0.00931372	0.00931380	0.00931388	0.00931399	0.00931410	0.00931422
Longitude = Central Meridian + 1°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	156269	156271	156273	156275	156276	156278	156279	156280	156281
1	78134.4	78135.4	78136.4	78137.4	78138.2	78139.0	78139.6	78140.0	78140.3
2	39067.2	39067.7	39068.2	39068.7	39069.1	39069.5	39069.8	39070.0	39070.1
3	19533.6	19533.9	19534.1	19534.3	19534.6	19534.7	19534.9	19535.0	19535.1
4	9766.80	9766.93	9767.05	9767.17	9767.28	9767.37	9767.44	9767.50	9767.53
5	4883.40	4883.46	4883.53	4883.59	4883.64	4883.69	4883.72	4883.75	4883.77
6	2441.70	2441.73	2441.76	2441.79	2441.82	2441.84	2441.86	2441.87	2441.88
7	1220.85	1220.87	1220.88	1220.90	1220.91	1220.92	1220.93	1220.94	1220.94
8	610.425	610.433	610.441	610.448	610.455	610.461	610.465	610.469	610.471
9	305.212	305.217	305.220	305.224	305.227	305.230	305.233	305.234	305.235
10	152.606	152.608	152.610	152.612	152.614	152.615	152.616	152.617	152.618
11	76.3031	76.3041	76.3051	76.3060	76.3069	76.3076	76.3082	76.3086	76.3089
12	38.1516	38.1521	38.1526	38.1530	38.1534	38.1538	38.1541	38.1543	38.1544
13	19.0758	19.0760	19.0763	19.0765	19.0767	19.0769	19.0770	19.0771	19.0772
14	9.53789	9.53802	9.53814	9.53825	9.53836	9.53845	9.53852	9.53857	9.53861
15	4.76894	4.76901	4.76907	4.76913	4.76918	4.76922	4.76926	4.76929	4.76930
16	2.38447	2.38450	2.38453	2.38456	2.38459	2.38461	2.38463	2.38464	2.38465
17	1.19224	1.19225	1.19227	1.19228	1.19229	1.19231	1.19232	1.19232	1.19233
18	0.596118	0.596126	0.596134	0.596141	0.596147	0.596153	0.596158	0.596161	0.596163
19	0.298059	0.298063	0.298067	0.298070	0.298074	0.298076	0.298079	0.298080	0.298081
20	0.149030	0.149031	0.149033	0.149035	0.149037	0.149038	0.149039	0.149040	0.149041
21	0.0745148	0.0745157	0.0745167	0.0745176	0.0745184	0.0745191	0.0745197	0.0745201	0.0745204
22	0.0372574	0.0372579	0.0372584	0.0372588	0.0372592	0.0372596	0.0372598	0.0372601	0.0372602
23	0.0186287	0.0186289	0.0186292	0.0186294	0.0186296	0.0186298	0.0186299	0.0186300	0.0186301
24	0.00931434	0.00931447	0.00931459	0.00931470	0.00931480	0.00931489	0.00931496	0.00931501	0.00931505
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 2°
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	156185	156186	156188	156191	156196	156202	156209	156217	156225
1	78092.4	78092.8	78093.9	78095.7	78098.1	78101.0	78104.5	78108.3	78112.3
2	39046.2	39046.4	39046.9	39047.8	39049.0	39050.5	39052.2	39054.1	39056.2
3	19523.1	19523.2	19523.5	19523.9	19524.5	19525.3	19526.1	19527.1	19528.1
4	9761.55	9761.60	9761.74	9761.96	9762.26	9762.63	9763.06	9763.53	9764.04
5	4880.78	4880.80	4880.87	4880.98	4881.13	4881.32	4881.53	4881.77	4882.02
6	2440.39	2440.40	2440.43	2440.49	2440.56	2440.66	2440.76	2440.88	2441.01
7	1220.19	1220.20	1220.22	1220.24	1220.28	1220.33	1220.38	1220.44	1220.50
8	610.097	610.100	610.109	610.122	610.141	610.164	610.191	610.221	610.252
9	305.049	305.050	305.054	305.061	305.071	305.082	305.096	305.110	305.126
10	152.524	152.525	152.527	152.531	152.535	152.541	152.548	152.555	152.563
11	76.2621	76.2625	76.2636	76.2653	76.2677	76.2706	76.2739	76.2776	76.2816
12	38.1311	38.1313	38.1318	38.1326	38.1338	38.1353	38.1370	38.1388	38.1408
13	19.0655	19.0656	19.0659	19.0663	19.0669	19.0676	19.0685	19.0694	19.0704
14	9.53277	9.53281	9.53295	9.53316	9.53346	9.53382	9.53424	9.53470	9.53519
15	4.76638	4.76641	4.76647	4.76658	4.76673	4.76691	4.76712	4.76735	4.76760
16	2.38319	2.38320	2.38324	2.38329	2.38336	2.38345	2.38356	2.38368	2.38380
17	1.19160	1.19160	1.19162	1.19165	1.19168	1.19173	1.19178	1.19184	1.19190
18	0.595798	0.595801	0.595809	0.595823	0.595841	0.595864	0.595890	0.595919	0.595950
19	0.297899	0.297900	0.297905	0.297911	0.297921	0.297932	0.297945	0.297959	0.297975
20	0.148949	0.148950	0.148952	0.148956	0.148960	0.148966	0.148972	0.148980	0.148987
21	0.0744747	0.0744751	0.0744761	0.0744778	0.0744801	0.0744830	0.0744862	0.0744899	0.0744937
22	0.0372374	0.0372375	0.0372381	0.0372389	0.0372401	0.0372415	0.0372431	0.0372449	0.0372469
23	0.0186187	0.0186188	0.0186190	0.0186195	0.0186200	0.0186207	0.0186216	0.0186225	0.0186234
24	0.00930934	0.00930939	0.00930952	0.00930973	0.00931002	0.00931037	0.00931078	0.00931123	0.00931171
Longitude = Central Meridian + 2°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	156233	156241	156249	156257	156264	156270	156274	156278	156280
1	78116.5	78120.6	78124.7	78128.4	78131.8	78134.8	78137.2	78138.9	78140.0
2	39058.2	39060.3	39062.3	39064.2	39065.9	39067.4	39068.6	39069.5	39070.0
3	19529.1	19530.2	19531.2	19532.1	19533.0	19533.7	19534.3	19534.7	19535.0
4	9764.56	9765.08	9765.58	9766.05	9766.48	9766.85	9767.15	9767.37	9767.50
5	4882.28	4882.54	4882.79	4883.03	4883.24	4883.42	4883.57	4883.68	4883.75
6	2441.14	2441.27	2441.40	2441.51	2441.62	2441.71	2441.79	2441.84	2441.87
7	1220.57	1220.63	1220.70	1220.76	1220.81	1220.86	1220.89	1220.92	1220.94
8	610.285	610.317	610.349	610.378	610.405	610.428	610.447	610.460	610.469
9	305.143	305.159	305.174	305.189	305.203	305.214	305.223	305.230	305.234
10	152.571	152.579	152.587	152.595	152.601	152.607	152.612	152.615	152.617
11	76.2856	76.2897	76.2936	76.2973	76.3006	76.3035	76.3058	76.3075	76.3086
12	38.1428	38.1448	38.1468	38.1487	38.1503	38.1518	38.1529	38.1538	38.1543
13	19.0714	19.0724	19.0734	19.0743	19.0752	19.0759	19.0765	19.0769	19.0771
14	9.53570	9.53621	9.53670	9.53716	9.53758	9.53794	9.53823	9.53844	9.53857
15	4.76785	4.76811	4.76835	4.76858	4.76879	4.76897	4.76911	4.76922	4.76929
16	2.38393	2.38405	2.38418	2.38429	2.38439	2.38448	2.38456	2.38461	2.38464
17	1.19196	1.19203	1.19209	1.19215	1.19220	1.19224	1.19228	1.19231	1.19232
18	0.595981	0.596013	0.596044	0.596073	0.596099	0.596121	0.596139	0.596153	0.596161
19	0.297991	0.298007	0.298022	0.298036	0.298049	0.298061	0.298070	0.298076	0.298080
20	0.148995	0.149003	0.149011	0.149018	0.149025	0.149030	0.149035	0.149038	0.149040
21	0.0744977	0.0745016	0.0745055	0.0745091	0.0745123	0.0745151	0.0745174	0.0745191	0.0745201
22	0.0372488	0.0372508	0.0372527	0.0372545	0.0372562	0.0372576	0.0372587	0.0372595	0.0372601
23	0.0186244	0.0186254	0.0186264	0.0186273	0.0186281	0.0186288	0.0186294	0.0186298	0.0186300
24	0.00931221	0.00931271	0.00931319	0.00931364	0.00931404	0.00931439	0.00931468	0.00931489	0.00931501
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 3°
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	156065	156067	156072	156080	156090	156104	156119	156136	156155
1	78032.5	78033.4	78035.8	78039.8	78045.2	78051.9	78059.6	78068.2	78077.3
2	39016.3	39016.7	39017.9	39019.9	39022.6	39026.0	39029.8	39034.1	39038.6
3	19508.1	19508.3	19509.0	19510.0	19511.3	19513.0	19514.9	19517.0	19519.3
4	9754.07	9754.17	9754.48	9754.98	9755.66	9756.49	9757.46	9758.52	9759.66
5	4877.03	4877.09	4877.24	4877.49	4877.83	4878.24	4878.73	4879.26	4879.83
6	2438.52	2438.54	2438.62	2438.74	2438.91	2439.12	2439.36	2439.63	2439.92
7	1219.26	1219.27	1219.31	1219.37	1219.46	1219.56	1219.68	1219.82	1219.96
8	609.629	609.636	609.655	609.686	609.728	609.781	609.841	609.908	609.979
9	304.815	304.818	304.827	304.843	304.864	304.890	304.921	304.954	304.989
10	152.407	152.409	152.414	152.422	152.432	152.445	152.460	152.477	152.495
11	76.2037	76.2045	76.2069	76.2108	76.2161	76.2226	76.2301	76.2385	76.2473
12	38.1018	38.1022	38.1034	38.1054	38.1080	38.1113	38.1151	38.1192	38.1237
13	19.0509	19.0511	19.0517	19.0527	19.0540	19.0556	19.0575	19.0596	19.0618
14	9.52546	9.52556	9.52586	9.52635	9.52701	9.52782	9.52877	9.52981	9.53092
15	4.76273	4.76278	4.76293	4.76317	4.76350	4.76391	4.76438	4.76490	4.76546
16	2.38136	2.38139	2.38146	2.38159	2.38175	2.38196	2.38219	2.38245	2.38273
17	1.19068	1.19069	1.19073	1.19079	1.19088	1.19098	1.19110	1.19123	1.19136
18	0.595341	0.595347	0.595366	0.595397	0.595438	0.595489	0.595548	0.595613	0.595682
19	0.297671	0.297674	0.297683	0.297698	0.297719	0.297744	0.297774	0.297807	0.297841
20	0.148835	0.148837	0.148842	0.148849	0.148859	0.148872	0.148887	0.148903	0.148921
21	0.0744176	0.0744184	0.0744208	0.0744246	0.0744297	0.0744361	0.0744435	0.0744516	0.0744603
22	0.0372088	0.0372092	0.0372104	0.0372123	0.0372149	0.0372181	0.0372217	0.0372258	0.0372302
23	0.0186044	0.0186046	0.0186052	0.0186061	0.0186074	0.0186090	0.0186109	0.0186129	0.0186151
24	0.00930220	0.00930230	0.00930259	0.00930307	0.00930372	0.00930451	0.00930544	0.00930645	0.00930754
Longitude = Central Meridian + 3°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	156173	156192	156210	156227	156242	156256	156266	156274	156279
1	78086.7	78096.0	78105.1	78113.6	78121.2	78127.8	78133.2	78137.1	78139.5
2	39043.3	39048.0	39052.5	39056.8	39060.6	39063.9	39066.6	39068.6	39069.8
3	19521.7	19524.0	19526.3	19528.4	19530.3	19532.0	19533.3	19534.3	19534.9
4	9760.83	9762.00	9763.13	9764.19	9765.15	9765.98	9766.65	9767.14	9767.44
5	4880.42	4881.00	4881.57	4882.10	4882.58	4882.99	4883.32	4883.57	4883.72
6	2440.21	2440.50	2440.78	2441.05	2441.29	2441.49	2441.66	2441.79	2441.86
7	1220.10	1220.25	1220.39	1220.52	1220.64	1220.75	1220.83	1220.89	1220.93
8	610.052	610.125	610.196	610.262	610.322	610.374	610.416	610.446	610.465
9	305.026	305.063	305.098	305.131	305.161	305.187	305.208	305.223	305.233
10	152.513	152.531	152.549	152.566	152.581	152.593	152.604	152.612	152.616
11	76.2565	76.2656	76.2745	76.2828	76.2903	76.2967	76.3019	76.3058	76.3081
12	38.1282	38.1328	38.1372	38.1414	38.1451	38.1484	38.1510	38.1529	38.1541
13	19.0641	19.0664	19.0686	19.0707	19.0726	19.0742	19.0755	19.0764	19.0770
14	9.53206	9.53320	9.53431	9.53535	9.53628	9.53709	9.53774	9.53822	9.53852
15	4.76603	4.76660	4.76715	4.76767	4.76814	4.76854	4.76887	4.76911	4.76926
16	2.38302	2.38330	2.38358	2.38384	2.38407	2.38427	2.38444	2.38456	2.38463
17	1.19151	1.19165	1.19179	1.19192	1.19204	1.19214	1.19222	1.19228	1.19231
18	0.595754	0.595825	0.595894	0.595959	0.596018	0.596068	0.596109	0.596139	0.596157
19	0.297877	0.297913	0.297947	0.297980	0.298009	0.298034	0.298054	0.298069	0.298079
20	0.148938	0.148956	0.148974	0.148990	0.149004	0.149017	0.149027	0.149035	0.149039
21	0.0744692	0.0744782	0.0744868	0.0744949	0.0745022	0.0745085	0.0745136	0.0745174	0.0745197
22	0.0372346	0.0372391	0.0372434	0.0372474	0.0372511	0.0372543	0.0372568	0.0372587	0.0372598
23	0.0186173	0.0186195	0.0186217	0.0186237	0.0186255	0.0186271	0.0186284	0.0186293	0.0186299
24	0.00930865	0.00930977	0.00931085	0.00931186	0.00931277	0.00931356	0.00931420	0.00931467	0.00931496
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 4°
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	155897	155900	155909	155923	155943	155966	155994	156024	156057
1	77948.7	77950.2	77954.6	77961.7	77971.3	77983.2	77996.9	78012.1	78028.3
2	38974.4	38975.1	38977.3	38980.8	38985.7	38991.6	38998.5	39006.1	39014.1
3	19487.2	19487.5	19488.6	19490.4	19492.8	19495.8	19499.2	19503.0	19507.1
4	9743.59	9743.77	9744.32	9745.21	9746.41	9747.90	9749.62	9751.51	9753.53
5	4871.80	4871.89	4872.16	4872.60	4873.21	4873.95	4874.81	4875.76	4876.77
6	2435.90	2435.94	2436.08	2436.30	2436.60	2436.97	2437.40	2437.88	2438.38
7	1217.95	1217.97	1218.04	1218.15	1218.30	1218.49	1218.70	1218.94	1219.19
8	608.974	608.986	609.020	609.075	609.151	609.244	609.351	609.470	609.596
9	304.487	304.493	304.510	304.538	304.575	304.622	304.675	304.735	304.798
10	152.244	152.246	152.255	152.269	152.288	152.311	152.338	152.367	152.399
11	76.1218	76.1232	76.1275	76.1344	76.1438	76.1554	76.1689	76.1837	76.1995
12	38.0609	38.0616	38.0637	38.0672	38.0719	38.0777	38.0844	38.0918	38.0997
13	19.0305	19.0308	19.0319	19.0336	19.0360	19.0389	19.0422	19.0459	19.0499
14	9.51523	9.51540	9.51594	9.51680	9.51798	9.51943	9.52111	9.52296	9.52494
15	4.75761	4.75770	4.75797	4.75840	4.75899	4.75972	4.76055	4.76148	4.76247
16	2.37881	2.37885	2.37898	2.37920	2.37950	2.37986	2.38028	2.38074	2.38123
17	1.18940	1.18943	1.18949	1.18960	1.18975	1.18993	1.19014	1.19037	1.19062
18	0.594702	0.594713	0.594746	0.594800	0.594874	0.594964	0.595069	0.595185	0.595308
19	0.297351	0.297356	0.297373	0.297400	0.297437	0.297482	0.297535	0.297593	0.297654
20	0.148675	0.148678	0.148687	0.148700	0.148718	0.148741	0.148767	0.148796	0.148827
21	0.0743377	0.0743391	0.0743433	0.0743500	0.0743592	0.0743706	0.0743837	0.0743981	0.0744136
22	0.0371688	0.0371695	0.0371716	0.0371750	0.0371796	0.0371853	0.0371918	0.0371991	0.0372068
23	0.0185844	0.0185848	0.0185858	0.0185875	0.0185898	0.0185926	0.0185959	0.0185995	0.0186034
24	0.00929221	0.00929239	0.00929291	0.00929375	0.00929490	0.00929632	0.00929796	0.00929977	0.00930170
Longitude = Central Meridian + 4°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	156090	156123	156155	156185	156213	156236	156255	156269	156278
1	78044.9	78061.5	78077.6	78092.7	78106.4	78118.1	78127.6	78134.6	78138.9
2	39022.5	39030.8	39038.8	39046.4	39053.2	39059.0	39063.8	39067.3	39069.5
3	19511.2	19515.4	19519.4	19523.2	19526.6	19529.5	19531.9	19533.7	19534.7
4	9755.62	9757.69	9759.71	9761.59	9763.29	9764.76	9765.95	9766.83	9767.36
5	4877.81	4878.85	4879.85	4880.80	4881.65	4882.38	4882.98	4883.41	4883.68
6	2438.90	2439.42	2439.93	2440.40	2440.82	2441.19	2441.49	2441.71	2441.84
7	1219.45	1219.71	1219.96	1220.20	1220.41	1220.60	1220.74	1220.85	1220.92
8	609.726	609.856	609.982	610.099	610.206	610.298	610.372	610.427	610.460
9	304.863	304.928	304.991	305.050	305.103	305.149	305.186	305.213	305.230
10	152.431	152.464	152.495	152.525	152.551	152.574	152.593	152.607	152.615
11	76.2157	76.2320	76.2477	76.2624	76.2757	76.2872	76.2965	76.3033	76.3075
12	38.1079	38.1160	38.1239	38.1312	38.1379	38.1436	38.1482	38.1517	38.1538
13	19.0539	19.0580	19.0619	19.0656	19.0689	19.0718	19.0741	19.0758	19.0769
14	9.52697	9.52900	9.53096	9.53280	9.53447	9.53590	9.53706	9.53792	9.53844
15	4.76348	4.76450	4.76548	4.76640	4.76723	4.76795	4.76853	4.76896	4.76922
16	2.38174	2.38225	2.38274	2.38320	2.38362	2.38398	2.38427	2.38448	2.38461
17	1.19087	1.19112	1.19137	1.19160	1.19181	1.19199	1.19213	1.19224	1.19231
18	0.595436	0.595562	0.595685	0.595800	0.595904	0.595994	0.596066	0.596120	0.596153
19	0.297718	0.297781	0.297843	0.297900	0.297952	0.297997	0.298033	0.298060	0.298076
20	0.148859	0.148891	0.148921	0.148950	0.148976	0.148998	0.149017	0.149030	0.149038
21	0.0744294	0.0744453	0.0744606	0.0744750	0.0744880	0.0744992	0.0745083	0.0745150	0.0745191
22	0.0372147	0.0372226	0.0372303	0.0372375	0.0372440	0.0372496	0.0372542	0.0372575	0.0372595
23	0.0186074	0.0186113	0.0186152	0.0186188	0.0186220	0.0186248	0.0186271	0.0186287	0.0186298
24	0.00930368	0.00930566	0.00930758	0.00930938	0.00931100	0.00931240	0.00931354	0.00931437	0.00931488
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 5°
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	155682	155687	155700	155722	155753	155790	155833	155880	155931
1	77841.0	77843.3	77850.1	77861.2	77876.3	77894.9	77916.3	77940.1	77965.3
2	38920.5	38921.6	38925.1	38930.6	38938.1	38947.4	38958.2	38970.0	38982.7
3	19460.3	19460.8	19462.5	19465.3	19469.1	19473.7	19479.1	19485.0	19491.3
4	9730.13	9730.41	9731.26	9732.65	9734.54	9736.86	9739.54	9742.51	9745.66
5	4865.06	4865.21	4865.63	4866.33	4867.27	4868.43	4869.77	4871.25	4872.83
6	2432.53	2432.60	2432.82	2433.16	2433.63	2434.21	2434.89	2435.63	2436.42
7	1216.27	1216.30	1216.41	1216.58	1216.82	1217.11	1217.44	1217.81	1218.21
8	608.133	608.151	608.204	608.291	608.409	608.554	608.721	608.907	609.104
9	304.066	304.075	304.102	304.145	304.204	304.277	304.361	304.453	304.552
10	152.033	152.038	152.051	152.073	152.102	152.138	152.180	152.227	152.276
11	76.0166	76.0188	76.0255	76.0363	76.0511	76.0692	76.0902	76.1133	76.1380
12	38.0083	38.0094	38.0127	38.0182	38.0255	38.0346	38.0451	38.0567	38.0690
13	19.0042	19.0047	19.0064	19.0091	19.0128	19.0173	19.0225	19.0283	19.0345
14	9.50208	9.50236	9.50319	9.50454	9.50638	9.50865	9.51127	9.51417	9.51725
15	4.75104	4.75118	4.75159	4.75227	4.75319	4.75432	4.75564	4.75708	4.75863
16	2.37552	2.37559	2.37580	2.37614	2.37660	2.37716	2.37782	2.37854	2.37931
17	1.18776	1.18779	1.18790	1.18807	1.18830	1.18858	1.18891	1.18927	1.18966
18	0.593880	0.593897	0.593949	0.594034	0.594149	0.594291	0.594454	0.594635	0.594828
19	0.296940	0.296949	0.296975	0.297017	0.297074	0.297145	0.297227	0.297318	0.297414
20	0.148470	0.148474	0.148487	0.148508	0.148537	0.148573	0.148614	0.148659	0.148707
21	0.0742350	0.0742372	0.0742436	0.0742542	0.0742686	0.0742863	0.0743068	0.0743294	0.0743535
22	0.0371175	0.0371186	0.0371218	0.0371271	0.0371343	0.0371432	0.0371534	0.0371647	0.0371768
23	0.0185587	0.0185593	0.0185609	0.0185636	0.0185672	0.0185716	0.0185767	0.0185824	0.0185884
24	0.00927937	0.00927964	0.00928046	0.00928178	0.00928358	0.00928579	0.00928835	0.00929118	0.00929419
Longitude = Central Meridian + 5°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	155983	156035	156085	156132	156175	156211	156241	156263	156276
1	77991.3	78017.3	78042.4	78066.0	78087.3	78105.6	78120.5	78131.4	78138.1
2	38995.7	39008.6	39021.2	39033.0	39043.6	39052.8	39060.2	39065.7	39069.1
3	19497.8	19504.3	19510.6	19516.5	19521.8	19526.4	19530.1	19532.9	19534.5
4	9748.92	9752.16	9755.31	9758.25	9760.91	9763.20	9765.06	9766.43	9767.26
5	4874.46	4876.08	4877.65	4879.13	4880.45	4881.60	4882.53	4883.21	4883.63
6	2437.23	2438.04	2438.83	2439.56	2440.23	2440.80	2441.26	2441.61	2441.82
7	1218.61	1219.02	1219.41	1219.78	1220.11	1220.40	1220.63	1220.80	1220.91
8	609.307	609.510	609.707	609.891	610.057	610.200	610.316	610.402	610.454
9	304.654	304.755	304.853	304.945	305.028	305.100	305.158	305.201	305.227
10	152.327	152.378	152.427	152.473	152.514	152.550	152.579	152.600	152.613
11	76.1634	76.1888	76.2133	76.2363	76.2571	76.2750	76.2895	76.3002	76.3067
12	38.0817	38.0944	38.1067	38.1182	38.1285	38.1375	38.1448	38.1501	38.1534
13	19.0409	19.0472	19.0533	19.0591	19.0643	19.0688	19.0724	19.0751	19.0767
14	9.52043	9.52360	9.52667	9.52954	9.53214	9.53438	9.53619	9.53753	9.53834
15	4.76021	4.76180	4.76333	4.76477	4.76607	4.76719	4.76809	4.76876	4.76917
16	2.38011	2.38090	2.38167	2.38239	2.38303	2.38359	2.38405	2.38438	2.38459
17	1.19005	1.19045	1.19083	1.19119	1.19152	1.19180	1.19202	1.19219	1.19229
18	0.595027	0.595225	0.595417	0.595596	0.595759	0.595898	0.596012	0.596095	0.596146
19	0.297513	0.297612	0.297708	0.297798	0.297879	0.297949	0.298006	0.298048	0.298073
20	0.148757	0.148806	0.148854	0.148899	0.148940	0.148975	0.149003	0.149024	0.149037
21	0.0743783	0.0744031	0.0744271	0.0744495	0.0744698	0.0744873	0.0745015	0.0745119	0.0745183
22	0.0371892	0.0372015	0.0372135	0.0372248	0.0372349	0.0372437	0.0372507	0.0372560	0.0372592
23	0.0185946	0.0186008	0.0186068	0.0186124	0.0186175	0.0186218	0.0186254	0.0186280	0.0186296
24	0.00929729	0.00930039	0.00930338	0.00930619	0.00930873	0.00931091	0.00931269	0.00931399	0.00931479
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 6°
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	155419	155425	155445	155477	155520	155574	155636	155704	155777
1	77709.4	77712.7	77722.5	77738.5	77760.2	77787.0	77817.9	77852.1	77888.5
2	38854.7	38856.4	38861.3	38869.3	38880.1	38893.5	38909.0	38926.0	38944.2
3	19427.4	19428.2	19430.6	19434.6	19440.1	19446.7	19454.5	19463.0	19472.1
4	9713.68	9714.09	9715.31	9717.32	9720.03	9723.37	9727.24	9731.51	9736.06
5	4856.84	4857.04	4857.66	4858.66	4860.02	4861.69	4863.62	4865.76	4868.03
6	2428.42	2428.52	2428.83	2429.33	2430.01	2430.84	2431.81	2432.88	2434.01
7	1214.21	1214.26	1214.41	1214.66	1215.00	1215.42	1215.90	1216.44	1217.01
8	607.105	607.131	607.207	607.332	607.502	607.711	607.952	608.219	608.504
9	303.552	303.565	303.604	303.666	303.751	303.855	303.976	304.110	304.252
10	151.776	151.783	151.802	151.833	151.875	151.928	151.988	152.055	152.126
11	75.8881	75.8913	75.9009	75.9165	75.9377	75.9638	75.9941	76.0274	76.0630
12	37.9440	37.9457	37.9504	37.9583	37.9689	37.9819	37.9970	38.0137	38.0315
13	18.9720	18.9728	18.9752	18.9791	18.9844	18.9910	18.9985	19.0069	19.0157
14	9.48601	9.48641	9.48761	9.48957	9.49222	9.49548	9.49926	9.50343	9.50787
15	4.74301	4.74321	4.74381	4.74478	4.74611	4.74774	4.74963	4.75171	4.75393
16	2.37150	2.37160	2.37190	2.37239	2.37305	2.37387	2.37481	2.37586	2.37697
17	1.18575	1.18580	1.18595	1.18620	1.18653	1.18694	1.18741	1.18793	1.18848
18	0.592876	0.592901	0.592976	0.593098	0.593264	0.593468	0.593704	0.593964	0.594242
19	0.296438	0.296450	0.296488	0.296549	0.296632	0.296734	0.296852	0.296982	0.297121
20	0.148219	0.148225	0.148244	0.148274	0.148316	0.148367	0.148426	0.148491	0.148560
21	0.0741095	0.0741126	0.0741220	0.0741372	0.0741579	0.0741834	0.0742129	0.0742455	0.0742802
22	0.0370547	0.0370563	0.0370610	0.0370686	0.0370790	0.0370917	0.0371065	0.0371228	0.0371401
23	0.0185274	0.0185282	0.0185305	0.0185343	0.0185395	0.0185459	0.0185532	0.0185614	0.0185701
24	0.00926368	0.00926408	0.00926525	0.00926716	0.00926974	0.00927293	0.00927662	0.00928069	0.00928503
Longitude = Central Meridian + 6°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	155852	155927	155999	156067	156128	156181	156223	156255	156274
1	77925.9	77963.3	77999.5	78033.4	78064.0	78090.4	78111.7	78127.5	78137.1
2	38963.0	38981.6	38999.7	39016.7	39032.0	39045.2	39055.9	39063.7	39068.6
3	19481.5	19490.8	19499.9	19508.3	19516.0	19522.6	19527.9	19531.9	19534.3
4	9740.74	9745.41	9749.94	9754.17	9758.00	9761.30	9763.97	9765.94	9767.14
5	4870.37	4872.71	4874.97	4877.09	4879.00	4880.65	4881.98	4882.97	4883.57
6	2435.18	2436.35	2437.48	2438.54	2439.50	2440.32	2440.99	2441.48	2441.78
7	1217.59	1218.18	1218.74	1219.27	1219.75	1220.16	1220.50	1220.74	1220.89
8	608.796	609.088	609.371	609.636	609.875	610.081	610.248	610.371	610.446
9	304.398	304.544	304.685	304.818	304.937	305.040	305.124	305.185	305.223
10	152.199	152.272	152.343	152.409	152.469	152.520	152.562	152.593	152.612
11	76.0995	76.1360	76.1714	76.2045	76.2344	76.2601	76.2810	76.2964	76.3058
12	38.0498	38.0680	38.0857	38.1022	38.1172	38.1301	38.1405	38.1482	38.1529
13	19.0249	19.0340	19.0428	19.0511	19.0586	19.0650	19.0702	19.0741	19.0764
14	9.51244	9.51700	9.52142	9.52556	9.52930	9.53252	9.53512	9.53705	9.53822
15	4.75622	4.75850	4.76071	4.76278	4.76465	4.76626	4.76756	4.76852	4.76911
16	2.37811	2.37925	2.38036	2.38139	2.38232	2.38313	2.38378	2.38426	2.38456
17	1.18905	1.18963	1.19018	1.19069	1.19116	1.19156	1.19189	1.19213	1.19228
18	0.594527	0.594813	0.595089	0.595347	0.595581	0.595782	0.595945	0.596065	0.596139
19	0.297264	0.297406	0.297544	0.297674	0.297790	0.297891	0.297973	0.298033	0.298069
20	0.148632	0.148703	0.148772	0.148837	0.148895	0.148946	0.148986	0.149016	0.149035
21	0.0743159	0.0743516	0.0743861	0.0744184	0.0744476	0.0744728	0.0744932	0.0745082	0.0745174
22	0.0371580	0.0371758	0.0371931	0.0372092	0.0372238	0.0372364	0.0372466	0.0372541	0.0372587
23	0.0185790	0.0185879	0.0185965	0.0186046	0.0186119	0.0186182	0.0186233	0.0186270	0.0186293
24	0.00928949	0.00929395	0.00929826	0.00930230	0.00930595	0.00930910	0.00931165	0.00931352	0.00931467
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 7°
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	155108	155117	155144	155187	155246	155319	155403	155497	155596
1	77554.0	77558.5	77571.8	77593.6	77623.2	77659.6	77701.7	77748.3	77797.8
2	38777.0	38779.2	38785.9	38796.8	38811.6	38829.8	38850.9	38874.1	38898.9
3	19388.5	19389.6	19393.0	19398.4	19405.8	19414.9	19425.4	19437.1	19449.4
4	9694.25	9694.81	9696.48	9699.21	9702.90	9707.45	9712.72	9718.53	9724.72
5	4847.12	4847.40	4848.24	4849.60	4851.45	4853.73	4856.36	4859.27	4862.36
6	2423.56	2423.70	2424.12	2424.80	2425.73	2426.86	2428.18	2429.63	2431.18
7	1211.78	1211.85	1212.06	1212.40	1212.86	1213.43	1214.09	1214.82	1215.59
8	605.890	605.926	606.030	606.200	606.431	606.716	607.045	607.408	607.795
9	302.945	302.963	303.015	303.100	303.216	303.358	303.522	303.704	303.897
10	151.473	151.481	151.507	151.550	151.608	151.679	151.761	151.852	151.949
11	75.7363	75.7407	75.7537	75.7750	75.8039	75.8395	75.8806	75.9260	75.9744
12	37.8681	37.8703	37.8769	37.8875	37.9020	37.9197	37.9403	37.9630	37.9872
13	18.9341	18.9352	18.9384	18.9438	18.9510	18.9599	18.9702	18.9815	18.9936
14	9.46704	9.46759	9.46922	9.47188	9.47549	9.47993	9.48508	9.49075	9.49680
15	4.73352	4.73379	4.73461	4.73594	4.73774	4.73997	4.74254	4.74538	4.74840
16	2.36676	2.36690	2.36730	2.36797	2.36887	2.36998	2.37127	2.37269	2.37420
17	1.18338	1.18345	1.18365	1.18399	1.18444	1.18499	1.18563	1.18634	1.18710
18	0.591690	0.591724	0.591826	0.591993	0.592218	0.592496	0.592817	0.593172	0.593550
19	0.295845	0.295862	0.295913	0.295996	0.296109	0.296248	0.296409	0.296586	0.296775
20	0.147922	0.147931	0.147957	0.147998	0.148055	0.148124	0.148204	0.148293	0.148387
21	0.0739612	0.0739655	0.0739783	0.0739991	0.0740273	0.0740620	0.0741022	0.0741465	0.0741937
22	0.0369806	0.0369828	0.0369891	0.0369995	0.0370136	0.0370310	0.0370511	0.0370733	0.0370969
23	0.0184903	0.0184914	0.0184946	0.0184998	0.0185068	0.0185155	0.0185255	0.0185366	0.0185484
24	0.00924515	0.00924569	0.00924728	0.00924988	0.00925341	0.00925775	0.00926277	0.00926831	0.00927422
Longitude = Central Meridian + 7°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	155697	155799	155898	155990	156073	156145	156203	156246	156272
1	77848.7	77899.6	77948.8	77994.9	78036.5	78072.4	78101.5	78122.9	78135.9
2	38924.4	38949.8	38974.4	38997.5	39018.3	39036.2	39050.7	39061.4	39068.0
3	19462.2	19474.9	19487.2	19498.7	19509.1	19518.1	19525.4	19530.7	19534.0
4	9731.09	9737.45	9743.60	9749.36	9754.57	9759.05	9762.68	9765.36	9766.99
5	4865.54	4868.72	4871.80	4874.68	4877.28	4879.52	4881.34	4882.68	4883.50
6	2432.77	2434.36	2435.90	2437.34	2438.64	2439.76	2440.67	2441.34	2441.75
7	1216.39	1217.18	1217.95	1218.67	1219.32	1219.88	1220.34	1220.67	1220.87
8	608.193	608.590	608.975	609.335	609.660	609.941	610.168	610.335	610.437
9	304.097	304.295	304.488	304.668	304.830	304.970	305.084	305.167	305.219
10	152.048	152.148	152.244	152.334	152.415	152.485	152.542	152.584	152.609
11	76.0241	76.0738	76.1219	76.1669	76.2075	76.2426	76.2710	76.2918	76.3046
12	38.0121	38.0369	38.0609	38.0835	38.1038	38.1213	38.1355	38.1459	38.1523
13	19.0060	19.0185	19.0305	19.0417	19.0519	19.0606	19.0677	19.0730	19.0762
14	9.50302	9.50923	9.51523	9.52086	9.52594	9.53032	9.53387	9.53648	9.53808
15	4.75151	4.75461	4.75762	4.76043	4.76297	4.76516	4.76693	4.76824	4.76904
16	2.37575	2.37731	2.37881	2.38022	2.38149	2.38258	2.38347	2.38412	2.38452
17	1.18788	1.18865	1.18940	1.19011	1.19074	1.19129	1.19173	1.19206	1.19226
18	0.593939	0.594327	0.594702	0.595054	0.595371	0.595645	0.595867	0.596030	0.596130
19	0.296969	0.297163	0.297351	0.297527	0.297686	0.297823	0.297933	0.298015	0.298065
20	0.148485	0.148582	0.148676	0.148763	0.148843	0.148911	0.148967	0.149008	0.149032
21	0.0742423	0.0742908	0.0743378	0.0743817	0.0744214	0.0744556	0.0744834	0.0745038	0.0745162
22	0.0371212	0.0371454	0.0371689	0.0371909	0.0372107	0.0372278	0.0372417	0.0372519	0.0372581
23	0.0185606	0.0185727	0.0185844	0.0185954	0.0186054	0.0186139	0.0186208	0.0186259	0.0186291
24	0.00928029	0.00928635	0.00929222	0.00929772	0.00930268	0.00930695	0.00931042	0.00931297	0.00931453
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 8°
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	154749	154761	154796	154853	154931	155026	155136	155257	155387
1	77374.7	77380.6	77398.1	77426.6	77465.3	77512.8	77567.9	77628.6	77693.3
2	38687.4	38690.3	38699.1	38713.3	38732.6	38756.4	38783.9	38814.3	38846.6
3	19343.7	19345.2	19349.5	19356.7	19366.3	19378.2	19392.0	19407.2	19423.3
4	9671.84	9672.58	9674.76	9678.33	9683.16	9689.10	9695.98	9703.58	9711.66
5	4835.92	4836.29	4837.38	4839.16	4841.58	4844.55	4847.99	4851.79	4855.83
6	2417.96	2418.14	2418.69	2419.58	2420.79	2422.28	2424.00	2425.89	2427.91
7	1208.98	1209.07	1209.35	1209.79	1210.39	1211.14	1212.00	1212.95	1213.96
8	604.490	604.536	604.673	604.895	605.197	605.569	605.999	606.474	606.979
9	302.245	302.268	302.336	302.448	302.599	302.784	302.999	303.237	303.489
10	151.123	151.134	151.168	151.224	151.299	151.392	151.500	151.618	151.745
11	75.5613	75.5670	75.5841	75.6119	75.6497	75.6961	75.7499	75.8092	75.8723
12	37.7806	37.7835	37.7920	37.8060	37.8248	37.8481	37.8749	37.9046	37.9362
13	18.8903	18.8918	18.8960	18.9030	18.9124	18.9240	18.9375	18.9523	18.9681
14	9.44516	9.44588	9.44801	9.45149	9.45621	9.46201	9.46873	9.47615	9.48404
15	4.72258	4.72294	4.72401	4.72575	4.72810	4.73101	4.73437	4.73808	4.74202
16	2.36129	2.36147	2.36200	2.36287	2.36405	2.36550	2.36718	2.36904	2.37101
17	1.18064	1.18073	1.18100	1.18144	1.18203	1.18275	1.18359	1.18452	1.18551
18	0.590322	0.590367	0.590501	0.590718	0.591013	0.591376	0.591796	0.592259	0.592753
19	0.295161	0.295184	0.295250	0.295359	0.295506	0.295688	0.295898	0.296130	0.296376
20	0.147581	0.147592	0.147625	0.147680	0.147753	0.147844	0.147949	0.148065	0.148188
21	0.0737903	0.0737959	0.0738126	0.0738398	0.0738766	0.0739220	0.0739745	0.0740324	0.0740941
22	0.0368952	0.0368980	0.0369063	0.0369199	0.0369383	0.0369610	0.0369872	0.0370162	0.0370470
23	0.0184476	0.0184490	0.0184531	0.0184599	0.0184692	0.0184805	0.0184936	0.0185081	0.0185235
24	0.00922379	0.00922449	0.00922657	0.00922997	0.00923458	0.00924025	0.00924681	0.00925405	0.00926176
Longitude = Central Meridian + 8°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	155520	155652	155781	155901	156010	156103	156179	156235	156269
1	77759.8	77826.2	77890.5	77950.6	78004.9	78051.7	78089.6	78117.5	78134.6
2	38879.9	38913.1	38945.2	38975.3	39002.5	39025.9	39044.8	39058.8	39067.3
3	19440.0	19456.6	19472.6	19487.7	19501.2	19512.9	19522.4	19529.4	19533.7
4	9719.98	9728.28	9736.31	9743.83	9750.62	9756.46	9761.20	9764.69	9766.83
5	4859.99	4864.14	4868.15	4871.91	4875.31	4878.23	4880.60	4882.35	4883.41
6	2429.99	2432.07	2434.08	2435.96	2437.65	2439.12	2440.30	2441.17	2441.71
7	1215.00	1216.03	1217.04	1217.98	1218.83	1219.56	1220.15	1220.59	1220.85
8	607.498	608.017	608.519	608.989	609.413	609.779	610.075	610.293	610.427
9	303.749	304.009	304.260	304.495	304.707	304.890	305.038	305.147	305.213
10	151.875	152.004	152.130	152.247	152.353	152.445	152.519	152.573	152.607
11	75.9373	76.0022	76.0649	76.1237	76.1767	76.2224	76.2594	76.2867	76.3033
12	37.9687	38.0011	38.0324	38.0618	38.0883	38.1112	38.1297	38.1433	38.1517
13	18.9843	19.0005	19.0162	19.0309	19.0442	19.0556	19.0649	19.0717	19.0758
14	9.49216	9.50027	9.50811	9.51546	9.52209	9.52780	9.53243	9.53583	9.53792
15	4.74608	4.75013	4.75406	4.75773	4.76104	4.76390	4.76621	4.76792	4.76896
16	2.37304	2.37507	2.37703	2.37886	2.38052	2.38195	2.38311	2.38396	2.38448
17	1.18652	1.18753	1.18851	1.18943	1.19026	1.19097	1.19155	1.19198	1.19224
18	0.593260	0.593767	0.594257	0.594716	0.595130	0.595487	0.595777	0.595989	0.596120
19	0.296630	0.296883	0.297129	0.297358	0.297565	0.297744	0.297888	0.297995	0.298060
20	0.148315	0.148442	0.148564	0.148679	0.148783	0.148872	0.148944	0.148997	0.149030
21	0.0741575	0.0742208	0.0742821	0.0743395	0.0743913	0.0744359	0.0744721	0.0744987	0.0745150
22	0.0370788	0.0371104	0.0371411	0.0371698	0.0371956	0.0372180	0.0372360	0.0372493	0.0372575
23	0.0185394	0.0185552	0.0185705	0.0185849	0.0185978	0.0186090	0.0186180	0.0186247	0.0186287
24	0.00926969	0.00927761	0.00928527	0.00929244	0.00929891	0.00930449	0.00930901	0.00931234	0.00931437
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 9°
N	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	154344	154358	154403	154475	154573	154693	154833	154987	155150
1	77171.8	77179.2	77201.4	77237.5	77286.4	77346.7	77416.3	77493.3	77575.1
2	38585.9	38589.6	38600.7	38618.7	38643.2	38673.3	38708.2	38746.6	38787.5
3	19292.9	19294.8	19300.3	19309.4	19321.6	19336.7	19354.1	19373.3	19393.8
4	9646.47	9647.41	9650.17	9654.69	9660.80	9668.33	9677.04	9686.66	9696.88
5	4823.24	4823.70	4825.09	4827.34	4830.40	4834.17	4838.52	4843.33	4848.44
6	2411.62	2411.85	2412.54	2413.67	2415.20	2417.08	2419.26	2421.66	2424.22
7	1205.81	1205.93	1206.27	1206.84	1207.60	1208.54	1209.63	1210.83	1212.11
8	602.905	602.963	603.136	603.418	603.800	604.271	604.815	605.416	606.055
9	301.452	301.481	301.568	301.709	301.900	302.135	302.408	302.708	303.028
10	150.726	150.741	150.784	150.854	150.950	151.068	151.204	151.354	151.514
11	75.3631	75.3704	75.3920	75.4272	75.4750	75.5339	75.6019	75.6770	75.7569
12	37.6815	37.6852	37.6960	37.7136	37.7375	37.7669	37.8009	37.8385	37.8785
13	18.8408	18.8426	18.8480	18.8568	18.8688	18.8835	18.9005	18.9193	18.9392
14	9.42039	9.42130	9.42400	9.42840	9.43438	9.44173	9.45024	9.45963	9.46961
15	4.71019	4.71065	4.71200	4.71420	4.71719	4.72087	4.72512	4.72981	4.73481
16	2.35510	2.35532	2.35600	2.35710	2.35859	2.36043	2.36256	2.36491	2.36740
17	1.17755	1.17766	1.17800	1.17855	1.17930	1.18022	1.18128	1.18245	1.18370
18	0.588774	0.588831	0.589000	0.589275	0.589649	0.590108	0.590640	0.591227	0.591851
19	0.294387	0.294415	0.294500	0.294638	0.294824	0.295054	0.295320	0.295613	0.295925
20	0.147194	0.147208	0.147250	0.147319	0.147412	0.147527	0.147660	0.147807	0.147963
21	0.0735968	0.0736039	0.0736250	0.0736594	0.0737061	0.0737635	0.0738300	0.0739033	0.0739813
22	0.0367984	0.0368019	0.0368125	0.0368297	0.0368530	0.0368818	0.0369150	0.0369517	0.0369907
23	0.0183992	0.0184010	0.0184062	0.0184149	0.0184265	0.0184409	0.0184575	0.0184758	0.0184953
24	0.00919959	0.00920048	0.00920312	0.00920743	0.00921326	0.00922044	0.00922875	0.00923792	0.00924767
Longitude = Central Meridian + 9°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	155318	155486	155649	155801	155938	156057	156153	156223	156266
1	77659.2	77743.2	77824.5	77900.6	77969.2	78028.3	78076.3	78111.5	78133.1
2	38829.6	38871.6	38912.2	38950.3	38984.6	39014.2	39038.1	39055.8	39066.5
3	19414.8	19435.8	19456.1	19475.1	19492.3	19507.1	19519.1	19527.9	19533.3
4	9707.41	9717.90	9728.06	9737.57	9746.15	9753.54	9759.53	9763.94	9766.64
5	4853.70	4858.95	4864.03	4868.79	4873.08	4876.77	4879.77	4881.97	4883.32
6	2426.85	2429.48	2432.02	2434.39	2436.54	2438.39	2439.88	2440.98	2441.66
7	1213.43	1214.74	1216.01	1217.20	1218.27	1219.19	1219.94	1220.49	1220.83
8	606.713	607.369	608.004	608.598	609.134	609.596	609.971	610.246	610.415
9	303.356	303.685	304.002	304.299	304.567	304.798	304.985	305.123	305.207
10	151.678	151.842	152.001	152.150	152.284	152.399	152.493	152.562	152.604
11	75.8391	75.9211	76.0005	76.0748	76.1418	76.1996	76.2463	76.2808	76.3018
12	37.9196	37.9606	38.0002	38.0374	38.0709	38.0998	38.1232	38.1404	38.1509
13	18.9598	18.9803	19.0001	19.0187	19.0355	19.0499	19.0616	19.0702	19.0755
14	9.47989	9.49014	9.50006	9.50935	9.51773	9.52494	9.53079	9.53510	9.53773
15	4.73994	4.74507	4.75003	4.75467	4.75886	4.76247	4.76540	4.76755	4.76887
16	2.36997	2.37254	2.37502	2.37734	2.37943	2.38124	2.38270	2.38377	2.38443
17	1.18499	1.18627	1.18751	1.18867	1.18972	1.19062	1.19135	1.19189	1.19222
18	0.592493	0.593134	0.593754	0.594334	0.594858	0.595309	0.595675	0.595944	0.596108
19	0.296247	0.296567	0.296877	0.297167	0.297429	0.297655	0.297837	0.297972	0.298054
20	0.148123	0.148283	0.148438	0.148584	0.148714	0.148827	0.148919	0.148986	0.149027
21	0.0740616	0.0741417	0.0742192	0.0742918	0.0743572	0.0744136	0.0744593	0.0744929	0.0745135
22	0.0370308	0.0370709	0.0371096	0.0371459	0.0371786	0.0372068	0.0372297	0.0372465	0.0372568
23	0.0185154	0.0185354	0.0185548	0.0185729	0.0185893	0.0186034	0.0186148	0.0186232	0.0186284
24	0.00925770	0.00926772	0.00927740	0.00928647	0.00929465	0.00930170	0.00930741	0.00931162	0.00931419
Table 3: Tiled transverse Mercator zoom-levels scale sets
Longitude = Central Meridian + 10°
n	0°	5°	10°	15°	20°	25°	30°	35°	40°
0	153890	153909	153963	154053	154174	154322	154495	154685	154886
1	76945.2	76954.4	76981.7	77026.3	77086.8	77161.2	77247.3	77342.3	77443.2
2	38472.6	38477.2	38490.9	38513.2	38543.4	38580.6	38623.6	38671.1	38721.6
3	19236.3	19238.6	19245.4	19256.6	19271.7	19290.3	19311.8	19335.6	19360.8
4	9618.15	9619.30	9622.72	9628.29	9635.85	9645.15	9655.91	9667.78	9680.40
5	4809.07	4809.65	4811.36	4814.15	4817.93	4822.58	4827.95	4833.89	4840.20
6	2404.54	2404.82	2405.68	2407.07	2408.96	2411.29	2413.98	2416.95	2420.10
7	1202.27	1202.41	1202.84	1203.54	1204.48	1205.64	1206.99	1208.47	1210.05
8	601.134	601.206	601.420	601.768	602.241	602.822	603.494	604.236	605.025
9	300.567	300.603	300.710	300.884	301.120	301.411	301.747	302.118	302.513
10	150.284	150.302	150.355	150.442	150.560	150.706	150.874	151.059	151.256
11	75.1418	75.1508	75.1775	75.2210	75.2801	75.3528	75.4368	75.5295	75.6282
12	37.5709	37.5754	37.5887	37.6105	37.6400	37.6764	37.7184	37.7648	37.8141
13	18.7854	18.7877	18.7944	18.8053	18.8200	18.8382	18.8592	18.8824	18.9070
14	9.39272	9.39385	9.39718	9.40263	9.41001	9.41910	9.42960	9.44119	9.45352
15	4.69636	4.69692	4.69859	4.70131	4.70501	4.70955	4.71480	4.72060	4.72676
16	2.34818	2.34846	2.34930	2.35066	2.35250	2.35477	2.35740	2.36030	2.36338
17	1.17409	1.17423	1.17465	1.17533	1.17625	1.17739	1.17870	1.18015	1.18169
18	0.587045	0.587115	0.587324	0.587664	0.588126	0.588693	0.589350	0.590075	0.590845
19	0.293523	0.293558	0.293662	0.293832	0.294063	0.294347	0.294675	0.295037	0.295423
20	0.146761	0.146779	0.146831	0.146916	0.147031	0.147173	0.147337	0.147519	0.147711
21	0.0733806	0.0733894	0.0734155	0.0734580	0.0735157	0.0735867	0.0736687	0.0737593	0.0738556
22	0.0366903	0.0366947	0.0367077	0.0367290	0.0367579	0.0367933	0.0368344	0.0368797	0.0369278
23	0.0183452	0.0183474	0.0183539	0.0183645	0.0183789	0.0183967	0.0184172	0.0184398	0.0184639
24	0.00917258	0.00917368	0.00917694	0.00918226	0.00918946	0.00919834	0.00920859	0.00921992	0.00923195
Longitude = Central Meridian + 10°
n	45°	50°	55°	60°	65°	70°	75°	80°	85°
0	155094	155302	155502	155690	155859	156005	156123	156210	156263
1	77547.1	77650.8	77751.0	77844.8	77929.4	78002.3	78061.4	78104.8	78131.4
2	38773.6	38825.4	38875.5	38922.4	38964.7	39001.2	39030.7	39052.4	39065.7
3	19386.8	19412.7	19437.7	19461.2	19482.4	19500.6	19515.3	19526.2	19532.9
4	9693.39	9706.34	9718.87	9730.60	9741.18	9750.29	9757.67	9763.10	9766.43
5	4846.70	4853.17	4859.44	4865.30	4870.59	4875.14	4878.84	4881.55	4883.21
6	2423.35	2426.59	2429.72	2432.65	2435.29	2437.57	2439.42	2440.78	2441.61
7	1211.67	1213.29	1214.86	1216.32	1217.65	1218.79	1219.71	1220.39	1220.80
8	605.837	606.646	607.430	608.162	608.824	609.393	609.854	610.194	610.402
9	302.918	303.323	303.715	304.081	304.412	304.697	304.927	305.097	305.201
10	151.459	151.662	151.857	152.041	152.206	152.348	152.464	152.548	152.600
11	75.7296	75.8308	75.9287	76.0203	76.1029	76.1741	76.2318	76.2742	76.3002
12	37.8648	37.9154	37.9643	38.0102	38.0515	38.0871	38.1159	38.1371	38.1501
13	18.9324	18.9577	18.9822	19.0051	19.0257	19.0435	19.0580	19.0686	19.0751
14	9.46620	9.47885	9.49109	9.50254	9.51287	9.52177	9.52898	9.53428	9.53753
15	4.73310	4.73943	4.74554	4.75127	4.75643	4.76088	4.76449	4.76714	4.76876
16	2.36655	2.36971	2.37277	2.37563	2.37822	2.38044	2.38224	2.38357	2.38438
17	1.18328	1.18486	1.18639	1.18782	1.18911	1.19022	1.19112	1.19178	1.19219
18	0.591638	0.592428	0.593193	0.593909	0.594554	0.595110	0.595561	0.595892	0.596095
19	0.295819	0.296214	0.296596	0.296954	0.297277	0.297555	0.297780	0.297946	0.298048
20	0.147909	0.148107	0.148298	0.148477	0.148639	0.148778	0.148890	0.148973	0.149024
21	0.0739547	0.0740535	0.0741491	0.0742386	0.0743193	0.0743888	0.0744451	0.0744866	0.0745119
22	0.0369774	0.0370268	0.0370746	0.0371193	0.0371596	0.0371944	0.0372226	0.0372433	0.0372560
23	0.0184887	0.0185134	0.0185373	0.0185596	0.0185798	0.0185972	0.0186113	0.0186216	0.0186280
24	0.00924434	0.00925669	0.00926864	0.00927982	0.00928991	0.00929860	0.00930564	0.00931082	0.00931399
Table 4: Tiled polar stereographic zoom-levels scale sets

n	0°	1°	2°	3°	4°	5°	6°	7°	8°	9°
0	72507.7	73764.6	75021.0	76276.5	77530.7	78783.2	80033.8	81281.9	82527.3	83769.5
1	36253.9	36882.3	37510.5	38138.2	38765.3	39391.6	40016.9	40641.0	41263.6	41884.8
2	18126.9	18441.2	18755.2	19069.1	19382.7	19695.8	20008.4	20320.5	20631.8	20942.4
3	9063.47	9220.58	9377.62	9534.56	9691.33	9847.90	10004.2	10160.2	10315.9	10471.2
4	4531.73	4610.29	4688.81	4767.28	4845.67	4923.95	5002.11	5080.12	5157.96	5235.60
5	2265.87	2305.14	2344.41	2383.64	2422.83	2461.98	2501.05	2540.06	2578.98	2617.80
6	1132.93	1152.57	1172.20	1191.82	1211.42	1230.99	1250.53	1270.03	1289.49	1308.90
7	566.467	576.286	586.102	595.910	605.708	615.494	625.264	635.015	644.744	654.449
8	283.233	288.143	293.051	297.955	302.854	307.747	312.632	317.507	322.372	327.225
9	141.617	144.072	146.525	148.977	151.427	153.873	156.316	158.754	161.186	163.612
10	70.8083	72.0358	73.2627	74.4887	75.7135	76.9367	78.1580	79.3769	80.5931	81.8062
11	35.4042	36.0179	36.6313	37.2444	37.8568	38.4684	39.0790	39.6884	40.2965	40.9031
12	17.7021	18.0089	18.3157	18.6222	18.9284	19.2342	19.5395	19.8442	20.1483	20.4515
13	8.85104	9.00447	9.15784	9.31109	9.46419	9.61709	9.76975	9.92211	10.0741	10.2258
14	4.42552	4.50224	4.57892	4.65555	4.73210	4.80855	4.88487	4.96105	5.03707	5.11289
15	2.21276	2.25112	2.28946	2.32777	2.36605	2.40427	2.44244	2.48053	2.51853	2.55644
16	1.10638	1.12556	1.14473	1.16389	1.18302	1.20214	1.22122	1.24026	1.25927	1.27822
17	0.553190	0.562779	0.572365	0.581943	0.591512	0.601068	0.610609	0.620132	0.629633	0.639111
18	0.276595	0.281390	0.286182	0.290972	0.295756	0.300534	0.305305	0.310066	0.314817	0.319555
19	0.138298	0.140695	0.143091	0.145486	0.147878	0.150267	0.152652	0.155033	0.157408	0.159778
20	0.0691488	0.0703474	0.0715456	0.0727429	0.0739390	0.0751335	0.0763261	0.0775165	0.0787042	0.0798889
21	0.0345744	0.0351737	0.0357728	0.0363715	0.0369695	0.0375668	0.0381631	0.0387582	0.0393521	0.0399444
22	0.0172872	0.0175869	0.0178864	0.0181857	0.0184848	0.0187834	0.0190815	0.0193791	0.0196760	0.0199722
23	0.00864360	0.00879343	0.00894320	0.00909286	0.00924238	0.00939169	0.00954077	0.00968956	0.00983802	0.00998611
24	0.00432180	0.00439671	0.00447160	0.00454643	0.00462119	0.00469585	0.00477038	0.00484478	0.00491901	0.00499305
										
n	10°	11°	12°	13°	14°	15°	16°	17°	18°	19°
0	85008.3	86243.1	87473.8	88699.8	89920.8	91136.5	92346.5	93550.4	94748.0	95938.7
1	42504.1	43121.6	43736.9	44349.9	44960.4	45568.3	46173.3	46775.2	47374.0	47969.3
2	21252.1	21560.8	21868.4	22174.9	22480.2	22784.1	23086.6	23387.6	23687.0	23984.7
3	10626.0	10780.4	10934.2	11087.5	11240.1	11392.1	11543.3	11693.8	11843.5	11992.3
4	5313.02	5390.20	5467.11	5543.74	5620.05	5696.03	5771.66	5846.90	5921.75	5996.17
5	2656.51	2695.10	2733.56	2771.87	2810.03	2848.02	2885.83	2923.45	2960.87	2998.08
6	1328.25	1347.55	1366.78	1385.93	1405.01	1424.01	1442.91	1461.73	1480.44	1499.04
7	664.127	673.775	683.389	692.967	702.506	712.004	721.457	730.863	740.218	749.521
8	332.064	336.887	341.694	346.484	351.253	356.002	360.729	365.431	370.109	374.760
9	166.032	168.444	170.847	173.242	175.627	178.001	180.364	182.716	185.055	187.380
10	83.0159	84.2218	85.4236	86.6209	87.8133	89.0005	90.1821	91.3579	92.5273	93.6901
11	41.5079	42.1109	42.7118	43.3104	43.9067	44.5003	45.0911	45.6789	46.2637	46.8451
12	20.7540	21.0555	21.3559	21.6552	21.9533	22.2501	22.5455	22.8395	23.1318	23.4225
13	10.3770	10.5277	10.6780	10.8276	10.9767	11.1251	11.2728	11.4197	11.5659	11.7113
14	5.18849	5.26386	5.33898	5.41381	5.48833	5.56253	5.63638	5.70987	5.78296	5.85563
15	2.59425	2.63193	2.66949	2.70690	2.74417	2.78127	2.81819	2.85493	2.89148	2.92782
16	1.29712	1.31597	1.33474	1.35345	1.37208	1.39063	1.40910	1.42747	1.44574	1.46391
17	0.648562	0.657983	0.667372	0.676726	0.686041	0.695316	0.704548	0.713733	0.722870	0.731954
18	0.324281	0.328991	0.333686	0.338363	0.343021	0.347658	0.352274	0.356867	0.361435	0.365977
19	0.162140	0.164496	0.166843	0.169181	0.171510	0.173829	0.176137	0.178433	0.180717	0.182989
20	0.0810702	0.0822479	0.0834215	0.0845907	0.0857552	0.0869146	0.0880685	0.0892167	0.0903587	0.0914943
21	0.0405351	0.0411239	0.0417107	0.0422954	0.0428776	0.0434573	0.0440343	0.0446083	0.0451793	0.0457471
22	0.0202676	0.0205620	0.0208554	0.0211477	0.0214388	0.0217286	0.0220171	0.0223042	0.0225897	0.0228736
23	0.0101338	0.0102810	0.0104277	0.0105738	0.0107194	0.0108643	0.0110086	0.0111521	0.0112948	0.0114368
24	0.00506689	0.00514049	0.00521384	0.00528692	0.00535970	0.00543216	0.00550428	0.00557604	0.00564742	0.00571839
Table 4: Tiled polar stereographic zoom-levels scale sets

n	20°	21°	22°	23°	24°	25°	26°	27°	28°	29°
0	97122.3	98298.4	99466.6	100627	101778	102921	104054	105178	106292	107396
1	48561.1	49149.2	49733.3	50313.3	50889.1	51460.4	52027.1	52589.0	53146.0	53697.8
2	24280.6	24574.6	24866.7	25156.7	25444.6	25730.2	26013.6	26294.5	26573.0	26848.9
3	12140.3	12287.3	12433.3	12578.3	12722.3	12865.1	13006.8	13147.3	13286.5	13424.5
4	6070.14	6143.65	6216.66	6289.17	6361.14	6432.55	6503.39	6573.63	6643.25	6712.23
5	3035.07	3071.82	3108.33	3144.58	3180.57	3216.28	3251.70	3286.81	3321.62	3356.11
6	1517.54	1535.91	1554.17	1572.29	1590.28	1608.14	1625.85	1643.41	1660.81	1678.06
7	758.768	767.956	777.083	786.146	795.142	804.069	812.924	821.704	830.406	839.029
8	379.384	383.978	388.542	393.073	397.571	402.035	406.462	410.852	415.203	419.514
9	189.692	191.989	194.271	196.536	198.786	201.017	203.231	205.426	207.602	209.757
10	94.8460	95.9945	97.1354	98.2682	99.3928	100.509	101.615	102.713	103.801	104.879
11	47.4230	47.9973	48.5677	49.1341	49.6964	50.2543	50.8077	51.3565	51.9004	52.4393
12	23.7115	23.9986	24.2838	24.5671	24.8482	25.1272	25.4039	25.6782	25.9502	26.2196
13	11.8557	11.9993	12.1419	12.2835	12.4241	12.5636	12.7019	12.8391	12.9751	13.1098
14	5.92787	5.99966	6.07096	6.14177	6.21205	6.28179	6.35097	6.41956	6.48755	6.55491
15	2.96394	2.99983	3.03548	3.07088	3.10602	3.14089	3.17548	3.20978	3.24377	3.27746
16	1.48197	1.49991	1.51774	1.53544	1.55301	1.57045	1.58774	1.60489	1.62189	1.63873
17	0.740984	0.749957	0.758870	0.767721	0.776506	0.785224	0.793871	0.802445	0.810944	0.819364
18	0.370492	0.374979	0.379435	0.383860	0.388253	0.392612	0.396935	0.401223	0.405472	0.409682
19	0.185246	0.187489	0.189718	0.191930	0.194127	0.196306	0.198468	0.200611	0.202736	0.204841
20	0.0926230	0.0937446	0.0948588	0.0959651	0.0970633	0.0981530	0.0992339	0.100306	0.101368	0.102420
21	0.0463115	0.0468723	0.0474294	0.0479825	0.0485316	0.0490765	0.0496169	0.0501528	0.0506840	0.0512102
22	0.0231558	0.0234362	0.0237147	0.0239913	0.0242658	0.0245382	0.0248085	0.0250764	0.0253420	0.0256051
23	0.0115779	0.0117181	0.0118573	0.0119956	0.0121329	0.0122691	0.0124042	0.0125382	0.0126710	0.0128026
24	0.00578894	0.00585904	0.00592867	0.00599782	0.00606645	0.00613456	0.00620212	0.00626910	0.00633550	0.00640128
										
n	30°	31°	32°	33°	34°	35°	36°	37°	38°	39°
0	108489	109571	110642	111701	112749	113784	114807	115817	116814	117797
1	54244.4	54785.5	55321.0	55850.7	56374.5	56892.1	57403.5	57908.6	58407.0	58898.7
2	27122.2	27392.7	27660.5	27925.3	28187.2	28446.1	28701.8	28954.3	29203.5	29449.4
3	13561.1	13696.4	13830.2	13962.7	14093.6	14223.0	14350.9	14477.1	14601.8	14724.7
4	6780.55	6848.19	6915.12	6981.34	7046.81	7111.52	7175.44	7238.57	7300.88	7362.34
5	3390.27	3424.09	3457.56	3490.67	3523.40	3555.76	3587.72	3619.28	3650.44	3681.17
6	1695.14	1712.05	1728.78	1745.33	1761.70	1777.88	1793.86	1809.64	1825.22	1840.59
7	847.569	856.023	864.390	872.667	880.851	888.939	896.930	904.821	912.609	920.293
8	423.784	428.012	432.195	436.333	440.425	444.470	448.465	452.411	456.305	460.146
9	211.892	214.006	216.098	218.167	220.213	222.235	224.233	226.205	228.152	230.073
10	105.946	107.003	108.049	109.083	110.106	111.117	112.116	113.103	114.076	115.037
11	52.9730	53.5015	54.0244	54.5417	55.0532	55.5587	56.0581	56.5513	57.0381	57.5183
12	26.4865	26.7507	27.0122	27.2708	27.5266	27.7794	28.0291	28.2757	28.5190	28.7592
13	13.2433	13.3754	13.5061	13.6354	13.7633	13.8897	14.0145	14.1378	14.2595	14.3796
14	6.62163	6.68768	6.75305	6.81771	6.88165	6.94484	7.00727	7.06892	7.12976	7.18979
15	3.31081	3.34384	3.37652	3.40886	3.44082	3.47242	3.50363	3.53446	3.56488	3.59489
16	1.65541	1.67192	1.68826	1.70443	1.72041	1.73621	1.75182	1.76723	1.78244	1.79745
17	0.827704	0.835960	0.844131	0.852214	0.860206	0.868105	0.875909	0.883614	0.891220	0.898724
18	0.413852	0.417980	0.422066	0.426107	0.430103	0.434052	0.437954	0.441807	0.445610	0.449362
19	0.206926	0.208990	0.211033	0.213053	0.215051	0.217026	0.218977	0.220904	0.222805	0.224681
20	0.103463	0.104495	0.105516	0.106527	0.107526	0.108513	0.109489	0.110452	0.111403	0.112340
21	0.0517315	0.0522475	0.0527582	0.0532634	0.0537629	0.0542566	0.0547443	0.0552259	0.0557013	0.0561702
22	0.0258657	0.0261238	0.0263791	0.0266317	0.0268814	0.0271283	0.0273721	0.0276130	0.0278506	0.0280851
23	0.0129329	0.0130619	0.0131895	0.0133158	0.0134407	0.0135641	0.0136861	0.0138065	0.0139253	0.0140426
24	0.00646644	0.00653094	0.00659477	0.00665792	0.00672036	0.00678207	0.00684304	0.00690324	0.00696266	0.00702128
Table 4: Tiled polar stereographic zoom-levels scale sets

n	40°	41°	42°	43°	44°	45°	46°	47°	48°	49°
0	118767	119723	120664	121591	122503	123400	124281	125147	125997	126830
1	59383.6	59861.5	60332.2	60795.6	61251.6	61700.0	62140.6	62573.5	62998.3	63415.0
2	29691.8	29930.7	30166.1	30397.8	30625.8	30850.0	31070.3	31286.7	31499.2	31707.5
3	14845.9	14965.4	15083.0	15198.9	15312.9	15425.0	15535.2	15643.4	15749.6	15853.8
4	7422.95	7482.69	7541.52	7599.45	7656.45	7712.50	7767.58	7821.68	7874.79	7926.88
5	3711.48	3741.34	3770.76	3799.73	3828.22	3856.25	3883.79	3910.84	3937.39	3963.44
6	1855.74	1870.67	1885.38	1899.86	1914.11	1928.12	1941.90	1955.42	1968.70	1981.72
7	927.869	935.336	942.691	949.931	957.056	964.062	970.948	977.710	984.349	990.860
8	463.935	467.668	471.345	474.966	478.528	482.031	485.474	488.855	492.174	495.430
9	231.967	233.834	235.673	237.483	239.264	241.016	242.737	244.428	246.087	247.715
10	115.984	116.917	117.836	118.741	119.632	120.508	121.368	122.214	123.044	123.857
11	57.9918	58.4585	58.9182	59.3707	59.8160	60.2539	60.6842	61.1069	61.5218	61.9287
12	28.9959	29.2292	29.4591	29.6854	29.9080	30.1269	30.3421	30.5535	30.7609	30.9644
13	14.4980	14.6146	14.7295	14.8427	14.9540	15.0635	15.1711	15.2767	15.3804	15.4822
14	7.24898	7.30731	7.36477	7.42134	7.47700	7.53174	7.58553	7.63836	7.69022	7.74109
15	3.62449	3.65366	3.68239	3.71067	3.73850	3.76587	3.79276	3.81918	3.84511	3.87055
16	1.81224	1.82683	1.84119	1.85533	1.86925	1.88293	1.89638	1.90959	1.92256	1.93527
17	0.906122	0.913414	0.920596	0.927667	0.934625	0.941467	0.948191	0.954795	0.961278	0.967636
18	0.453061	0.456707	0.460298	0.463834	0.467312	0.470733	0.474096	0.477398	0.480639	0.483818
19	0.226531	0.228353	0.230149	0.231917	0.233656	0.235367	0.237048	0.238699	0.240319	0.241909
20	0.113265	0.114177	0.115075	0.115958	0.116828	0.117683	0.118524	0.119349	0.120160	0.120955
21	0.0566326	0.0570884	0.0575373	0.0579792	0.0584141	0.0588417	0.0592619	0.0596747	0.0600799	0.0604773
22	0.0283163	0.0285442	0.0287686	0.0289896	0.0292070	0.0294208	0.0296310	0.0298374	0.0300399	0.0302386
23	0.0141582	0.0142721	0.0143843	0.0144948	0.0146035	0.0147104	0.0148155	0.0149187	0.0150200	0.0151193
24	0.00707908	0.00713605	0.00719216	0.00724740	0.00730176	0.00735521	0.00740774	0.00745934	0.00750998	0.00755966
										
n	50°	51°	52°	53°	54°	55°	56°	57°	58°	59°
0	127647	128447	129230	129996	130745	131476	132189	132883	133560	134218
1	63823.5	64223.6	64615.2	64998.2	65372.5	65737.9	66094.4	66441.7	66779.9	67108.9
2	31911.8	32111.8	32307.6	32499.1	32686.2	32869.0	33047.2	33220.9	33390.0	33554.4
3	15955.9	16055.9	16153.8	16249.6	16343.1	16434.5	16523.6	16610.4	16695.0	16777.2
4	7977.94	8027.95	8076.90	8124.78	8171.56	8217.24	8261.79	8305.22	8347.49	8388.61
5	3988.97	4013.98	4038.45	4062.39	4085.78	4108.62	4130.90	4152.61	4173.75	4194.30
6	1994.48	2006.99	2019.23	2031.19	2042.89	2054.31	2065.45	2076.30	2086.87	2097.15
7	997.242	1003.49	1009.61	1015.60	1021.45	1027.15	1032.72	1038.15	1043.44	1048.58
8	498.621	501.747	504.806	507.799	510.723	513.577	516.362	519.076	521.718	524.288
9	249.311	250.873	252.403	253.899	255.361	256.789	258.181	259.538	260.859	262.144
10	124.655	125.437	126.202	126.950	127.681	128.394	129.091	129.769	130.430	131.072
11	62.3276	62.7184	63.1008	63.4748	63.8403	64.1972	64.5453	64.8845	65.2148	65.5360
12	31.1638	31.3592	31.5504	31.7374	31.9202	32.0986	32.2726	32.4423	32.6074	32.7680
13	15.5819	15.6796	15.7752	15.8687	15.9601	16.0493	16.1363	16.2211	16.3037	16.3840
14	7.79095	7.83980	7.88760	7.93435	7.98004	8.02465	8.06816	8.11056	8.15185	8.19200
15	3.89548	3.91990	3.94380	3.96718	3.99002	4.01232	4.03408	4.05528	4.07592	4.09600
16	1.94774	1.95995	1.97190	1.98359	1.99501	2.00616	2.01704	2.02764	2.03796	2.04800
17	0.973869	0.979974	0.985950	0.991794	0.997505	1.00308	1.00852	1.01382	1.01898	1.02400
18	0.486935	0.489987	0.492975	0.495897	0.498752	0.501540	0.504260	0.506910	0.509491	0.512000
19	0.243467	0.244994	0.246487	0.247949	0.249376	0.250770	0.252130	0.253455	0.254745	0.256000
20	0.121734	0.122497	0.123244	0.123974	0.124688	0.125385	0.126065	0.126728	0.127373	0.128000
21	0.0608668	0.0612484	0.0616219	0.0619871	0.0623441	0.0626925	0.0630325	0.0633638	0.0636863	0.0640000
22	0.0304334	0.0306242	0.0308109	0.0309936	0.0311720	0.0313463	0.0315162	0.0316819	0.0318432	0.0320000
23	0.0152167	0.0153121	0.0154055	0.0154968	0.0155860	0.0156731	0.0157581	0.0158409	0.0159216	0.0160000
24	0.00760835	0.00765605	0.00770273	0.00774839	0.00779301	0.00783657	0.00787906	0.00792047	0.00796079	0.00800000
Table 4: Tiled polar stereographic zoom-levels scale sets

n	60°	61°	62°	63°	64°	65°	66°	67°	68°	69°
0	134857	135477	136078	136659	137221	137764	138286	138789	139271	139733
1	67428.4	67738.4	68038.9	68329.7	68610.7	68881.9	69143.1	69394.3	69635.4	69866.3
2	33714.2	33869.2	34019.5	34164.8	34305.4	34440.9	34571.5	34697.1	34817.7	34933.1
3	16857.1	16934.6	17009.7	17082.4	17152.7	17220.5	17285.8	17348.6	17408.8	17466.6
4	8428.55	8467.31	8504.86	8541.21	8576.34	8610.23	8642.89	8674.29	8704.42	8733.29
5	4214.27	4233.65	4252.43	4270.61	4288.17	4305.12	4321.44	4337.14	4352.21	4366.64
6	2107.14	2116.83	2126.22	2135.30	2144.08	2152.56	2160.72	2168.57	2176.11	2183.32
7	1053.57	1058.41	1063.11	1067.65	1072.04	1076.28	1080.36	1084.29	1088.05	1091.66
8	526.784	529.207	531.554	533.826	536.021	538.140	540.180	542.143	544.026	545.830
9	263.392	264.603	265.777	266.913	268.011	269.070	270.090	271.071	272.013	272.915
10	131.696	132.302	132.888	133.456	134.005	134.535	135.045	135.536	136.007	136.458
11	65.8480	66.1508	66.4442	66.7282	67.0026	67.2674	67.5225	67.7679	68.0033	68.2288
12	32.9240	33.0754	33.2221	33.3641	33.5013	33.6337	33.7613	33.8839	34.0016	34.1144
13	16.4620	16.5377	16.6111	16.6821	16.7507	16.8169	16.8806	16.9420	17.0008	17.0572
14	8.23101	8.26885	8.30553	8.34103	8.37533	8.40843	8.44032	8.47098	8.50041	8.52860
15	4.11550	4.13443	4.15277	4.17051	4.18767	4.20422	4.22016	4.23549	4.25021	4.26430
16	2.05775	2.06721	2.07638	2.08526	2.09383	2.10211	2.11008	2.11775	2.12510	2.13215
17	1.02888	1.03361	1.03819	1.04263	1.04692	1.05105	1.05504	1.05887	1.06255	1.06608
18	0.514438	0.516803	0.519096	0.521314	0.523458	0.525527	0.527520	0.529436	0.531276	0.533038
19	0.257219	0.258402	0.259548	0.260657	0.261729	0.262763	0.263760	0.264718	0.265638	0.266519
20	0.128609	0.129201	0.129774	0.130329	0.130865	0.131382	0.131880	0.132359	0.132819	0.133259
21	0.0643047	0.0646004	0.0648870	0.0651643	0.0654323	0.0656909	0.0659400	0.0661795	0.0664095	0.0666297
22	0.0321524	0.0323002	0.0324435	0.0325821	0.0327161	0.0328454	0.0329700	0.0330898	0.0332047	0.0333148
23	0.0160762	0.0161501	0.0162217	0.0162911	0.0163581	0.0164227	0.0164850	0.0165449	0.0166024	0.0166574
24	0.00803809	0.00807505	0.00811087	0.00814553	0.00817903	0.00821136	0.00824250	0.00827244	0.00830118	0.00832871
										
n	70°	71°	72°	73°	74°	75°	76°	77°	78°	79°
0	140174	140595	140995	141374	141732	142069	142384	142679	142951	143203
1	70087.0	70297.3	70497.3	70686.8	70865.8	71034.3	71192.1	71339.3	71475.7	71601.4
2	35043.5	35148.7	35248.6	35343.4	35432.9	35517.1	35596.0	35669.6	35737.9	35800.7
3	17521.7	17574.3	17624.3	17671.7	17716.5	17758.6	17798.0	17834.8	17868.9	17900.3
4	8760.87	8787.16	8812.16	8835.85	8858.23	8879.28	8899.01	8917.41	8934.46	8950.17
5	4380.44	4393.58	4406.08	4417.93	4429.11	4439.64	4449.51	4458.70	4467.23	4475.09
6	2190.22	2196.79	2203.04	2208.96	2214.56	2219.82	2224.75	2229.35	2233.62	2237.54
7	1095.11	1098.40	1101.52	1104.48	1107.28	1109.91	1112.38	1114.68	1116.81	1118.77
8	547.554	549.198	550.760	552.241	553.639	554.955	556.188	557.338	558.404	559.386
9	273.777	274.599	275.380	276.120	276.820	277.478	278.094	278.669	279.202	279.693
10	136.889	137.299	137.690	138.060	138.410	138.739	139.047	139.334	139.601	139.846
11	68.4443	68.6497	68.8450	69.0301	69.2049	69.3694	69.5235	69.6672	69.8005	69.9232
12	34.2222	34.3249	34.4225	34.5150	34.6024	34.6847	34.7618	34.8336	34.9002	34.9616
13	17.1111	17.1624	17.2113	17.2575	17.3012	17.3423	17.3809	17.4168	17.4501	17.4808
14	8.55554	8.58122	8.60563	8.62876	8.65061	8.67117	8.69044	8.70840	8.72506	8.74040
15	4.27777	4.29061	4.30281	4.31438	4.32531	4.33559	4.34522	4.35420	4.36253	4.37020
16	2.13888	2.14530	2.15141	2.15719	2.16265	2.16779	2.17261	2.17710	2.18127	2.18510
17	1.06944	1.07265	1.07570	1.07860	1.08133	1.08390	1.08631	1.08855	1.09063	1.09255
18	0.534721	0.536326	0.537852	0.539298	0.540663	0.541948	0.543153	0.544275	0.545316	0.546275
19	0.267361	0.268163	0.268926	0.269649	0.270332	0.270974	0.271576	0.272138	0.272658	0.273138
20	0.133680	0.134081	0.134463	0.134824	0.135166	0.135487	0.135788	0.136069	0.136329	0.136569
21	0.0668401	0.0670407	0.0672315	0.0674122	0.0675829	0.0677436	0.0678941	0.0680344	0.0681645	0.0682844
22	0.0334201	0.0335204	0.0336157	0.0337061	0.0337915	0.0338718	0.0339470	0.0340172	0.0340823	0.0341422
23	0.0167100	0.0167602	0.0168079	0.0168530	0.0168957	0.0169359	0.0169735	0.0170086	0.0170411	0.0170711
24	0.00835502	0.00838009	0.00840393	0.00842652	0.00844786	0.00846794	0.00848676	0.00850430	0.00852057	0.00853555
Table 4: Tiled polar stereographic zoom-levels scale sets

n	80°	81°	82°	83°	84°	85°
0	143433	143641	143827	143992	144134	144255
1	71716.3	71820.4	71913.6	71995.9	72067.2	72127.7
2	35858.1	35910.2	35956.8	35997.9	36033.6	36063.8
3	17929.1	17955.1	17978.4	17999.0	18016.8	18031.9
4	8964.54	8977.54	8989.19	8999.48	9008.41	9015.96
5	4482.27	4488.77	4494.60	4499.74	4504.20	4507.98
6	2241.13	2244.39	2247.30	2249.87	2252.10	2253.99
7	1120.57	1122.19	1123.65	1124.94	1126.05	1126.99
8	560.284	561.097	561.825	562.468	563.025	563.497
9	280.142	280.548	280.912	281.234	281.513	281.749
10	140.071	140.274	140.456	140.617	140.756	140.874
11	70.0354	70.1371	70.2281	70.3085	70.3782	70.4372
12	35.0177	35.0685	35.1140	35.1542	35.1891	35.2186
13	17.5089	17.5343	17.5570	17.5771	17.5945	17.6093
14	8.75443	8.76713	8.77851	8.78856	8.79727	8.80465
15	4.37722	4.38357	4.38926	4.39428	4.39864	4.40232
16	2.18861	2.19178	2.19463	2.19714	2.19932	2.20116
17	1.09430	1.09589	1.09731	1.09857	1.09966	1.10058
18	0.547152	0.547946	0.548657	0.549285	0.549829	0.550291
19	0.273576	0.273973	0.274328	0.274642	0.274915	0.275145
20	0.136788	0.136986	0.137164	0.137321	0.137457	0.137573
21	0.0683940	0.0684932	0.0685821	0.0686606	0.0687287	0.0687863
22	0.0341970	0.0342466	0.0342911	0.0343303	0.0343643	0.0343932
23	0.0170985	0.0171233	0.0171455	0.0171652	0.0171822	0.0171966
24	0.00854925	0.00856165	0.00857276	0.00858258	0.00859108	0.00859829
						
n	86°	87°	88°	89°	90°	
0	144354	144431	144486	144519	144530	
1	72177.2	72215.7	72243.2	72259.7	72265.2	
2	36088.6	36107.8	36121.6	36129.8	36132.6	
3	18044.3	18053.9	18060.8	18064.9	18066.3	
4	9022.14	9026.96	9030.40	9032.46	9033.15	
5	4511.07	4513.48	4515.20	4516.23	4516.57	
6	2255.54	2256.74	2257.60	2258.11	2258.29	
7	1127.77	1128.37	1128.80	1129.06	1129.14	
8	563.884	564.185	564.400	564.529	564.572	
9	281.942	282.092	282.200	282.264	282.286	
10	140.971	141.046	141.100	141.132	141.143	
11	70.4855	70.5231	70.5500	70.5661	70.5715	
12	35.2428	35.2615	35.2750	35.2830	35.2857	
13	17.6214	17.6308	17.6375	17.6415	17.6429	
14	8.81069	8.81539	8.81875	8.82076	8.82143	
15	4.40534	4.40769	4.40937	4.41038	4.41072	
16	2.20267	2.20385	2.20469	2.20519	2.20536	
17	1.10134	1.10192	1.10234	1.10260	1.10268	
18	0.550668	0.550962	0.551172	0.551298	0.551340	
19	0.275334	0.275481	0.275586	0.275649	0.275670	
20	0.137667	0.137740	0.137793	0.137824	0.137835	
21	0.0688335	0.0688702	0.0688964	0.0689122	0.0689174	
22	0.0344167	0.0344351	0.0344482	0.0344561	0.0344587	
23	0.0172084	0.0172176	0.0172241	0.0172280	0.0172294	
24	0.00860419	0.00860878	0.00861206	0.00861402	0.00861468	

