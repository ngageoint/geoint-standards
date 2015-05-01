<pre>

	NGA.STND.0019_2.0
	2012-04-05









<b><i><h1 style="text-align:center" style="font-family:verdana" >NGA STANDARDIZATION DOCUMENT</h1></i></b>


Time-Space-Position Information
(TSPI)
(2012-04-05)






Version 2.0






 
| |#####DISTRIBUTION STATEMENT A:   Approved for public release; distribution is unlimited.| | 
 




---
#####NATIONAL CENTER FOR GEOSPATIAL INTELLIGENCE STANDARDS
---
 
#####Table of Contents
1.	Introduction ..............................................................1  
  1.1.	Spatiotemporal ............................................................1  
  1.2.	TSPI Terminology...........................................................1  
  1.3.	TSPI Exchange..............................................................2  
  1.4.	TSPI-related XML-based Standards...........................................2  
  1.5.	SCOTS Software.............................................................4  
  1.6.	Data Mediation.............................................................4  
  1.7.	Space and Place............................................................4  
  1.8.	TSPI Capabilities..........................................................5  
  1.9.	TSPI Schema Components.....................................................6  
  1.10.	Specification Overview.....................................................7  
2.	Conformance................................................................8  
3.	References.................................................................8  
  3.1.	Normative..................................................................8  
  3.2.	Informative................................................................9  
4.	Terms, Definitions and Acronyms...........................................10  
  4.1.	Terms and Definitions.....................................................10  
  4.2.	Acronyms..................................................................13      
5.	Where – Spatial Position..................................................15    
	5.1.	Introduction......................................................15  
	5.2.	Abstract Position.................................................15  
	5.3.	Position Infrastructure...........................................16  
		5.3.1.	Coordinate Reference Systems..............................16  
		5.3.2.	Earth-referenced Coordinate Reference Systems.............20  
		5.3.3.	Earth-referenced Position Presentation....................30  
		5.3.4.	Earth-referenced Elevation, Height, Altitude and Depth....42  
		5.3.5.	Coordinate Resolution.....................................43  
		5.3.6.	Positional Uncertainty....................................47  
	5.4.	Spatial Extent....................................................48  
		5.4.1.	Introduction..............................................48  
		5.4.2.	TSPI Point Position.......................................49  
		5.4.3.	TSPI Line String..........................................52  
		5.4.4	TSPI Circle...............................................54  
		5.4.5	TSPI Ellipse..............................................57  
		5.4.6	TSPI Polygon	59    
		5.4.7	TSPI Simple Polygon	63  
		5.4.8	TSPI Simple Rectangle	65  
		5.4.9	TSPI Envelope	68  
		5.4.10	TSPI Circular Surface	70  
5.4.11	TSPI Elliptical Surface	72  
5.5	Spatial Relations	74  
5.5.1	Measured Direction	74  
5.5.2	Cardinal Direction	74  
5.5.3	Topology	75  
5.6	Spatial Measures	75  
5.7	Spatial Change	76  
5.8	Spatial Position Extension	76  
5.8.1	Introduction	76  
5.8.2	CRS-restricted Point (WGS84E_3D)	77  
6	 Where – Geographic Location	79  
 6.1	 Introduction	79  
 6.2	 Abstract Geographically-identified Location	79  
 6.3	 Geographic Identifiers	80  
 6.4	 Geographic Location Extension	81  
   6.4.1 Geographic Location (GEOLOC) Identifiers	81  
7	 Where – Physical Address	81  
 7.1	 Introduction	81  
 7.2	 Abstract Address	82  
 7.3	 Thoroughfare, Landmark, and Postal Addressing	82  
   7.3.1 Address Components	82  
   7.3.2 Address Types	83  
 7.4	 Physical Address Extension	84  
8	 When – Temporal Position	85  
 8.1	 Overview	85  
 8.2	 Temporal Reference Systems	85  
 8.3	 Time Zones	86  
  8.3.1	 Introduction	86  
  8.3.2	 Local Time	87  
  8.3.3	 Local Time and UTC of Day	88  
  8.3.4	 Daylight Savings Time	88  
 8.4	 Time-related GML Restrictions	88  
 8.5	 Temporal Position	89  
  8.5.1	 Position Encoding	89  
  8.5.2	 Exact Temporal Position	92  
  8.5.3	 Inexact Temporal Position	93  
 8.6	 Temporal Extent	93  
  8.6.1	 Exact Temporal Extent	93  
  8.6.2	 Inexact Temporal Extent	94  
  8.6.3	 Reduced Temporal Resolution	94  
 8.7	Temporal Duration and Interval	95  
  8.7.1	Introduction	95  
8.7.2	Temporal Duration	95  
8.7.3	Temporal Interval	96  
8.7.4	Encoding	96  
8.8	Temporal Uncertainty	96    

Annex A – Conventions (Normative)	98  
A.1	Introduction	98  
A.2	Naming and Design Rules from GML	98
A.2.1	Introduction	98
A.2.2	Lexical Conventions	98  
A.2.3	XML Schema Conventions	98  
A.3	Referencing GML	99  
A.3.1	GPAS Governance Namespace	99  
A.3.2	Referencing GPAS Schemas	99  
A.3.3	Modifications to Publicly Available Schemas	100  
A.3.4	XML Schema Namespace Identifiers	101  
A.4	Referencing TSPI	102  
A.4.1	GSIP Governance Namespace	102  
A.4.2	TSPI XML Namespace	102  
A.5	Information Resources	103  
A.5.1	Introduction	103  
A.5.2	Coordinate Reference System Resources	103  
A.5.3	Code List Resources	103  
A.5.3.1	Fixed Enumerations	103  
A.5.3.2	Flexible Enumerations	104  
A.5.3.3	Managed Code Lists	106  
A.5.3.4	Code List Item References	106  
A.5.4	Physical Quantity and Unit of Measure Resources	106  
A.5.4.1	Introduction	106  
A.5.4.2	Radix Point Presentation	107  
A.5.4.3	SI Prefixes	107  
A.5.4.4	Measures and Units of Measure	107  
A.5.4.5	Unit of Measure Dictionaries	108  
A.5.4.6	Unit of Measure References	110  
A.5.5	Data Quality Measure Resources	110  
A.5.6	Void Values	111  
A.6	Data Validation	112  
Annex B – Test Suite (Normative)	114  
B.1	Introduction	114  
B.2	Validating XML Processor	114  
B.3	Schematron Validator	114  
B.4	Conformance	115  
B.4.1	Introduction	115  
B.4.2	Schema Subsetting	116  
B.4.3	Instance Document	117  
B.4.4	Document Generation	117  
B.4.5	Document Consumption	118  
Annex C – Geodetic Datums (Informative)	119  
C.1	Coordinate Reference System Ambiguity	119  
C.2	CRS Referencing	119  
C.3	Registered CRS	119  
C.4	Alternate and Legacy Datums	119  
Annex D – GML Profiles and Application Schemas (Informative)	127  
D.1	Geography Markup Language	127  
D.2	GML Data Instances	127  
D.3	GML Profiles	127  
Annex E – Extension Procedure (Informative)	129  
E.1	Introduction	129  
E.2	Substitution Group Extension	129  
E.3	Code List Extension	130  

Table of Figures  
Figure 1 – WGS84E_2D CRS Specification	20  
Figure 2 – TSPI Horizontal Presentation Type	32  
Figure 3 – tspi-core:SexagesimalPresentationType	36  
Figure 4 – tspi-core:GridMetrePresentationType	37  
Figure 5 – tspi-core:ZoneMetrePresentationType	38  
Figure 6 – tspi-core:QuadranglePresentationType	39  
Figure 7 – tspi-core:NumericBitPresentationType	41  
Figure 8 – TSPI Vertical Presentation Type..............................................................42  
Figure 9 – TSPI Position Presentation Model Group.......................................................42  
Figure 10 – Extending the GML Measure Type with Vertical Reference Information..........................43  
Figure 11 – TSPI Position Resolution Model Group........................................................47  
Figure 12 – Examples of Point Positions Specified using GML.............................................50  
Figure 13 – Extending the GML Point to include Resolution and Presentation Information..................50  
Figure 14 – Example of a Point Position with Sexagesimal Presentation...................................52  
Figure 15 – Example of a Line String Specified using GML................................................52  
Figure 16 – Extending the gml:LineString to include Resolution and Presentation Information.............53  
Figure 17 – Example of a LineString Position with Grid-Metre Presentation...............................54  
Figure 18 – Example of a Simple Circle by Center Point Position Specified using GML.....................56  
Figure 19 – Extending the gml:Circle to include Resolution and Presentation Information.................56  
Figure 20 – Example of a Circle Position with Numeric-Bit Presentation..................................57  
Figure 21 – The tspi:Ellipse (including Resolution and Presentation Information)........................57  
Figure 22 – Example of a Ellipse Position with Numeric-Bit Presentation.................................59  
Figure 23 – Example of a Polygon Specified using GML....................................................60  
Figure 24 – Extending the gml:Polygon to include Resolution and Presentation Information................61  
Figure 25 – Example of a Polygon Position with Zone-Metre Presentation..................................62  
Figure 26 – Examples of a Simple Polygon Specified using GML 3.3........................................63  
Figure 27 – Extending the gmlce:SimplePolygon to include Resolution and Presentation Information........64  
Figure 28 – Example of a Simple Polygon Position with Zone-Metre Presentation...........................65  
Figure 29 – Examples of a Simple Rectangle Specified using GML 3.3......................................66  
Figure 30 – Extending the gmlce:SimpleRectangle to include Resolution and Presentation Information......66  
Figure 31 – Example of a Simple Rectangle Position with Zone-Metre Presentation.........................68  
Figure 32 – Replacing the gml:Envelope (to include Resolution and Presentation Information).............69  
Figure 33 – Example of an Envelope Position with Quadrangle Presentation................................70  
Figure 34 – The tspi:CircularSurface (including Resolution and Presentation Information)................71  
Figure 35 – Example of a CircularSurface Position with Numeric-Bit Presentation.........................72  
Figure 36 – The tspi:EllipticalSurface (including Resolution and Presentation Information)..............72  
Figure 37 – Example of a Elliptical Surface Position with Numeric-Bit Presentation......................74  
Figure 38 – Extending the GML Measure Type with an Angle Reference Datum................................74  
Figure 39 – Cardinal Directions with an Angle Reference Datum...........................................75  
Figure 40 – Example Length Type Schema Fragment	75  
Figure 41 – Specification of tspi-ext:Point_WGS84E_3D and its supporting types	79  
Figure 42 – Specification of si:SI_LocationInstanceType and supporting types	80  
Figure 43 – Specification of si:SI_LocationType	81  
Figure 44 – Example Temporal Extent as a Closed Period	94  
Figure 45 – Example Temporal Extent as an Open Period	94  
Figure 46 – Example Import of the GPAS-registered GML Schema	100  
Figure 47 – Example schemaLocation Usage of the GPAS-registered GML Schema	100  
Figure 48 – Example Change of Absolute to Relative URL for an Imported Schema	101  
Figure 49 – Example Change of URL Reference to a Local Relative URL	101  
Figure 50 – Example Codelist Instance Document Fragment	104  
Figure 51 – Example Enumeration Instance Document Fragment	105  
Figure 52 – Example Flexible Enumeration Schema Fragment	105  
Figure 53 – Example GML Units of Measure Dictionary	110  
Figure 54 – Example Inclusion of a Schematron Pattern Element in an XSD	113  
Figure 55 – Relating the GML Standard to a GML-based Application Schema and a Data Instance	127  
Figure 56 – Relating the GML Standard to a GML Profile and a GML-based Application Schema	128  

Table of Tables  
Table 1 – Normative References	8  
Table 2 – Informative References	9  
Table 3 – Definitions Applicable to this Specification	10  
Table 4 – Legal Single Coordinate Sexagesimal Encodings	33  
Table 5 – Legal Grid-Metre Encodings	36  
Table 6 – Legal Zone-Metre Encodings	38  
Table 7 – Legal Quadrangle Encodings	39  
Table 8 – Ellipsoidal Distance	44  
Table 9 – Local Time and Standard Winter Time Zones	87  
Table 10 – Supported Date/Time Representations	91  
Table 11 – GPAS Document Organization	99  
Table 12 – Example GPAS Schema Locations	100  
Table 13 – Unit of Measure Prefixes	107  
Table 14 – USMTF GEODETIC DATUM Domain Values	120  
 


CHANGE LOG  
Version	Date	Description	Author  
2.0	4/05/2012	Initial version	ASFE Chair  
			
			
			


 
1	Introduction
1.1	Spatiotemporal Data
Spatiotemporal data is critical to missions throughout the U.S. Department of Defense (DoD) and Intelligence Community (IC). Spatiotemporal data includes the specification of the spatial, temporal, and accompanying quality assessment, characteristics of entities (e.g., equipment, combatants and targets).
Spatial information includes position, extent (shape), size, orientation, and rates of change in these characteristics. Unambiguous expression of the values of these characteristics requires the identification of a robust coordinate reference system, such as those associated with the World Geodetic System 1984 (WGS 84), and the ability to specify the values of such characteristics with respect to that coordinate reference system. Spatial information also includes identifiers based on geographic place-names, physical addresses, and other systems in which a spatial reference in the form of a label or code is used to identifiy a location that may then be more rigorously tied to a position.
Temporal information includes position (instant), extent (duration), and periodic recurrence characteristics. Unambiguous expression of the values of these characteristics requires the identification of a robust temporal reference system, such as Coordinated Universal Time (UTC), and the ability to specify the values of such characteristics with respect to that temporal reference system. 
Quality assessment information includes the precision of data values as well as quantitative and qualitative estimates of the accuracy and/or uncertainty of spatial and temporal characteristics.
Spatiotemporal data in the DoD/IC may be generated by a variety of mechanisms. These include by being: sensed remotely, predicted by computational algorithms, or directly determined and reported using on-board equipment containing a Global Positioning System (GPS) receiver and Inertial Measurement Unit (IMU). For convenience this specification adopts the terminology of the (latter) instrumentation community by referring to spatiotemporal data as Time-Space-Position Information (TSPI).
Unambiguous specification of TSPI is central to Geospatial Intelligence (GEOINT) and the functioning of the National System for Geospatial Intelligence (NSG). The National Geospatial-Intelligence Agency (NGA) is the Functional Manager of the NSG, and as such is a key stakeholder in ensuring that TSPI is well-specified – particularly as regards precise spatiotemporal positioning for the purposes of targeting.
It is the case that not all communications of TSPI data, today, include explicit characterization of their spatiotemporal reference system(s). Even when they do, it is sometimes the case that participants to the TSPI exchange do not completely understand how that spatiotemporal reference system relates to the “real Earth” (e.g., the relationship between Military Grid Reference System (MGRS) “flat” coordinates and geodetic coordinates on a “curved Earth”). As the promulgating Agency for MGRS and WGS 84, NGA has a vested interest in ensuring (to the maximum extent possible) that these standards are correctly adopted and supported in DoD/IC systems across the NSG.
1.2	TSPI Terminology
The NSG includes many communities of practice, each having developed and employed “local variations” in TSPI-related terminology. These variations can be an impediment to clear and unambiguous communication of TSPI. Athough the purpose of this TSPI standard is to provide consistent support to all of these communities, it specifically emphasizes two:
•	Warfighters, intelligence analysts, and their DoD/IC software applications; and
•	Commercial Off-The-Shelf (COTS) software based on Open Geospatial Consortium (OGC) and International Organization for Standardization (ISO) 19100-series standards – that warfighters and intelligence analysts may employ in their applications.
In consequence , where there are terminological differences it employs a consistent set of terminology that maximally aligns with the expectations and practices of these two communities wherever possible. In particular, as regards terminology this specification conforms to:
•	CJCSI 3900.01C, Position (Point and Area) Reference Procedures, 30 June 2007, adopting and extending from its terminology wherever appropriate; and
•	ISO 19111:2007, Geographic information – Spatial referencing by coordinates, which specifies a conceptual schema and associated terminology for spatial references that is used throughout OGC and ISO 19100-series standards.
Other terminological choices are identified as aliases, where appropriate, and footnoted accordingly.
1.3	TSPI Exchange
TSPI, especially as generated at high rates by onboard instrumentation, may be communicated using bit-oriented protocols (e.g., Link-16 or Variable Message Format (VMF)) intended only for machine-to-machine interactions (and for use in limited bandwidth environments). However, in many cases TSPI is exchanged at low rates using character-oriented protocols such as U.S. Message Text Format (USMTF) or Variable Message Format – Extensible Markup Language (VMF-XML). In these latter cases the formatting of the TSPI content is often determined more by human-factors considerations than encoding-efficiency, and the end-to-end exchange is generally human-to-human and less “encoding efficient”. A wide variety of capabilities and missions may be supported by character-oriented protocols (for example: Command,  Control, and Intelligence).
To better understand the distinction being drawn here, consider the encoding of a single spatial coordinate value. In a bit-oriented environment a coordinate value could be efficiently encoded as a double precision floating point number (8 octets). In a character-oriented environment it may instead be encoded as a series of characters that are understood to denote a series of values in the form of “DDDMMSSH” where the initial three Dee characters indicate a three digit integer number of arc-degrees, the two following Em characters indicate a two digit integer number of arc-minutes, the subsequent two Ess characters indicate a two digit integer number of arc-seconds, the final character indicates the hemisphere, and the numeric precision of the result is “to the nearest arc-second”. This character-oriented encoding is not particularly space-efficient, nor especially precise, and not directly usable in computation; however, it is in a format that is well-understood by warfighters. This format is, in effect, a “unique presentation” of the intended mathematically rigorous double precision floating point number.
As the DoD moves towards a net-centric and data-centric paradigm many systems are being enhanced to use Extensible Markup Language (XML) as the unifying and interoperable basis for information exchange (the case of VMF-XML is an exemplar of this trend). However, each system has tended to develop a unique approach to specifying TSPI using XML – sometimes for the purposes of maximizing backwards-compatibility, and at other times in order to meet evolving data exchange objectives. Standardizing the exchange of TSPI through the promulgation of a well-documented and unambiguous XML schema would promote, and then enable, interoperability between many disparate systems in the DoD/IC. Accompanying implementation guidance would help ensure that such an XML schema was correctly and consistently employed by systems developers and operators.
While it is desirable to simply specify a single approach to specifying each “item type” of TSPI, the reality of system acquisition and upgrade processes will result in a non-uniform rate of adoption across the DoD/IC of such a “unitary” schema. It is therefore necessary that any TSPI specification should support a graceful transition from legacy and current operational practices to the objective capability. Thus, for a specific “item type” of TSPI it may be appropriate to specify both a mandatory representation and one or more optional alternative representations for use during the period of system(s) transition. This optionality may be made conditional (or mandatory) in the context of specific community data exchanges.
1.4	TSPI-related XML-based Standards
The World Wide Web Consortium (W3C) specifications XML Schema Definition Language (XSD) 1.1 – Part 1: Structures and Part 2: Datatypes are the basis for the development of all XML schemas. While they are not “spatially aware”, they do specify a set of basic datatypes for time that are tied to International Organization for Standardization (ISO) 8601:1988 Representations of dates and times. From this common starting point different limited- or non-interoperable XML-based solutions to the TSPI exchange problem have been developed.
ISO 19136:2007 Geographic information – Geography Markup Language (GML)  builds upon the infrastructure of XSD both a more robust XML-based model for temporal representation (and reasoning) and a new XML-based model for spatial representation. ISO 19136 draws upon the conceptual schemas of multiple related standards, specifically including ISO 19107:2003 Geographic information – Spatial schema, ISO 19108:2002 Geographic information – Temporal schema, and ISO 19111:2007, Geographic information – Spatial referencing by coordinates, resulting in an internationally recognized and commercially employed consistent XML-based encoding of these conceptual schemas.
OGC® Geography Markup Language (GML) - Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1) extends ISO 19136:2007 to specify additional geometric representations, compact geometry encodings, and enhancements in basic types and XML encoding rules.
ISO 19112:2003 Geographic information – Spatial referencing by geographic identifiers specifies a conceptual schema for spatial references based on geographic identifiers – the relationship to a location that is determined by a geographic feature or features (for example a named country, administrative subdivision, town, property, or river basin). It establishes a general model for spatial referencing using geographic identifiers, defines the components of a spatial reference system and defines the essential components of a gazetteer (a directory of geographic identifiers describing location instances). Its conceptual schema enables consistent application of Web Feature Services (WFS) with gazetteer data, which is further elaborated by draft OGC Best Practices Document: Gazetteer Service - Application Profile of the Web Feature Service Implementation Specification, OGC 11-122r1, Version: 0.9.4.
ISO 19136:2007, ISO 19107:2003, ISO 19108:2002, ISO 19111:2007 and ISO 19112:2003 have all been identified as mandatory standards for use is systems-acquisition in both the DoD Information Technology Standards Registry (DISR) and the Intelligence Community Standards Registry (ICSR).
ISO 6709:2008 Standard representation of geographic point location by coordinates specifies the representation of coordinates, including latitude and longitude, to be used in data interchange. It additionally specifies the representation of height and depth that may be associated with horizontal coordinates. The representation of coordinates includes units of measure and coordinate order.
ISO 6709:2008 supports point location representation using XML and, recognizing the need for compatibility with the previous version of the standard (ISO 6709:1983), it allows for the use of a single alpha-numeric string to describe point locations. In particular it allows for the use of sexagesimal notations: degrees, minutes and decimal minutes or degrees, minutes, seconds and decimal seconds. For computer data interchange of latitude and longitude coordinates, ISO 6709:2008 recommends that decimal degrees be used.
Federal Geographic Data Committee (FGDC) United States Thoroughfare, Landmark, and Postal Address Data Standard, FGDC-STD-016-2011, February 2011, recognizes that physical addresses are the location identifiers most widely used by the public and by state and local government, being critical for emergency response, homeland security, and disaster management. In lieu of a recognized international standard for addressing , FGDC-STC-016-2011 specifies a comprehensive U.S. address data standard that meets a wide range of addressing requirements: postal delivery and census enumeration, local government administration and intergovernmental cooperation, emergency dispatch, the creation and administration of master address repositories by local address authorities, and the aggregation of local records into larger regional, state, and national address databases.
Internet Engineering Task Force (IETF) RFC 5870 – A Uniform Resource Identifier for Geographic Locations (’geo’ URI), specifies a Uniform Resource Identifier (URI) for geographic locations using the ’geo’ scheme name. A ’geo’ URI identifies a physical location in a two- or three-dimensional coordinate reference system in a compact, simple, human-readable, and protocol independent way. A mechanism for Coordinate Reference System identification is specified; the default coordinate reference system used is WGS 84. Location uncertainty may be expressed, and recommendations are made for mapping ‘geo’ URIs to/from GML Point, Circle and Sphere – the latter two mappings being based on an uncertainty parameter that is present and nonzero.
ISO 8601:2004 Data elements and interchange formats – Information interchange – Representation of dates and times specifies numeric representations of information regarding date and time of day as well as formats of these numeric representations.
ISO 19106:2004 Geographic information – Profiles specifies two classes of conformance when developing a profile of a base standard. A Class 1 profile is a strict subset of the base standard, while a Class 2 profile includes non-conflicting extensions of the base standard.
Numerous programs (e.g., the DoD Discovery Metadata Specification (DDMS) and the Universal Core (UCore)) have developed (generally) Class 1 Profiles of GML as part of their schema development activities. However, each has done so in a unique manner sufficient only to meet their limited program-specific objectives. The proliferation of program-specific Class 1 Profiles of GML as regards time-space-position information does not meet DoD/IC-wide net- and data-centric objectives.
Few, if any, of these program-specific Profiles of GML include Class 2 TSPI-related extensions that are necessary to address TSPI requirements that are not directly addressed by GML itself.
1.5	SCOTS Software
It is the intent of DoD/IC leadership that investments in new information technologies maximally leverage Commercial Off-The-Shelf (COTS) capabilities whenever doing so does not adversely affect mission effectiveness. Government-unique software development should, whenever possible, be limited to government-unique functionality. When procuring, and possibly further adapting, COTS capabilities it is to the benefit of the government to procure capabilities that adhere to open standards. Procurement of standards-based COTS (SCOTS) aids in ensuring cross-program interoperability and reduces the risks associated with proprietary interfaces and concomitant vendor lock-in.
As the Functional Manager of the NSG, the Director of NGA has specified that NSG systems shall, where applicable, employ standards developed by the Open Geospatial Consortium (OGC) that facilitate net-centric data exchange using service-oriented interfaces. These include the Web Feature Service (WFS) and other GML-based web services. These standards have a wide (and growing) variety of SCOTS implementations. Non-NSG systems can similarly benefit from this commercial marketplace and “riding the wave” of commercial investment and technology evolution. But they can only do so if they understand and employ ISO 19136:2007 (GML) in a consistent and rigorous manner.
1.6	Data Mediation
The DoD data- and net-centric tenets include the concept that data mediation may be employed to bridge between the information exchange schemas of different Communities of Interest (COI). Where both COIs share the same semantics, but differ only in the syntactic structure of their schemas it is possible to dynamically restructure instance data to facilitate cross-community information exchange.
For XML-based schemas and data instances, the Extensible Stylesheet Language Transformations (XSLT) technology may be used to facilitate this data restructuring once a semantic-preserving structural mapping has been specified. Achieving the necessary semantic pre-requisite is facilitated by sharing common schema data components where those data components “mean the same thing” in both communities.
ISO 19136:2007 (GML) specifies such a set of common data components for use in building community-specific schemas where spatiotemporal information is involved. The adoption of a common Profile of GML by multiple COIs, and then its consistent and correct employment in community-specific schemas, can facilitate TSPI interoperability despite other types of community differences. 
1.7	Space and Place
Spatial information includes position, extent (shape), size, orientation, and rates of change in these characteristics. Unambiguous expression of the values of these characteristics requires the identification of a robust coordinate reference system, such as those associated with the World Geodetic System 1984 (WGS 84), and the ability to specify the values of such characteristics with respect to that coordinate reference system.
ISO 19133:2005, Geographic information – Location based services tracking and navigation defines position as “a point or geometry potentially occupied by a (spatial) object.” ISO 19107:2003, Geographic information – Spatial schema elaborates by stating that “A position is described by a single set of coordinates within a coordinate reference system”.
Spatial information also includes identifiers based on geographic place-names, physical addresses, and other systems in which a spatial reference in the form of a label or code is used to identifiy a location that may then be more rigorously tied to a position with respect to a coordinate reference system.
ISO 19112:2003, Geographic information – Spatial referencing by geographic identifiers defines location as “an identifiable geographic place.” ISO/WD 19160-1, Geographic information – Addressing – Part 1: Conceptual model defines a (physical) address as “structured information that uniquely references a (physical) object for the purpose of identification and (spatial) location.”
ISO/CD 19155, Geographic information – Place Identifier (PI) architecture defines place as “an identifiable part of any space”, where a “place” may be located in either the real or virtual world.
In this specification, a “place” is referred to as a:
•	position when that place is identified using spatial coordinates (e.g., geodetic latitude and longitude);
•	location when that place is identified using geographic identifiers (e.g., place name); or
•	address when that place is identified using (physical ) addresses (e.g., postal address).
In all three types of “place”, a spatial reference system is established that (eventually) allows identification of a position in the real world.
•	In the case of positioning, a coordinate reference system relates the position to an established datum (e.g., one based on an ellipsoid of revolution describing the shape of the Earth).
•	In the case of locating, a spatial reference system using geographic identifiers is established that relates locations to positions. Gazetteers are then used to establish directories of (geographically) identified locations along with their corresponding positions.
•	In the case of addressing, a systematic mapping is established based on the structure of the addressing scheme that allows for geocoding – the process of converting addresses (e.g., "1600 Amphitheatre Parkway, Mountain View, CA") into positions (e.g., geodetic latitude/ longitude {37.423021 -122.083739} ).
This specification supports all three types of “place”. It does not specify mechanisms for converting among positions, locations, and addresses.
1.8	TSPI Capabilities
This specification provides a “bridge” from legacy information exchanges (e.g., USMTF and VMF-XML) to a well-structured, well-documented, robust XML schema for spatiotemporal data which has broad DoD/IC applicability.
The TSPI specification is a common set of XML-based representations, being shared across many communities of interest. It is a robust mechanism for expressing “Where” and “When” in various core and extended XML-based information schemas in the DoD/IC. It addresses the specification and exchange of data regarding:
•	Earth-referenced spatial coordinate systems;
•	Two- and three-dimensional position in an Earth-referenced spatial coordinate system;
•	Geographic identifiers based on geographic place-names, physical addresses, and other systems in which a spatial reference in the form of a label or code is used to identifiy a location that may then be more rigorously tied to a position in an Earth-referenced spatial coordinate system;
•	Elevation, height, altitude and depth in a suitable one-dimensional “vertical” frame of reference (e.g., Earth Gravitational Model 1996);
•	One-, two-, and three-dimensional extent (shape) in terms of a structured set of positions;
•	Direction (bearing) between two positions;
•	Dimensional measures (“size”; e.g., length, width, height, depth, radius) in a suitable frame of reference;
•	Rates of change in these spatial characteristics (e.g., linear speed, linear velocity, angular velocity, acceleration);
•	Earth-referenced temporal coordinate systems;
•	Position (instant) in an Earth-referenced temporal coordinate system;
•	Extent (duration) in an Earth-referenced temporal coordinate system;
•	Spatiotemporal quality assessment information to include the precision of data values as well as quantitative and qualitative estimates of the accuracy and/or uncertainty of spatial and temporal characteristics; and
•	“Presentation-oriented” data representations intended principally or exclusively for human-to-human communication (e.g., “DDDMMSSH” type encodings). Such data representations constitute “presentations” only in the sense that they encode a spatial position specification in a manner amenable to direct use in generating text-strings for use in human-computer interfaces.
The following topics fall outside the scope of this specification:
•	Spatial coordinate systems that are time-varying; 
•	Topologic relations  between/among spatial extents (shapes);
•	Geocoding, coordinate conversion, datum transformation, and associated algorithms for relating spatiotemporal data specified in different spatiotemporal reference systems;
•	Methods for determining the precision, accuracy and/or uncertainty of spatiotemporal data;
•	Encodings for bit-oriented communications environments;  and
•	Means for asserting domain-specific semantics of entities with spatiotemporal characteristics (e.g., equipment, feature, or target types).
This specification is:
1.	An ISO 19106-conformant Class 2 Profile of ISO 19136:2007 (GML).
2.	An ISO 19106-conformant Class 2 Profile of ISO 6709:2008.
3.	Maximally consistent with IETF RFC 5870 – A Uniform Resource Identifier for Geographic Locations (’geo’ URI).
4.	Designed so as to enable the use of applicable OGC Open Web Service standards with TSPI-conformant instance documents. This may, in some cases, require data mediation through the use of XSLT technology.
5.	Designed so as to maximally enable data mediation to/with other XML-based schemas in common use in the DoD/IC that include time-space-position information, e.g., XML-MTF, VMF-XML, and XML-based encodings of the NSG Application Schema (NAS).
This specification utilizes the terminology of ISO 80000:2009 Quantities and units (multi-part).  This means that throughout this specification the standard unit of measure for length (dimension) is named “metre”.
1.9	TSPI Schema Components
The TSPI Schema is implemented in terms of a set of data-file components that collectively are referred to throughout this specification simply as “the TSPI Schema” when greater specificity is unnecessary. These data-file components are of one of the following three types:
•	XML Schema documents (XSD): These specify authoritative XML Schema components that are either:
o	imported from other XML namespaces, or 
o	define the TSPI XML namespaces (‘tspi-core’, ‘tspi-ext’, and ‘tspi’).
•	ISO/IEC 19757:2006 Schematron (SCH) documents: These specify authoritative constraints applied to XML Schema components that are either:
o	imported from other XML namespaces, or
o	define the TSPI XML namespaces (‘tspi-core’, ‘tspi-ext’, and ‘tspi’).
•	XML instance documents: These either specify:
o	authoritative GML-based CodeList Dictionaries that are used by various XML Schema components and associated Schematron assertions, or
o	informative examples of the use of TSPI Schema components in XML-based information exchange.
Almost all of these data-files depend on the the TSPI XML Namespace(s); Annex A.4 specifies how those namespaces relate to the DoD Data Services Environment (DSE) Metadata Registry (MDR) and the information resources that are published there.
The three TSPI-associated XML namespaces are as follows:
•	‘tspi-core’: Specifies core XML type components that shall always be used as specified without further restriction unless documented by, and accomplished using, Schematron assertions.
•	‘tspi-ext’: TSPI-conformant registered extensions that specify additional representations for spatial position, geographic location, and/or physical address. It is populated with initial high-value extensions, but is dynamically maintained on the MDR. Its use is conditional on the requirements of a given system/application and its accompanying business requirements.
•	‘tspi’: XML elements and non-core types with less strict reuse rules than ‘tspi-core’; it imports the schemas of the ‘tspi-core’and ‘tspi-ext’ namespaces.
This TSPI specification defines XML Schema components in all three of these XML namespaces, as well as related Schematron assertions and GML dictionaries upon which those components depend.
When any of these three XML namespaces are referenced from other schemas then the single valid schemaLocation for the <import> is that established in the MDR. For the current TSPI release these are, respectively:
•	‘tspi-core’: http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0.0/tspi-core.xsd
•	‘tspi-ext’: http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0.0/tspi-ext.xsd
•	‘tspi’: http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0.0/tspi.xsd 
Schema component files (XSD, SCH, XML) may be copied to other locations for development and/or efficiency purposes, however any alteration or substitution violates TSPI conformance requirements (see Annex B).
1.10	Specification Overview
This specification is organized into seven primary sections followed by a series of Annexes, some of which are informative in nature (and so marked).
Section 2 specifies conformance requirements.
Section 3 specifies the normative and informative references used in this specification. Normative references are necessary for the complete understanding of this specification. Informative references are not essential but provide supplementary material from which the user of this specification may benefit.
Section 4 specifies the terms, definitions and acronyms used in this specification.
Section 5 specifies the mechanisms established by this specification for representing spatial position. It also specifies mechanisms for extending TSPI (and GML) with additional representations for spatial position and includes initial high-value extensions.
Section 6 specifies the mechanisms established by this specification for representing spatial location using geographic identifiers (e.g., place names). It also specifies mechanisms for extending TSPI with additional representations for spatial location and includes initial high-value extensions.
Section 7 specifies the mechanisms established by this specification for representing (physical) address (e.g., postal address).
Section 8 specifies the mechanisms established by this specification for representing temporal position.
Annex A (normative) establishes a set of conventions used throughout this specification. These include naming and design rules, the referencing of various schemas, the establishment and use of information resources (e.g., coordinate reference systems, code lists, and units of measure) in support of this specification, the use of ISO/IEC 19757:2006 Schematron in validating XML instance documents, and issues in conformance and reuse of this specification.
Annex B (normative) establishes a conformance test suite.
Annex C (informative) identifies a set of Geodetic 2D coordinate reference systems that are registered in the GSIP Governance Namespace of the DoD Data Services Environment (DSE) Metadata Registry (MDR) that may be used with this specification.
Annex D (informative) explains the principal structuring concepts used by GML: Profiles and Application Schemas.
Annex E (informative) describes the procedures to be followed when extending the TSPI through a process of registering new XML components, code lists, and codes, to include Coordinate Reference Systems, Physical Quantities, Units of Measure, and Data Quality Measures.
2	Conformance
Conformance to this specification ensures that XML instance documents are both well-formed (meet syntactic requirements) and valid (meet logical requirements) with respect to the requirements of the TSPI Schema, and in the case of a TSPI Schema-conformant application whether it correctly writes and/or reads TSPI Schema-conformant instance documents.
Conformance with the TSPI specification shall be determined using all of the relevant tests and conditions specified in Annex B. The TSPI Schema includes multiple XML namespaces (see Section 1.9) all of which are included in conformance testing.
The TSPI Schema supports a range of existing and future business practices for time-space-position information specification and exchange within the NSG. In this specification some of these practices are deprecated while others are recommended. These identifications shall be considered as advisory in nature; their adoption is a policy decision that falls outside the scope of this specification. Individual COIs need to determine what policies they will adopt when employing the TSPI Schema.
Future versions of the TSPI specification may include stronger policy language and/or remove representation and encoding options to ensure that communities of practice within the NSG more rapidly converge on a small set of widely adopted business practices.
3	References
3.1	Normative
The documents listed in Table 1 are indispensable to understanding and using this specification. For dated references, only the cited edition or version applies. For undated references, the latest edition or version of the referenced document (including any amendments) applies.
Table 1 – Normative References
Standard or Specification 
CJCSI 3900.01C, Position (Point and Area) Reference Procedures, 30 June 2007
http://www.dtic.mil/cjcs_directives/cdata/unlimit/3900_01.pdf
NIMA TR8350.2, DoD World Geodetic System 1984 – Its Definition and Relationships with Local Geodetic Systems, Third Edition, Amendment 2, 23 June 2004
http://earth-info.nga.mil/GandG/publications/tr8350.2/tr8350_2.html 

DMA TM8358.1, Datums, Ellipsoids, Grids, and Grid Reference Systems, September 1990
http://earth-info.nga.mil/GandG/publications/tm8358.1/toc.html 

DMA TM8358.2, The Universal Grids: Universal Transverse Mercator (UTM) and Universal Polar Stereographic (UPS), September 1989
http://earth-info.nga.mil/GandG/publications/tm8358.2/TM8358_2.pdf 

Earth Gravitational Model EGM2008, April 2008
http://earth-info.nga.mil/GandG/wgs84/gravitymod/egm2008/egm08_wgs84.html 

ISO 6709:2008, Standard representation of geographic point location by coordinates
ISO 8601:2004, Data elements and interchange formats – Information interchange – Representation of dates and times
ISO 19136:2007, Geographic information – Geography Markup Language (GML)
	https://nsgreg.nga.mil/doc/view?i=2016 
(same as: Geography Markup Language, Version 3.2.1 (OGC 07-036))
OGC® Geography Markup Language (GML) – Extended schemas and encoding rules, 
Version 3.3 (OGC 10-129r1)
https://nsgreg.nga.mil/doc/view?i=2296 

FGDC-STD-016-2011, United States Thoroughfare, Landmark, and Postal Address Data Standard,
February 2011
	http://www.fgdc.gov/standards/projects/FGDC-standards-projects/street-address 

XML Schema Part 1: Structures (Second Edition), 28 October 2004
http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/ 

XML Schema Part 2: Datatypes (Second Edition), 28 October 2004
http://www.w3.org/TR/2004/REC-xmlschema-2-20041028/ 

ISO/IEC 19757:2006, Information Technology – Document Schema Definition Language (DSDL) – Part 3: Rule-based validation – Schematron
	http://standards.iso.org/ittf/PubliclyAvailableStandards/c040833_ISO_IEC_19757-3_2006(E).zip 

3.2	Informative
The informative (non-normative) documents listed in Table 2 are useful to understanding and using this specification. For dated references, only the cited edition or version applies.
Table 2 – Informative References
Standard or Specification 
ISO 3166-1, Codes for the representation of names of countries and their subdivisions – Part 1: Country codes
ISO 19101:2002, Geographic information – Reference model
ISO 19106:2004, Geographic information – Profiles
ISO 19107:2003, Geographic information – Spatial schema
ISO 19108:2002, Geographic information – Temporal schema
ISO 19111:2007, Geographic information – Spatial referencing by coordinates
ISO 19112:2003, Geographic information – Spatial referencing by geographic identifiers
ISO 19133:2005, Geographic information – Location based services tracking and navigation
ISO/DIS 19157-1, Geographic information – Data quality
ISO/WD 19160-1, Geographic information – Addressing – Part 1: Conceptual model
ISO 80000:2009 (multi-part), Quantities and units
NIST Special Publication 811, Ed. 2008, Guide for the Use of the International System of Units (SI)
	http://physics.nist.gov/cuu/pdf/sp811.pdf 

IEC 60050-111:1996/Amd.1 Ed 2:2005, International Electrotechnical Vocabulary – Chapter 111: Physics and chemistry – Time and related concepts
IEC 60050-713:1998, International Electrotechnical Vocabulary – Part 713: Radiocommunications: transmitters, receivers, networks and operation
Recommendation ITU-R TF.460-6, Standard-frequency and time-signal emissions
https://nsgreg.nga.mil/doc/view?i=2097 

ISO/IEC 11404:2007, Information technology – General-Purpose Datatypes (GPD)
ISO/IEC Guide 98:1995, Guide to the expression of uncertainty in measurement
Uncertainty Markup Language (UnCertML) Version 0.6 (OGC 08-122r2)
http://portal.opengeospatial.org/files/?artifact_id=33234 

IETF RFC 5870 - A Uniform Resource Identifier for Geographic Locations (’geo’ URI), June 2010	
http://tools.ietf.org/html/rfc5870 

NGA.SIG.0007_1.0, Information Guidance for Earth Gravitational Model 2008 (EGM 2008), 15 February 2012
NGA.STND.0012-1_2.1 NSG Metadata Foundation (NMF) – Part 1: Core,
Version 2.1 (draft), 29 February 2011
NGA.STND.0012-2_1.0 NSG Metadata Foundation (NMF) – Part 2: Quality Metadata,
Version 1.0 (draft), 20 February 2011
OASIS XML Catalogs, Committee Specification 06 Aug 2001
http://www.oasis-open.org/committees/entity/spec-2001-08-06.html 

Efficient XML Interchange (EXI) Format 1.0, W3C Recommendation, 10 March 2011
	http://www.w3.org/TR/2011/REC-exi-20110310 

OGC Best Practices Document: Gazetteer Service - Application Profile of the Web Feature Service Implementation Specification, Version 0.9.4 (OGC 11-122r1)
NSG Application Schema (NAS) – Part 1: Platform Independent Model, Version 4.0, 21 November 2011
	https://nsgreg.nga.mil/doc/view?i=81071  

4	Terms, Definitions and Acronyms
4.1	Terms and Definitions
The terms and definitions specific to this specification are given in Table 3.
Table 3 – Definitions Applicable to this Specification
Term	Definition
accuracy	The closeness of agreement between a test result or measurement result and the true value. [ISO 6709:2008]
(physical) address	Structured information that uniquely references an object for purposes of identification and (spatial) location. [ISO/WD 19160-1]
altitude	A height where the chosen reference surface is mean sea level. [ISO 6709:2008] 
coordinate	One of a sequence of n numbers designating the position of a point in n-dimensional space. [ISO 19111:2007]
NOTE: In a coordinate reference system, the coordinate numbers are qualified by units.
coordinate reference system	A coordinate system that is related to a (physical) object by a datum. [ISO 19111:2007]
coordinate system	A set of mathematical rules for specifying how coordinates are to be assigned to points. [ISO 19111:2007]
coordinate tuple	An ordered list of values composed of a sequence of coordinates. [ISO 19111:2007]
NOTE: The number of coordinates in the coordinate tuple equals the dimension of the coordinate system; the order of coordinates in the coordinate tuple is identical to the order of the axes of the coordinate system.
Coordinated Universal Time (UTC)	A time scale which forms the basis of a coordinated radio dissemination of standard frequencies and time signals; it corresponds exactly in rate with International Atomic Time (TAI), but differs from it by an integral number of seconds. [IEC 60050-713 and ITU-R TF.460-6]
NOTE1: UTC is established by the International Bureau of Weights and Measures (BIPM, i.e., Bureau International des Poids et Mesures) and the International Earth Rotation Service (IERS). UTC provides the basis of standard time, the use of which is legal in most countries.
data quality element	A quantitative component documenting the quality of a dataset. [ISO 19101:2002]
NOTE1: The applicability of a data quality element to a dataset depends on both the dataset’s content and its product specification; the result being that all data quality elements may not be applicable to all datasets.
NOTE2: Data quality elements may, on occasion, be qualititative in nature.
datum	A parameter or set of parameters that define the position of the origin, the scale, and the orientation of a coordinate system.
depth	The distance of a point from a chosen reference surface measured downward along a line perpendicular to that surface. [ISO 19111:2007]
NOTE: A depth above the reference surface will have a negative value.
duration	A non-negative quantity attributed to a time interval, the value of which is equal to the difference between the time points of the final instant and the initial instant of the time interval, when the time points are quantitative marks. [IEC 60050-111]
easting	The distance in a coordinate system, eastwards (positive) or westwards (negative) from a north-south reference line. [ISO 19111:2007]
NOTE: In use, the first of two coordinates which comprise a Cartesian system for the plane of a map projection, typically increasing in an eastward-like direction.  
ellipsoid	A surface formed by the rotation of an ellipse about a main axis. [ISO 19111:2007]
NOTE1: In this specification, ellipsoids are always oblate, meaning that the axis of rotation is always the minor axis.
NOTE2: A mathematical figure generated by the revolution of an ellipse about one of its axes. The ellipsoid that approximates the geoid is an ellipse rotated about its minor axis. [CJCSI 3900.01C]
ellipsoid height	See “geodetic height” and “height above ellipsoid”.
gazetteer	A directory of instances of a class or classes of features containing some information regarding (spatial) position. [ISO 19112:2003]
geocentric (coordinate system)	An Earth-centered Cartesian 3D coordinate system where the Z-axis is aligned with the Earth's rotation axis, the X-axis lies within the equatorial plane and a plane containing the prime meridian, and the Y-axis is such that (X,Y,Z) forms a right-handed coordinate system.
geodetic (coordinate system)	A coordinate system based on a reference ellipsoid as an approximation to the shape of the geoid. The position of a point relative to the ellipsoid is given by the triple, (λ, φ, h), where λ is the geodetic longitude, φ is the geodetic latitude, and h is the height of the point above the ellipsoid (taken perpendicularlay to the ellipsoid).
geoid	An equipotential surface of the Earth’s gravity field which is everywhere perpendicular to the direction of gravity and which best fits mean sea level either locally or globally. [ISO 19111:2007]
NOTE: The equipotential surface in the gravity field of the Earth that coincides with the undisturbed mean sea level extended continuously through the continents. The geoid is the reference surface for geodetic leveling (surveying) and some inertial navigation systems. [CJCSI 3900.01C]
geoid height	The height of the geoid above or below the referenced ellipsoid.
NOTE: Ellipsoid (geodetic) height (h) differs from heights related to the geoid (N) by the amount by which the geoid undulates relative to the ellipsoid.
geodetic datum	A datum describing the relationship of a two- or three-dimensional coordinate system to the Earth. [ISO 19111:2007]
NOTE1: A reference surface consisting of the following parameters: the latitude and longitude of an initial point (origin), the orientation of the network and the two parameters of a reference ellipsoid. [CJCSI 3900.01C] 
NOTE2: In the geodesy community the use of this term is restricted to the three-dimensional case.
geodetic height 	The distance of a point from the ellipsoid measured along the perpendicular from the ellipsoid to this point, positive if upwards or outside of the ellipsoid. [ISO 19111:2007]
NOTE1: Specified in CJCSI 3900.01C as Height Above [the] Ellipsoid (HAE); also known as “ellipsoid height”.
NOTE2: Symbolized as h.
geographic identifier	A spatial reference in the form of a label or code that identifies a location. [ISO 19112:2003]
geographic name	A name applied to a geographic feature. It is the proper name, specific term, or expression by which a particular geographic entity is, or was, known. A geographic entity is any relatively permanent part of the natural or manmade landscape or seascape that has recognizable identity within a particular cultural context. A geographic name, then, may refer to any place, feature, or area on the Earth's surface, or to a related group of similar places, features, or areas.
grid	Two sets of parallel lines intersecting at right angles and forming squares. [CJCSI 3900.01C]
NOTE: A grid is superimposed on maps, charts and other similar representations of the Earth's surface in an accurate and consistent manner to permit identification of ground locations with respect to other locations and the computation of direction and distance to other points.
height	The distance of a point from a chosen reference surface measured upward along a line perpendicular to that surface. [ISO 19111:2007] 
NOTE: A height below the reference surface will have a negative value.
height above ellipsoid	The distance above or below the ellipsoid (plus or minus). [CJCSI 3900.01C]
NOTE: Ellipsoid height is also called geodetic height or HAE.
instant	A point on the time axis. [IEC 60050-111]
(geodetic) latitude	The angle from the equatorial plane to the perpendicular to the ellipsoid through a given point with northwards treated as positive. [ISO 19111:2007]
NOTE: Symbolized as  (Greek letter ‘phi’).
location	An identifiable geographic place. [ISO 19112:2003] 
NOTE: For example, the “Eiffel Tower”, “Madrid, Spain”, or “California, USA”.
(geodetic) longitude	The angle from the prime meridian plane to the meridian plane of a given point with eastwards treated as positive. [ISO 19111:2007]
NOTE: Symbolized as  (Greek letter ‘lambda’).
map projection	A set of mathematical algorithms and associated parameters that establish a systematic, one-to-one correspondence between points on the surface of an ellipsoid and points on a plane while controlling the resulting geometric distortions. [CJCSI 3900.01C]
mean sea level	The average level of the surface of the sea over all stages of tide and seasonal variations. [ISO 19111:2007]
NOTE: Mean sea level in a local context normally means mean sea level for the region calculated from observations at one or more points over a given period of time. Mean sea level in a global context differs from a global geoid by not more than 2 metres.
northing	The distance in a coordinate system, northwards (positive) or southwards (negative) from an east-west reference line. [ISO 19111:2007]
NOTE: In use, the second of two coordinates which comprise a Cartesian system for the plane of a map projection, typically increasing in an northward-like direction.    
orthometric height	Approximately, the height above the geoid and symbolized as H.
NOTE: Geodetic height (h of the triple (λ, φ, h)) is measured along the perpendicular to the reference surface, but orthometric height (H) is measured along the plumb-line to the reference surface.
position	A point or geometry potentially occupied by a (spatial) object. [derived from ISO 19133:2007]
NOTE1: A (direct) position is described by a single set of coordinates within a coordinate reference system. [ISO 19107:2003]
NOTE2: A direct position is a semantic subtype of position. Direct positions as described can only define a point and therefore not all positions can be represented by a direct position. That is consistent with the “is type of” relation. A 19107 geometry is also a position, just not a direct position. [ISO 19133:2005]
precision	A measure of the repeatability of a set of measurements. [ISO 6709:2008]
quality	The totality of characteristics of a product that bear on its ability to satisfy stated and implied needs. [ISO 19101:2002]
resolution	The coordinate unit associated with the least significant digit of a coordinate. [ISO 6709:2008]
sexagesimal degree	An angle represented by a sequence of values in arc degrees, arc minutes and arc seconds. [ISO 6709:2008]
sounding datum	A tidal datum to which soundings and drying heights are referenced.
NOTE: It is usually taken to correspond to a low water stage of the tide.
spatial reference	A description of position in the real world. [ISO 19111:2007] 
NOTE: This may take the form of a label, code or coordinate tuple (a sequence of coordinates).
spatial reference system	A system for identifying position in the real world. [ISO 19112:2003]
time axis	A mathematical representation of the succession in time of instantaneous events along a unique axis. [IEC 60050-111]
time interval	A part of the time axis limited by two instants. [IEC 60050-111]
uncertainty	A measure of the inherent variability of repeated measurements of a quantity.
vertical datum	A datum describing the relation of gravity-related heights or depths to the Earth. [ISO 19111:2007]
NOTE1: A surface that approximates the size and shape of all or part of the Earth’s surface and is designated a height of zero. The height of any point that does not lie on this surface is measured along a line perpendicular to the reference surface and passing through the point. [CJCSI 3900.01C]
NOTE2: In most cases, the vertical datum will be related to mean sea level. Ellipsoid (geodetic) heights are treated as related to a three-dimensional ellipsoidal coordinate system referenced to a geodetic datum. Vertical datums include sounding datums (used for hydrographic purposes), in which case the heights may be negative heights or depths.
World Geodetic System 1984	An Earth-centered, Earth-fixed worldwide geodetic datum and reference system based on a determination of the Earth's parameters and gravity field.
Note: Also called "WGS 84".
4.2	Acronyms
The acronyms that are used in this standard are specified in the following list.
BIH	Bureau International de l'Heure
COI	Community of Interest
COTS	Commercial Off-The-Shelf
DDMS	(U.S.) Department of Defense Discovery Metadata Specification
DISR	(U.S.) Department of Defense Information Technology Standards Registry
DMA	Defense Mapping Agency
DoD	(U.S.) Department of Defense
DSDL	Document Schema Definition Language
DST	Daylight Savings Time
EGM96	Earth Gravitational Model 1996
EGM08	Earth Gravitational Model 2008
EXI	Efficient XML Interchange
FGDC	(U.S.) Federal Geographic Data Committee
FL	Flight Level
GEOINT	Geospatial Intelligence
GEOREF	World Geographic Reference System
GIS	Geographic Information System
GML	Geography Markup Language
GPAS	Geospatial Publicly Available Specifications
GPS	Global Positioning System
GSIP	GEOINT Structure Implementation Profile
GWG	GEOINT Standards Working Group
HAE	Height Above the Ellipsoid
IC	(U.S.) Intelligence Community
ICSR	(U.S.) Intelligence Community Standards Registry
IEC	International Electrotechnical Commission
IERS	International Earth Rotation Service
IES	Information Exchange Specification
IETF	Internet Engineering Task Force
IHO	International Hydrographic Organization
IMU	Inertial Measurement Unit
ISO	International Organization for Standardization
MDR	DoD Data Services Environment (DSE) Metadata Registry
MGRS	Military Grid Reference System
MSL	Mean Sea Level
MTF	Message Text Format
NAS	NSG Application Schema
NGA	National Geospatial-Intelligence Agency
NIMA	National Imagery and Mapping Agency
NIST	National of Standards and Technology
NSG	National System for Geospatial Intelligence
OGC	Open Geospatial Consortium
SCOTS	Standards-based COTS
SI	International System of Units
TSPI	Time-Space-Position Information
UCore	Universal Core
UoM	Unit of Measure
UPS	Universal Polar Stereographic (map projection)
URI	Uniform Resource Identifier
URL	Uniform Resource Locator
URN	Uniform Resource Name
USMTF	United States Message Text Format
USPS	U.S. Postal Service
UTC	Coordinated Universal Time
UTM	Universal Transverse Mercator (map projection)
VMF	Variable Message Format
VMF-XML	Variable Message Format – Extensible Markup Language
WFS	Web Feature Service
WGS 84	World Geodetic System 1984
WGS 84 EGM 96	WGS 84 Earth Gravitational Model 1996
W3C	World Wide Web Consortium
XML	Extensible Markup Language
XML-MTF	Extensible Markup Language – Message Text Format
XSD	XML Schema Definition
XSLT	Extensible Stylesheet Language Transformations
5	Where – Spatial Position
5.1	Introduction
The unambiguous exchange of spatiotemporal data requires the specification of the spatial, and accompanying quality assessment, characteristics of entities (e.g., equipment, combatants and targets).
Spatial information includes position, extent (shape), size, orientation, and rates of change in these characteristics. Unambiguous expression of the values of these characteristics requires the identification of a robust coordinate reference system, such as those associated with the World Geodetic System 1984 (WGS 84), and the ability to specify the values of such characteristics with respect to that coordinate reference system.
The TSPI Schema specifies XML types for use in the exchange of the following categories of spatial position-related information:
•	Two- and three-dimensional position in an Earth-referenced spatial coordinate system;
•	Elevation, height, altitude and depth in a suitable one-dimensional “vertical” frame of reference (e.g., Earth Gravitational Model 1996);
•	One-, two-, and three-dimensional extent (shape) in terms of a structured set of positions;
•	Direction (bearing) between two positions;
•	Dimensional measures (“size”; e.g., length, width, height, depth, radius) in a suitable frame of reference; and
•	Rates of change in these spatial characteristics (e.g., linear speed, linear velocity, angular velocity, acceleration).
In each of these information categories, as appropriate, this specification supports the specification of quality assessment information including the precision of data values as well as quantitative and qualitative estimates of the accuracy and/or uncertainty of spatial characteristics.
These spatial position-associated information types are specified in subsequent sections of this document.
5.2	Abstract Position
The TSPI Schema employs the abstract GML element gml:AbstractGeometry as the head of a substitution group of which all TSPI-specified elements that represent positions are members (as well as all GML-specified elements that represent positions). TSPI-specified elements include:
•	tspi:Point (see Section 5.4.2);
•	tspi:LineString (see Section 5.4.3);
•	tspi:Circle and tspi:Ellipse (see Sections 5.4.4 and 5.4.5);
•	tspi:Polygon, tspi:SimplePolygon, and tspi:SimpleRectangle (see Sections 5.4.6, 5.4.7, and 5.4.8); 
•	tspi:Envelope (see Section 5.4.9);
•	tspi:CircularSurface and tspi:EllipticalSurface (see Sections 5.4.10 and 5.4.11); and
•	 ‘tspi-ext’ elements that represent position (see Section  5.8).
When defining Information Exchange Specifications (IES) that <import> the TSPI Schema it is therefore sufficient to use the abstract GML element gml:AbstractGeometry wherever it is intended to represent a spatial position.
No elements shall be allowed as members of the gml:AbstractGeometry substitution group other than those in the ‘gml’ ("http://www.opengis.net/gml/3.2"), ‘gmlce’ ("http://www.opengis.net/gml/3.3/ce"), ‘tspi’, ‘tspi-core’ and ‘tspi-ext’ XML namespaces.
5.3	Position Infrastructure
5.3.1	Coordinate Reference Systems
5.3.1.1	Coordinates
A coordinate  is one of n scalar values that when taken together define a direct position. A coordinate tuple is an ordered list of n coordinates that define that position. In this TSPI specification the coordinate tuple shall be composed of one, two or three spatial coordinates. These coordinates shall be mutually independent and their number is equal to the dimension of the coordinate space.
Coordinates are ambiguous until the system to which those coordinates are related has been fully defined, otherwise coordinates are relatively meaningless. A Coordinate Reference System (CRS) defines the coordinate space such that the coordinate values are unambiguous. The order of the coordinates within the coordinate tuple and their unit(s) of measure are parts of the CRS definition.
ISO 19136:2007 (GML) encodes a spatial coordinate as an xsd:double. XML Schema Part 2: Datatypes Second Edition (W3C Recommendation 28 October 2004) Section 3.2.5 specifies the characteristics of this encoding as follows:
[Definition:]  The double datatype is patterned after the IEEE double-precision 64-bit floating point type  [IEEE 754-1985]. The basic value space of double consists of the values m × 2^e, where m is an integer whose absolute value is less than 2^53, and e is an integer between -1075 and 970, inclusive. In addition to the basic value space described above, the value space of double also contains the following three special values: positive and negative infinity and not-a-number (NaN). The order-relation on double is: x < y iff y - x is positive for x and y in the value space. Positive infinity is greater than all other non-NaN values. NaN equals itself but is incomparable with (neither greater than nor less than) any other value in the value space.
A literal in the lexical space representing a decimal number d maps to the normalized value in the value space of double that is closest to d; if d is exactly halfway between two such values then the even value is chosen. This is the best approximation of d ([Clinger, WD (1990)], [Gay, DM (1990)]), which is more accurate than the mapping required by [IEEE 754-1985].
double values have a lexical representation consisting of a mantissa followed, optionally, by the character "E" or "e", followed by an exponent. The exponent must be an integer. The mantissa must be a decimal number. The representations for exponent and mantissa must follow the lexical rules for integer and decimal. If the "E" or "e" and the following exponent are omitted, an exponent value of 0 is assumed.
The special values positive and negative infinity and not-a-number have lexical representations INF, -INF and NaN, respectively. Lexical representations for zero may take a positive or negative sign.
For example, -1E4, 1267.43233E12, 12.78e-2, 12, -0, 0 and INF are all legal literals for double.
The canonical representation for double is defined by prohibiting certain options from the Lexical representation (§3.2.5.1). Specifically, the exponent must be indicated by "E". Leading zeroes and the preceding optional "+" sign are prohibited in the exponent. If the exponent is zero, it must be indicated by "E0". For the mantissa, the preceding optional "+" sign is prohibited and the decimal point is required. Leading and trailing zeroes are prohibited subject to the following: number representations must be normalized such that there is a single digit which is non-zero to the left of the decimal point and at least a single digit to the right of the decimal point unless the value being represented is zero. The canonical representation for zero is 0.0E0.
ISO 19136:2007 (GML) encodes a coordinate tuple as a whitespace-separated list of xsd:double. 
5.3.1.2	CRS Components
A CRS is defined by the combination of one coordinate system with one datum.
A coordinate system is composed of a non-repeating sequence of coordinate system axes. The dimension of the coordinate space, the names, the unit(s) of measure, the direction(s) and sequence of the axes are all part of the coordinate system definition. The number of axes is equal to the dimension of the space of which it describes the geometry. Section 5.3.1.4 addresses the specification of coordinate systems in greater detail.
A datum specifies the relationship of a coordinate system to a (physical) object, thus ensuring that the abstract mathematical concept “coordinate system” can be applied to the practical problem of describing positions of features on or near the object's surface by means of coordinates. The reference object is generally, but not necessarily, the Earth; for certain coordinate reference systems, the object may be a moving platform – however these latter cases are not addressed by this specification. Section 5.3.1.5 addresses the specification of datums in greater detail.
5.3.1.3	CRS Categories
CRS are distinguished by the type of datum associated with the CRS. In accordance with ISO 19111:2007 Clause 8.3, this specification distinguishes four categories of CRS.
•	Geodetic  CRS: A coordinate reference system that is associated with a datum describing the relationship of a two- or three-dimensional coordinate system to the Earth. They are associated with ellipsoidal and 3D Cartesian coordinate systems. A geodetic CRS using 2D ellipsoidal coordinates (geodetic longitude and geodetic latitude) is used when positions of features are described on the surface of the ellipsoid; a geodetic CRS using 3D ellipsoidal coordinates (geodetic longitude, geodetic latitude, and ellipsoid (geodetic) height: h) is used when positions are described on, above or below the ellipsoid. A geodetic 3D CRS using three-dimensional Cartesian coordinates is used when describing positions relative to the center of the Earth.
•	Vertical CRS: A coordinate reference system that is associated with a datum describing the relation of gravity-related heights or depths to the Earth.  Vertical CRSs make use of the direction of gravity to define the concept of height (e.g., orthometric height (H)) or depth.
It is established practice to create and use maps/charts that represent the curved surface of the Earth as if it were flat. Doing so necessarily introduces distortions of various types (e.g., directions, shapes, and sizes) however positions on the map/chart can be exactly related to positions in the real-world. The relationship between the curved surface of the Earth and the flat surface of the map/chart is known as a “map projection” (e.g., Transverse Mercator).
•	Projected CRS: A coordinate reference system which is derived from a geodetic CRS by applying a map projection coordinate conversion to geodetic latitude and geodetic longitude coordinate values to obtain X and Y positions on the map/chart sheet.
The traditional separation of horizontal and vertical position results in CRSs that are horizontal (2D) and vertical (1D) in nature, as opposed to truly three-dimensional. It is established practice to combine the horizontal coordinates of a point with a height or depth from a different CRS. The CRS to which these 2D + 1D coordinates are referenced combines the separate horizontal and vertical CRS of the horizontal and vertical coordinates.
•	Compound CRS: A coordinate reference system consisting of a non-repeating sequence of two or more single CRS, none of which can themselves be compound. The coordinate order within a coordinate tuple for a Compound CRS follows the order of coordinates within the coordinate tuples for each of its component single CRSs, in the order of the component single CRSs. In this specification a Compound CRS shall contain exactly three axes, typically x and y of a map projection followed by ellipsoid (geodetic) height h  or orthometric height H.
These four categories of CRS are the basis for the Earth-referenced spatial coordinate systems supported by this TSPI specification.
5.3.1.4	Coordinate Systems
A coordinate system is composed of a non-repeating sequence of coordinate system axes. The dimension of the coordinate space, the names, the unit(s) of measure, the direction(s) and sequence of the axes are all part of the coordinate system definition. The number of axes is equal to the dimension of the space of which it describes the geometry.
In this specification coordinate systems are of three types: Cartesian, ellipsoidal and linear.
Cartesian coordinate systems are either two- or three-dimensional; the position is specified relative to orthogonal straight axes. All axes shall have the same unit of measure. They are used with both geodetic and projected CRS. When used with geodetic CRS the axis names and ordering are: geocentric X (followed by) geocentric Y (followed by) geocentric Z. When used with Projected CRS in this specification the axis names and ordering are always easting (followed by) northing.
Ellipsoidal coordinate systems are either two- or three-dimensional, their axes are (in effect) curved, and position is specified by geodetic longitude, geodetic latitude, and (in the three-dimensional case) ellipsoid (geodetic) height – thus (λ, φ, h). They are only used with geodetic CRS. In this specification the axis ordering is always geodetic longitude (followed by) geodetic latitude (followed conditionally by) ellipsoid (geodetic) height (h).
Linear coordinate systems are one-dimensional, and position is specified relative to a single axis.  In this specification when specifying a CRS these are only used with Vertical CRS. The single axis is named (gravity-related) height (H), altitude, or depth.
5.3.1.5	Datums
In accordance with ISO 19111:2007 Clause 8.3, in this specification spatial datums are of two types: geodetic and vertical.
A geodetic datum describes the relationship of a two- or three-dimensional coordinate system to the surface of the Earth. It is specified by (i) an ellipsoid approximating the shape of the Earth, (ii) a prime meridian – the origin from which geodetic longitude values are specified (e.g., North-South plane through the focal point of the transit instrument of the Royal Obervatory at Greenwhich, England), and (iii) typically, a point of origin and orientation where the ellipsoid is attached to the Earth.
The ellipsoid is defined either by:
•	semi-major axis length and inverse flattening ratio; or
•	semi-major axis length and semi-minor axis length; or
•	radius of a sphere, being a special case of an ellipsoid whose semi-major axis length = semi-minor-axis length.  
The plane formed by rotating the semi-major axis about the semi-minor axis establishes the origin (equator) from which geodetic latitude values are specified..
In this specification vertical datums are of two types: geoidal and depth.
Geoidal vertical datums establish the origin of the vertical coordinate system axis as approximating a constant gravitational potential surface, usually the geoid. Such a reference surface is usually determined by a national or scientific authority and is then a well-known, named datum. Mean Sea Level (MSL), as determined by an appropriate local authority,  is widely used – however it is a recommended practice within the DoD/IC to approximate Mean Sea Level heights with the particular EGM pedigree used with the data type (e.g., DTED and SRTM use EGM96) or for new data to use the latest Earth Gravitational Model defined within WGS 84 (EGM08 as of 1 April 2012).
NGA.SIG.0007_1.0, Information Guidance for Earth Gravitational Model 2008 (EGM 2008), 15 February 2012, establishes the EGM08 as the current model for the WGS 84 EGM from which geoid heights are derived for the NSG. All previous EGMs, geoid grids, and implementations are categorized as legacy data. Support for EGM84 implementations is only available by special request as of 1 October 2011. Support for EGM96 implementations will continue at least until December 2019.
Depth-based vertical datums establish the origin of the vertical coordinate system axis at a surface that has meaning for the purpose for which the associated vertical measurements are used. For hydrographic charts, this is often a predicted nominal sea surface (i.e., without waves or other wind and current effects) which occurs at low tide (e.g., Lowest Astronomical Tide (LAT) or Lowest Low Water Springs (LLWS)). The choice to be used in the preparation of charts is usually established by the hydrographic authority for each country. In riverine mapping a sloping and undulating River Datum, defined as the nominal river water surface occurring at a quantified river discharge, may be used.  
5.3.1.6	Registered CRS
This TSPI specification only allows for the use of CRS that have been registered in the DoD Data Services Environment (DSE) Metadata Registry (MDR) (see Annex A.5.2).
Each registered CRS is identified by a URI composed from a base URL:
http://metadata.ces.mil/mdr/ns/GSIP/crs/
To this is concatenated a short CRS-specific identifier. In the case of the World Geodetic System 1984 - Geographic, 2-Dimensional CRS, the resulting identification is by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
Each such URI has a corresponding CRS-specific accessible information resource.
Preceding sections of this specification described the structure of a CRS. The MDR information resource encodes this structure and CRS-specific values as an XML instance document using XML elements and types specified in ISO 19136:2007 (GML) Clause 12.3 Coordinate reference systems. Figure 1 illustrates the resulting registered specification for this commonly-used CRS.
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet href="crsViewer.xsl" type="text/xsl"?>
<gml:GeodeticCRS gml:id="WGS84E_2D" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:gco="http://www.isotc211.org/2005/gco" xmlns:gmd="http://www.isotc211.org/2005/gmd"
  xmlns:gml="http://www.opengis.net/gml/3.2">

  <gml:identifier codeSpace="http://metadata.ces.mil/mdr/ns/GSIP/crs">WGS84E_2D</gml:identifier>
  <gml:name>World Geodetic System 1984 - Geographic, 2-Dimensional</gml:name>
  <gml:remarks>Since its establishment for epoch 1984, additional higher accuracy reference frame realizations have been established based on specific Global Positioning System (GPS) weeks (for example: Week 873, denoted as “G873”); these revised realizations of the reference frame are generally only important to applications requiring centimetre-level horizontal positioning accuracy. gml:remarks>
  <gml:domainOfValidity>
    <gmd:EX_Extent>
      <gmd:description>
        <gco:CharacterString>Earth (Global)</gco:CharacterString>
      </gmd:description>
    </gmd:EX_Extent>
  </gml:domainOfValidity>
  <gml:scope>Whole Earth; used for horizontal positioning.</gml:scope>

  <gml:ellipsoidalCS>
    <gml:EllipsoidalCS gml:id="EllipsoidalCS_2D">
      <gml:identifier codeSpace="http://metadata.ces.mil/mdr/ns/GSIP/crs">EllipsoidalCS_2D</gml:identifier>
      <gml:axis>
        <gml:CoordinateSystemAxis uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/arcDegree" gml:id="geodeticLatitude">
          <gml:identifier codeSpace="http://metadata.ces.mil/mdr/ns/GSIP/term">geodeticLatitude</gml:identifier>
          <gml:remarks> The axis direction is positive towards the pole about which the Earth rotates in a counter-clockwise direction. gml:remarks>
          <!-- Symbol is small Greek phi. -->
          <gml:axisAbbrev>Lat</gml:axisAbbrev>
          <gml:axisDirection codeSpace="http://metadata.ces.mil/mdr/ns/GSIP/term"
          >north</gml:axisDirection>
        </gml:CoordinateSystemAxis>
      </gml:axis>
      <gml:axis>
        <gml:CoordinateSystemAxis uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/arcDegree" gml:id="geodeticLongitude">
          <gml:identifier codeSpace="http://metadata.ces.mil/mdr/ns/GSIP/term">geodeticLongitude</gml:identifier>
          <gml:remarks> The axis direction is positive in the direction of the Earth's rotation. </gml:remarks>
          <!-- Symbol is small Greek lambda. -->
          <gml:axisAbbrev>Lon</gml:axisAbbrev>
          <gml:axisDirection codeSpace="http://metadata.ces.mil/mdr/ns/GSIP/term"
          >east</gml:axisDirection>
        </gml:CoordinateSystemAxis>
      </gml:axis>
    </gml:EllipsoidalCS>
  </gml:ellipsoidalCS>

  <gml:geodeticDatum>
    <gml:GeodeticDatum gml:id="WGS84_Datum">
      <gml:identifier codeSpace="http://metadata.ces.mil/mdr/ns/GSIP/crs">WGS84_Datum</gml:identifier>
      <gml:name>World Geodetic System 1984</gml:name>
      <gml:remarks>This datum is defined by Department of Defense World Geodetic System 1984 - Its Definition and Relationships with Local Geodetic Systems, NIMA TR8350.2, Third Edition, Amendment 2, 2000-01-03.</gml:remarks>
      <gml:scope>Earth (Global)</gml:scope>
      <gml:primeMeridian>
        <gml:PrimeMeridian gml:id="Greenwich">
          <gml:identifier codeSpace="http://metadata.ces.mil/mdr/ns/GSIP/crs">Greenwich</gml:identifier>
          <gml:name>Greenwich</gml:name>
          <gml:greenwichLongitude uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/arcDegree"
          >0</gml:greenwichLongitude>
        </gml:PrimeMeridian>
      </gml:primeMeridian>
      <gml:ellipsoid>
        <gml:Ellipsoid gml:id="WGS84_Ellipsoid">
          <gml:identifier codeSpace="http://metadata.ces.mil/mdr/ns/GSIP/crs">WGS84_Ellipsoid</gml:identifier>
          <gml:semiMajorAxis uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/metre">6378137.0</gml:semiMajorAxis>
          <gml:secondDefiningParameter>
            <gml:SecondDefiningParameter>
              <gml:inverseFlattening uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/unitless"
                >298.257223563</gml:inverseFlattening>
            </gml:SecondDefiningParameter>
          </gml:secondDefiningParameter>
        </gml:Ellipsoid>
      </gml:ellipsoid>
    </gml:GeodeticDatum>
  </gml:geodeticDatum>
</gml:GeodeticCRS>
Figure 1 – WGS84E_2D CRS Specification
5.3.2	Earth-referenced Coordinate Reference Systems
5.3.2.1	Coordinate Reference System Types
This TSPI specification supports seven types of CRS, as follows:
1.	Geodetic 2D: The coordinate system is ellipsoidal and most commonly the datum will be World Geodetic System 1984 (WGS 84) however other geodetic datums of limited geographic extent may be employed for particular purposes. This specification has the following restrictions:
a.	WGS84E_2D is the recommended practice (see Section 5.3.2.2).
b.	Geodetic 2D CRS as specified in Annex C are also supported.
c.	An alternative Geodetic 2D CRS for a limited-extent geographic region may be used if that CRS has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
2.	Geodetic 3D: The coordinate system is ellipsoidal and most commonly the datum will be WGS 84 however other geodetic datums of limited geographic extent may be employed for particular purposes. The third coordinate axis is perpendicular to the ellipsoid, positive upwards. This specification has the following restrictions:
a.	WGS84E_3D is the recommended practice (see Section 5.3.2.3).
b.	An alternative Geodetic 3D CRS for a limited-extent geographic region may be used if that CRS has been registered in the GSIP Governance Namespace in the MDR.
3.	Geocentric 3D: The coordinate system is Cartesian and the datum is always WGS 84; these establish a right-handed Earth-centered Earth-fixed (ECEF) reference frame. This specification has the following restrictions:
a.	WGS84C_3D is the only supported Geocentric 3D CRS (see Section 5.3.2.4).
4.	Vertical: The coordinate system is linear, most commonly based on the geoid, thus the third coordinate is an orthometric height or altitude; less commonly the Vertical CRS will be based on a sounding datum, in which case the third coordinate is a depth. This specification has the following restrictions:
a.	EGM96_H and EGM96_D are recommended practices (see Section 5.3.2.5.2).
b.	EGM08_H and EGM08_D are emerging practices (see Section 5.3.2.5.3).
c.	MSL_H and MSL_D are deprecated practices (see Section 5.3.2.5.4). It is instead recommended practice within the DoD/IC to approximate Mean Sea Level heights with the particular EGM pedigree used with the data type (e.g., DTED and SRTM use EGM96).
d.	An alternative Vertical CRS may be used if that CRS has been registered in the GSIP Governance Namespace in the MDR.
5.	Projected 2D: The coordinate system is Cartesian, most commonly based on the Transverse Mercator or Polar Stereographic map projections.  Most commonly the datum will be WGS 84, however other geodetic datums of limited geographic extent may be employed for particular purposes. This specification has the following restrictions:
a.	WGS84E_UTM* and WGS84E_UPS* are recommended practices (see Section 5.3.2.6.3).
b.	Only the UTM- and UPS-based projections are supported.
c.	An alternative Projected 2D CRS may be used if that CRS has been registered in the GSIP Governance Namespace in the MDR and it is either UTM- or UPS-based.
6.	Compound = Geodetic 2D + Vertical: The coordinate system is ellipsoidal and most commonly the datum will be WGS 84 however other geodetic datums of limited geographic extent may be employed for particular purposes. Most commonly the Vertical CRS will be based on the geoid, thus the third coordinate is an orthometric height or altitude; less commonly the Vertical CRS will be based on a sounding datum, in which case the third coordinate is a depth (meaning positive downwards). This specification has the following restrictions:
a.	WGS84E_EGM96_H and WGS84E_EGM96_D are recommended practices (see Section 5.3.2.7.2).
b.	WGS84E_EGM08_H and WGS84E_EGM08_D are are emerging practices (see Section 5.3.2.7.3).
c.	WGS84E_MSL_H and WGS84E_MSL_D are deprecated practices (see Section 5.3.2.7.4). It is instead recommended practice within the DoD/IC to approximate Mean Sea Level heights with the particular EGM pedigree used with the data type (e.g., DTED and SRTM use EGM96).
d.	An alternative Compound Geodetic 2D + Vertical CRS may be used if that CRS has been registered in the GSIP Governance Namespace in the MDR and it uses the MSL Vertical CRS.
7.	Compound = Projected 2D + Vertical: Most commonly the Projected CRS (a Cartesian coordinate system) will be based on the Transverse Mercator or Polar Stereographic map projections and the Vertical CRS will be based on the geoid, thus the third coordinate is an orthometric height or altitude; less commonly the Vertical CRS will be based on a sounding datum, in which case the third coordinate is a depth (meaning positive downwards). This specification has the following restrictions:
a.	It is recommended practice within the DoD/IC to approximate Mean Sea Level heights with the particular EGM pedigree used with the data type (e.g., DTED and SRTM use EGM96).
b.	WGS84E_UTM*_EGM96_H and WGS84E_UTM*_EGM96_D, WGS84E_UPS*_EGM96_H and WGS84E_UPS*_EGM96_D are recommended practices (see Section 5.3.2.8).
c.	Only the UTM- and UPS-based projections are supported.
d.	An alternative Compound Projected 2D + Vertical CRS may be used if that CRS has been registered in the GSIP Governance Namespace in the MDR and it is either UTM- or UPS-based.
The components of these seven CRS types are further specified in Section 5.3.1.
Sections 5.3.2.2 through 5.3.2.8 describe type-specific constraints and usages, and then provide coordinate tuple examples.
All CRS supported by this TSPI specification are registered in the GSIP Governance Namespace on the DoD Data Services Environment (DSE) Metadata Registry (MDR); see Annex A.5.2 for further information regarding these resources.
5.3.2.2	Geodetic 2D CRS
WGS 84 is a global reference system for identifying locations on the Earth and is defined in NIMA TR8350.2 Department of Defense World Geodetic System 1984 - Its Definition and Relationships with Local Geodetic Systems, 3rd Edition, Amendment 2. In addition to WGS 84, there are also many localized “Earth reference systems” that specify a different, usually geographically localized, geodetic datum. 
It is a recommended practice that when a Geodetic 2D CRS is used that it be in accordance with World Geodetic System 1984 - Geographic, 2-Dimensional, as specified in NIMA TR8350.2 (3rd Edition, Amendment 2) and identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
Instance documents conforming to the TSPI Schema may specify an alternative Geodetic 2D CRS if that CRS has been registered in the GSIP Governance Namespace in the DoD Metadata Registry. Annex C identifies additional Geodetic 2D CRS established in accordance with NIMA TR8350.2 (3rd Edition, Amendment 2).
All Geodetic 2D CRS share the following constraints:
a.	(geodetic) Latitude shall be a real value in the range:  -90 <= latitude <= +90
i.	North latitudes shall be positive; south latitudes shall be negative.
ii.	The unit of measure is arc degree (a planar angle).
b.	(geodetic) Longitude shall be a real value in the range:  -180 <= longitude <= +180; note that there are two equally acceptable values of longitude for the meridian opposite the prime meridian.
● In accordance with ISO 6709:2008 it is a recommended practice that the longitude value of -180° not be used.
i.	East longitudes shall be positive; west longitudes shall be negative.
ii.	The unit of measure is arc degree (a planar angle).
c.	In an XML instance document this coordinate tuple is encoded as two decimal values separated by a single space character in the coordinate order of Latitude and then Longitude.
i.	An example location in the North Sea, as it would appear in XML, is “53.809394 2.12955”.
In accordance with IETF RFC 5870 the following are recommended practices:
● The (geodetic) longitude of positions reflecting the geographic poles (latitude set to -90° or 90°) SHOULD be set to "0", although consumers MUST accept any (geodetic) longitude value from -180° through 180°.
● Where the (geodetic) latitude of a position is set to either -90° or 90°, the (geodetic) longitude MUST be ignored in comparison operations ("poles case").
● A (geodetic) longitude of 180° MUST be considered equal to a (geodetic) longitude of -180° for the purpose of position comparison (“date line case”).
5.3.2.3	Geodetic 3D CRS
WGS 84 is a global reference system for identifying locations on the Earth and is defined in NIMA TR8350.2 Department of Defense World Geodetic System 1984 - Its Definition and Relationships with Local Geodetic Systems, 3rd Edition, Amendment 2. In addition to WGS 84, there are also many localized “Earth reference systems” that specify a different, usually geographically localized, geodetic datum.
It is a recommended practice that when a Geodetic 3D CRS is used that it be in accordance with World Geodetic System 1984 - Geographic, 3-Dimensional, as specified in NIMA TR8350.2 (3rd Edition, Amendment 2) and identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_3D
Instance documents conforming to the TSPI Schema may specify an alternative Geodetic 3D CRS if that CRS has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
All Geodetic 3D CRS share the following constraints:
a.	Latitude shall be a real value in the range:  -90.0 <= latitude <= +90.0
i.	North latitudes shall be positive; south latitudes shall be negative.
ii.	The unit of measure is arc degree (a planar angle).
b.	Longitude shall be a real value in the range:  -180.0 <= longitude <= +180.0; note that there are two equally acceptable values of longitude for the meridian opposite the prime meridian.
● In accordance with ISO 6709:2008 it is a recommended practice that the longitude value of -180° not be used.
i.	East longitudes shall be positive; west longitudes shall be negative.
ii.	The unit of measure is arc degree (a planar angle).
c.	Height shall be a real value along an axis perpendicular to the local ellipsoid tangent plane (“height above the ellipsoid”). 
i.	Positions above the ellipsoid shall be positive; positions below the ellipsoid shall be negative.
ii.	The unit of measure is metre (a length).
d.	In an XML instance document this coordinate tuple is encoded as three decimal values separated by single space characters in the coordinate order of Latitude and then Longitude and then Height.
i.	An example location in the North Sea at sea level, as it would appear in XML, is “53.809394 2.12955 73.0”.
In accordance with IETF RFC 5870 the following are recommended practices:
● The (geodetic) longitude of positions reflecting the geographic poles (latitude set to -90° or 90°) SHOULD be set to "0", although consumers MUST accept any (geodetic) longitude value from -180° through 180°.
● Where the (geodetic) latitude of a position is set to either -90° or 90°, the (geodetic) longitude MUST be ignored in comparison operations ("poles case").
● A (geodetic) longitude of 180° MUST be considered equal to a (geodetic) longitude of -180° for the purpose of position comparison (“date line case”).
5.3.2.4	Geocentric 3D CRS
WGS 84 is a global reference system for identifying locations on the Earth and is defined in NIMA TR8350.2 Department of Defense World Geodetic System 1984 - Its Definition and Relationships with Local Geodetic Systems, 3rd Edition, Amendment 2.
When a Geodetic 3D CRS is used it shall be in accordance with World Geodetic System 1984 - Earth Centered, Earth Fixed (ECEF), as specified in NIMA TR8350.2 (3rd Edition, Amendment 2) and identified by the URI:
 http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84C_3D
where:
a.	Origin = Earth’s center of mass.
b.	Z-Axis = The direction of the IERS Reference Pole. This direction corresponds to the direction of the BIH Conventional Terrestrial Pole  (epoch 1984.0) with an uncertainty of 0.005”.
c.	X-Axis = Intersection of the IERS Reference Meridian and the plane passing through the origin and normal to the Z-Axis. The IERS Reference Meridian is coincident with the BIH Zero Meridian with an uncertainty of 0.005”.
d.	Y-Axis = Completes a right-handed, Earth-Centered Earth-Fixed orthogonal coordinate system.
e.	In an XML instance document this coordinate tuple is encoded as three decimal values separated by single space characters in the coordinate order of geocentric X and then geocentric Y and then geocentric Z.
i.	An example location in the North Sea, as it would appear in XML, is “3771793.97 140253.34 5124304.35”.
5.3.2.5	Vertical CRS
5.3.2.5.1	Introduction
In this TSPI specification most commonly the Vertical CRS will be based on the geoid, thus the coordinate is an orthometric height or altitude; less commonly the Vertical CRS will be based on a sounding datum, in which case the third coordinate is a depth (meaning positive downwards).
This specification supports three Vertical CRS: Earth Gravitational Model 1996 (EGM96), Earth Gravitational Model 2008 (EGM08) and Mean Sea Level (MSL).  These are used in the specification of corresponding Compound Geodetic 2D + Vertical CRS.
Instance documents conforming to the TSPI Schema may specify an alternative Vertical CRS if that CRS has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
5.3.2.5.2	Earth Gravitational Model 1996
It is current practice that when a Vertical CRS is used that it be in accordance with the Earth Gravitational Model 1996 (EGM96), as specified in NIMA TR8350.2 (3rd Edition, Amendment 2). This Vertical CRS is identified by one of two URIs depending on whether the coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/EGM96_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/EGM96_D
5.3.2.5.3	Earth Gravitational Model 2008
It is an emerging practice that when a Vertical CRS is used that it be in accordance with the Earth Gravitational Model 2008 (EGM08). This Vertical CRS is identified by one of two URIs depending on whether the coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/EGM08_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/EGM08_D
NGA.SIG.0007_1.0, Information Guidance for Earth Gravitational Model 2008 (EGM 2008), 15 February 2012, establishes the EGM08 as the current model for the WGS 84 EGM from which geoid heights are derived for the NSG. All previous EGMs, geoid grids, and implementations are categorized as legacy data.  Support for EGM96 implementations will continue at least until December 2019.
5.3.2.5.4	Mean Sea Level
It is a deprecated practice that when a Vertical CRS is used that it be in accordance with the location- and epoch-free mean sea level (MSL). This Vertical CRS is identified by one of two URIs depending on whether the coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/MSL_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/MSL_D
It is recommended practice within the DoD/IC to approximate Mean Sea Level heights with the particular EGM pedigree used with the data type (e.g., DTED and SRTM use EGM96).
5.3.2.5.5	Coordinate Tuples
All Vertical CRS share the following constraints:
a.	Height and Depth shall be real values; usually they will be non-negative.
i.	The unit of measure is metre (a length).
b.	In an XML instance document this coordinate tuple is encoded as a single decimal value for Height or Depth.
i.	An example location, as it would appear in XML, is “1530.4”. Depending on the specified CRS this may be an atmospheric (height) or a subterranean (depth) position.
5.3.2.6	Projected 2D CRS
5.3.2.6.1	Introduction
It is established practice to create and use maps/charts that represent the curved surface of the Earth as if it were flat. Doing so necessarily introduces distortions of various types (e.g., directions, shapes, and sizes) however positions on the map/chart can be exactly related to positions in the real-world. The relationship between the curved surface of the Earth and the flat surface of the map/chart is known as a “map projection” (e.g., Transverse Mercator).
A Projected 2D CRS is derived from a geodetic CRS by applying a map projection coordinate conversion to geodetic latitude and geodetic longitude coordinate values to obtain X and Y positions on the map/chart sheet.
When a Projected 2D CRS is used in the TSPI Schema it shall be either the UTM or UPS universal grid in accordance with DMA TM8358.2, The Universal Grids: Universal Transverse Mercator (UTM) and Universal Polar Stereographic (UPS), September 1989. Non-universal grids (e.g., British National Grid, Irish Transverse Mercator Grid, Madagascar Grid, and New Zealand Grid) shall not be used.
Most commonly the datum of the Projected 2D CRS universal grid will be World Geodetic System 1984 (WGS 84), however other geodetic datums of limited geographic extent may be employed for particular purposes.
Instance documents conforming to the TSPI Schema may specify an alternative universal grid-based Projected 2D CRS if that CRS has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
5.3.2.6.2	Projections and Grids
The coordinate system of a Projected 2D CRS is Cartesian and is most commonly based on the Transverse Mercator or Polar Stereographic map projections as specified in DMA TM8358.2, The Universal Grids: Universal Transverse Mercator (UTM) and Universal Polar Stereographic (UPS), September 1989. In order to limit map projection distortion to acceptable values, UTM defines 60 longitudinal zones of 6° in width, limits the latitudinal extents to between 84°N and 80°S, and adjusts the projection such that the scale factor is 0.9996 at the central meridian. For the same reasons UPS defines two polar zones (one above 84°N and the other below 80°S) with a scale factor of 0.994 at the origin (pole). Taken together they define 62 distinct Projected 2D CRS that “cover the Earth”.
These two map projections, UTM and UPS, are used to define corresponding metric military grids consisting of parallel lines intersecting at right angles and forming a regular series of squares. North-south lines provide a reference for “easting” coordinate values and east-west lines provide a reference for “northing” coordinate values. Each grid line occurs at a mutliple of 100,000 metres, 10,000 metres, 1,000 metres, or 100 metres. The UTM grid zones extend between 84°N and 80°S; the UPS grid zones cover regions northwards of 84°N and southwards of 80°S.
The UTM-based grid zones intentionally overlap the adjacent UPS grid zones by 1°, and the UPS-based grids intentionally overlay the adjacent UTM grid zones by 1° in the opposite direction. In consequence it is the case that positions between 84.5°N and 80.5°S may be reported using a UTM grid zone, and positions northwards of 83.5°N or southwards of 79.5°S may be reported using a UPS grid zone.
On large-scale maps an overlap of approximately 40 kilometres on either side of the meridian separating adjacent UTM grid zones is provided; such UTM-to-UTM grid zone overlaps are known as “adjacent zone overlaps”.
The origins of UTM grid zones are intentionally offset so as to ensure that the only valid coordinate values will be positive. To accomplish this, the central meridian of each UTM grid zone is assigned the “false easting” value of 500,000 metres; smaller (non-negative) values are to the west and larger values are to the east. Additionally, in the Northern Hemisphere a “false northing” of 0 metres is assigned at the equator whereas in the Southern Hemisphere 10,000,000 is assigned at the equator. Since the Northern and Southern Hemispheres are disjoint there are, in effect, 120 UTM grid zones.
The origins of UPS grid zones (at the poles) are assigned the “false easting” and “false northing” values of 2,000,000 metres. For UPS North grids, the direction of increasing northing up to 2,000,000 metres is parallel to the direction of increasing latitude along the Prime meridian; at greater than 2,000,000 meters the direction is parallel to the direction of decreasing latitude along the Prime anti-meridian.
For UPS South grids, the direction of increasing northing up to 2,000,000 metres is parallel to the direction of decreasing latitude along the Prime anti-meridian; at greater than 2,000,000 meters the direction is parallel to the direction of increasing latitude along the Prime meridian.
Positions falling along the meridian boundary of adjacent grid zones (either UTM-UTM or UTM-UPS) may be reported in whichever grid zone is most convenient. 
5.3.2.6.3	Universal Grid-based CRS
UTM-based Projected 2D CRS are identified by one of 120 URIs of the following form, where each of the 60 UTM zones is split into separate Northern Hemisphere and Southern Hemisphere grid zones:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01N
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01S
  …
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60N
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60S
UPS-based Projected 2D CRS are identified by one of two URIs distinguished by the pole at which the grid zone is specified:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSN
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSS
5.3.2.6.4	Universal Grid-based Coordinate Tuples
All UTM-based Projected 2D CRS share the following constraints:
a.	Easting shall be a real value in the range:  0 <= easting <= 1,000,000.
i.	The unit of measure is metre (a length).
b.	Northing shall be a real value in the range:  0 <= northing <= 10,000,000.
i.	The unit of measure is metre (a length).
c.	In an XML instance document this coordinate tuple is encoded as two decimal values separated by a single space character in the coordinate order of Easting and then Northing.
i.	An example location in the South Atlantic in UTM grid zone 30S, as it would appear in XML, is “307758.89 4000329.42”; note that the northing value remains positive due to the false northing of 10,000,000 for grid zones in the Southern Hemisphere.
ii.	An example location in the Barents Sea that falls along the central meridian of UTM grid zone 38N, as it would appear in XML, is “500000.00 8100702.90”.
iii.	An example location near Mt. Jara, China, that falls along a grid zone boundary is specified in UTM grid zone 47N, as it would appear in XML, as “789422.07 3322624.35” while in the adjacent UTM grid zone 48N it is specified as  “210605.28 3322623.63”; note that the easting value moves from a “eastern zone edge” to a “western zone edge”.
iv.	An example location on Victoria Island, Canada, that falls near a grid zone boundary where grid zone extension may be applied is specified in UTM grid zone 12N, as it would appear in XML, as “4000000.00 8000000.01” while in the range-extended adjacent UTM grid zone 11N it is “606004.54 8000299.42”; note that in this case the northing values are different as well as (necessarily) the easting values.
All UPS-based Projected 2D CRS share the following constraints:
a.	Easting shall be a real value in the range:  0 <= easting <= 4,000,000.
i.	The unit of measure is metre (a length).
b.	Northing shall be a real value in the range:  0 <= northing <= 4,000,000.
i.	The unit of measure is metre (a length).
c.	In an XML instance document this coordinate tuple is encoded as two decimal values separated by a single space character in the coordinate order of Easting and then Northing.
i.	An example location in the Barents Sea that falls in UPS grid zone North, as it would appear in XML, is “2320416.75 1632668.43”.
ii.	An example location in Antarctica that falls in UPS grid zone South, as it would appear in XML, is “2222979.47 1797474.90”.
5.3.2.7	Compound Geodetic 2D + Vertical CRS
5.3.2.7.1	Introduction
In this TSPI specification a Geodetic 2D CRS may be used as the first component of a compound CRS where the second component is a Vertical CRS. Most commonly the Vertical CRS will be based on the geoid, thus the third coordinate is an orthometric height or altitude; less commonly the Vertical CRS will be based on a sounding datum, in which case the third coordinate is a depth (meaning positive downwards).
This specification supports three Vertical CRS: Earth Gravitational Model 1996 (EGM96), Earth Gravitational Model 2008 (EGM08) and Mean Sea Level (MSL). These are used in the specification of corresponding Compound Geodetic 2D + Vertical CRS.
Instance documents conforming to the TSPI Schema may specify an alternative Compound Geodetic 2D + Vertical CRS if that CRS uses the MSL Vertical CRS and has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
5.3.2.7.2	Earth Gravitational Model 1996
It is a recommended practice that when a Compound Geodetic 2D + Vertical CRS is used that it be in accordance with World Geodetic System 1984 - Geographic, 2-Dimensional plus the Earth Gravitational Model 1996 (EGM96), as specified in NIMA TR8350.2 (3rd Edition, Amendment 2). This compound CRS is identified by one of two URIs depending on whether the third coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_EGM96_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_EGM96_D
5.3.2.7.3	Earth Gravitational Model 2008
It is an emerging practice that when a Compound Geodetic 2D + Vertical CRS is used that it be in accordance with World Geodetic System 1984 - Geographic, 2-Dimensional, as specified in NIMA TR8350.2 (3rd Edition, Amendment 2) plus the Earth Gravitational Model 2008 (EGM08). This compound CRS is identified by one of two URIs depending on whether the third coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_EGM08_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_EGM08_D
NGA.SIG.0007_1.0, Information Guidance for Earth Gravitational Model 2008 (EGM 2008), 15 February 2012, establishes the EGM08 as the current model for the WGS 84 EGM from which geoid heights are derived for the NSG. All previous EGMs, geoid grids, and implementations are categorized as legacy data.  Support for EGM96 implementations will continue at least until December 2019.
5.3.2.7.4	Mean Sea Level
It is a deprecated practice that when a Compound Geodetic 2D + Vertical CRS is used that it be in accordance with World Geodetic System 1984 - Geographic, 2-Dimensional, as specified in NIMA TR8350.2 (3rd Edition, Amendment 2) plus the location- and epoch-free mean sea level (MSL). This compound CRS is identified by one of two URIs depending on whether the third coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_MSL_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_MSL_D
5.3.2.7.5	Coordinate Tuples
All Compound Geodetic 2D + Vertical CRS share the following constraints:
a.	(geodetic) Latitude shall be a real value in the range:  -90° <= latitude <= +90°.
i.	North latitudes shall be positive; south latitudes shall be negative.
ii.	The unit of measure is arc degree (a planar angle).
b.	(geodetic) Longitude shall be a real value in the range:  -180° <= longitude <= +180°; note that there are two equally acceptable values of longitude for the meridian opposite the prime meridian.
● In accordance with ISO 6709:2008 it is a recommended practice that the longitude value of -180° not be used.
i.	East longitudes shall be positive; west longitudes shall be negative.
ii.	The unit of measure is arc degree (a planar angle).
c.	Height and Depth shall be real values; usually they will be non-negative.
i.	The unit of measure is metre (a length).
d.	In an XML instance document this coordinate tuple is encoded as three decimal values separated by single space characters in the coordinate order of Latitude and then Longitude and then Height or Depth.
i.	An example location in the North Sea, as it would appear in XML, is “53.809394 2.12955 7345.2”. Depending on the specified CRS this may be an atmospheric (height) or a subterranean (depth) position.
In accordance with IETF RFC 5870 the following are recommended practices:
● The (geodetic) longitude of positions reflecting the geographic poles (latitude set to -90° or 90°) SHOULD be set to "0", although consumers MUST accept any (geodetic) longitude value from -180° through 180°.
● Where the (geodetic) latitude of a position is set to either -90° or 90°, the (geodetic) longitude MUST be ignored in comparison operations ("poles case").
● A (geodetic) longitude of 180° MUST be considered equal to a (geodetic) longitude of -180° for the purpose of position comparison (“date line case”).
5.3.2.8	Compound Projected 2D + Vertical CRS
5.3.2.8.1	Introduction
In this TSPI specification a Projected 2D CRS may be used as the first component of a compound CRS where the second component is a Vertical CRS. Most commonly the Vertical CRS will be based on the geoid, thus the third coordinate is an orthometric height or altitude; less commonly the Vertical CRS will be based on a sounding datum, in which case the third coordinate is a depth (meaning positive downwards).
When a Projected 2D CRS is used in the TSPI as the basis for a Compound Projected 2D + Vertical CRS it shall be either the UTM or UPS universal grid in accordance with DMA TM8358.2, The Universal Grids: Universal Transverse Mercator (UTM) and Universal Polar Stereographic (UPS), September 1989. Non-universal grids (e.g., British National Grid, Irish Transverse Mercator Grid, Madagascar Grid, and New Zealand Grid) shall not be used.
Most commonly the datum of the Projected 2D CRS universal grid will be World Geodetic System 1984 (WGS 84), however other geodetic datums of limited geographic extent may be employed for particular purposes.
This specification supports three Vertical CRS: Earth Gravitational Model 1996, Earth Gravitational Model 2008 and Mean Sea Level. These are used in the specification of corresponding Compound Geodetic 2D + Vertical CRS.
Instance documents conforming to the TSPI Schema may specify an alternative Compound universal grid-based Projected 2D + Vertical CRS if that CRS has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
5.3.2.8.2	Earth Gravitational Model 1996
It is a recommended practice that when a Compound Projected 2D + Vertical CRS is used that it be in accordance with either the UTM or UPS universal grids plus the Earth Gravitational Model 1996 (EGM96), as specified in NIMA TR8350.2 (3rd Edition, Amendment 2). 
UTM-based Projected 2D + Vertical CRS based on EGM96 are identified by one of 240 URIs of the following form, where each of the 60 UTM zones is split into separate Northern Hemisphere and Southern Hemisphere grid zones and each is further split according to whether the third coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01N_EGM96_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01N_EGM96_D
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01S_EGM96_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01S_EGM96_D
  …
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60N_EGM96_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60N_EGM96_D
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60S_EGM96_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60S_EGM96_D
UPS-based Projected 2D + Vertical CRS based on EGM96 are identified by one of four URIs distinguished by the pole at which the grid zone is specified and whether the third coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSN_EGM96_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSN_EGM96_D
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSS_EGM96_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSS_EGM96_D
5.3.2.8.3	Earth Gravitational Model 2008
It is an emerging practice that when a Compound Projected 2D + Vertical CRS is used that it be in accordance with either the UTM or UPS universal grids plus the Earth Gravitational Model 2008 (EGM08). 
UTM-based Projected 2D + Vertical CRS based on EGM08 are identified by one of 240 URIs of the following form, where each of the 60 UTM zones is split into separate Northern Hemisphere and Southern Hemisphere grid zones and each is further split according to whether the third coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01N_EGM08_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01N_EGM08_D
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01S_EGM08_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01S_EGM08_D
  …
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60N_EGM08_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60N_EGM08_D
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60S_EGM08_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60S_EGM08_D
UPS-based Projected 2D + Vertical CRS based on EGM08 are identified by one of four URIs distinguished by the pole at which the grid zone is specified and whether the third coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSN_EGM08_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSN_EGM08_D
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSS_EGM08_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSS_EGM08_D
NGA.SIG.0007_1.0, Information Guidance for Earth Gravitational Model 2008 (EGM 2008), 15 February 2012, establishes the EGM08 as the current model for the WGS 84 EGM from which geoid heights are derived for the NSG. All previous EGMs, geoid grids, and implementations are categorized as legacy data.  Support for EGM96 implementations will continue at least until December 2019.
5.3.2.8.4	Mean Sea Level
It is a deprecated practice that when a Compound Projected 2D + Vertical CRS is used that it be in accordance with either the UTM or UPS universal grids plus the location- and epoch-free mean sea level (MSL). 
UTM-based Projected 2D + Vertical CRS based on MSL are identified by one of 240 URIs of the following form, where each of the 60 UTM zones is split into separate Northern Hemisphere and Southern Hemisphere grid zones and each is further split according to whether the third coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01N_MSL_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01N_MSL_D
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01S_MSL_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM01S_MSL_D
  …
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60N_MSL_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60N_MSL_D
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60S_MSL_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM60S_MSL_D
UPS-based Projected 2D + Vertical CRS based on MSL are identified by one of four URIs distinguished by the pole at which the grid zone is specified and whether the third coordinate is a height or depth value:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSN_MSL_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSN_MSL_D
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSS_MSL_H
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UPSS_MSL_D
5.3.2.8.5	Coordinate Tuples
All UTM-based Projected 2D + Vertical CRS share the following constraints:
a.	Easting shall be a real value in the range:  0 <= easting <= 1,000,000.
i.	The unit of measure is metre (a length).
b.	Northing shall be a real value in the range:  0 <= northing <= 10,000,000.
i.	The unit of measure is metre (a length).
c.	Height and Depth shall be real values; usually they will be non-negative.
i.	The unit of measure is metre (a length).
d.	In an XML instance document this coordinate tuple is encoded as three decimal values separated by single space characters in the coordinate order of Easting and then Northing and then Height or Depth.
i.	An example location in the South Atlantic in UTM grid zone 30S, as it would appear in XML, is “307758.89 4000329.42 130.5”; note that the northing value remains positive due to the false northing of 10,000,000 for grid zones in the Southern Hemisphere. Depending on the specified CRS this may be an atmospheric (height) or an oceanographic (depth) position.
ii.	An example location in the Barents Sea that falls along the central meridian of UTM grid zone 38N, as it would appear in XML, is “500000.00 8100702.90 130.5”. Depending on the specified CRS this may be an atmospheric (height) or an oceanographic (depth) position.
iii.	An example location near Mt. Jara, China, that falls along a grid zone boundary is specified in UTM grid zone 47N, as it would appear in XML, as “789422.07 3322624.35 5157.5” while in the adjacent UTM grid zone 48N it is “210605.28 3322623.63 5157.5”; note that the easting value moves from a “eastern zone edge” to a “western zone edge”. Depending on the specified CRS this may be an atmospheric (height) or a subterranean (depth) position.
iv.	An example location on Victoria Island, Canada, that falls near a grid zone boundary where grid zone extension may be applied is specified in UTM grid zone 12N, as it would appear in XML, as “400000.00 8000000.01 425.3” while in the range-extended adjacent UTM grid zone 11N it is “606004.54 8000299.42 425.3”; note that in this case the northing values are different as well as (necessarily) the easting values. Depending on the specified CRS this may be an atmospheric (height) or a subterranean (depth) position.
All UPS-based Projected 2D + Vertical CRS share the following constraints:
a.	Easting shall be a real value in the range:  0 <= easting <= 4,000,000.
i.	The unit of measure is metre (a length).
b.	Northing shall be a real value in the range:  0 <= northing <= 4,000,000.
i.	The unit of measure is metre (a length).
c.	Height and Depth shall be real values; usually they will be non-negative.
i.	The unit of measure is metre (a length).
d.	In an XML instance document this coordinate tuple is encoded as three decimal values separated by single space characters in the coordinate order of Easting and then Northing and then Height or Depth.
i.	An example location in the Barents Sea that falls in UPS grid zone North, as it would appear in XML, is “3320416.75 632668.43 7345.2”. Depending on the specified CRS this may be an atmospheric (height) or a subterranean (depth) position.
ii.	An example location in Antarctica that falls in UPS grid zone South, as it would appear in XML, is “2222979.47 1797474.90 2342.7”. Depending on the specified CRS this may be an air-borne (height) or a subterranean (depth) position.
5.3.3	Earth-referenced Position Presentation
5.3.3.1	Overview
Systems in the DoD/IC employ a variety of mechanisms for specifying spatial position. In this TSPI specification these are all treated as alternative presentations of a single spatial position that individually vary by their style and coordinate resolution. Each of these presentations is “alternative” in the sense that it is always the case that the “actual position” is encoded using one or more xsd:double values (see Section 5.3.1.1), and each is a “presentation” only in the sense that they encode a spatial position specification in a manner amenable to direct use in generating text-strings for use in human-computer interfaces.
This specification recognizes five alternative horizontal position presentations; these are based on the sexagesimal, grid-metre (MGRS), zone-metre (UTM/UPS), quadrangle (GEOREF) and numeric-bit styles. Two of these are DoD standard alphanumeric two-dimensional position/area reporting systems – MGRS and GEOREF. These are described in Sections 5.3.3.2.1 and 5.3.3.2.2 of this specification.
Section 5.3.3.3 specifies the five alternative horizontal position presentations supported by this specification and an integrated type for specifying exactly one of them along with the applicable CRS.
Section 5.3.5 specifies how the TSPI Schema represents horizontal coordinate resolution.
Section 5.3.3.4 specifies vertical position presentations supported by this specification.
Section 5.3.5.2 specifies how the TSPI Schema represents vertical coordinate resolution.
Section 5.3.5 specifies how the TSPI Schema encodes spatial positions using GML, including their coordinate resolution and accompanying presentation(s).
5.3.3.2	DoD-standard Horizontal Position Presentations
5.3.3.2.1	Military Grid Reference System
The UTM and UPS grids are used as the basis for the DoD-standard Military Grid Reference System (MGRS) – an alphanumeric position reporting system – as specified in DMA TM8358.1, Datums, Ellipsoids, Grids, and Grid Reference Systems, September 1990. An MGRS position is an alphanumeric version of a numerical UTM or UPS grid coordinate (see Section 5.3.2.6.2).
For convenience, in MGRS the world is generally divided into 6° by 8° geographic areas, each of which is given a unique identification, called the Grid Zone Designation.
•	For that portion of the world where the UTM grid is specified (80° south to 84° north), the UTM grid zone number is the first element of an MGRS reference.  This number sets the zone longitude limits. Zone 32 has been widened to 9° (at the expense of zone 31) between latitudes 56° and 64° to accommodate southwest Norway. Similarly, between 72° and 84°, zones 33 and 35 have been widened to 12° to accommodate Svalbard. To compensate for these 12° wide zones, zones 31 and 37 are widened to 9° and zones 32, 34 and 36 are eliminated between 72° and 84°. 
The second element of a UTM-based MGRS reference is a letter which designates a latitude band. Beginning at 80° south and proceeding northward, twenty bands are lettered C through X, omitting the letters I and O (which may be confused with the digits “1” and “0”, respectively). The bands are all 8° tall except for band X which is 12° tall. Thus, in the UTM portion of the MGRS, these first three characters (the Grid Zone Designation) designate one of 1197 regions.
•	In the Polar Regions there is no grid zone number. A single letter (equivalent in effect to the UTM-based latitude band) designates the UPS semi-circular area and hemisphere. Since the letters A, B, Y, and Z are used only in the Polar Regions, their presence in an MGRS reference with the omission of a zone number, designates that the coordinates are UPS-based. Thus, in the UPS portion of the MGRS, this first single character (the Grid Zone Designation) designates one of 4 regions.
These grid zone regions are covered by a pattern of 100,000-metre squares. Each square is identified by two letters called the 100,000-metre Square Identification. This identification is unique within the area covered by the Grid Zone Designation. Exceptions to this general rule have been made in the past to preserve the 100,000-metre identifications on maps that already exist. These 100,000-metre squares form a matrix of rows and columns. Each row and each column is sequentially lettered such that two letters provide a unique identification, within approximately 9°, for each 100,000-metre grid square. The letters I and O (which may be confused with the digits “1” and “0”, respectively) are omitted.
Within a grid square, a pair of easting-northing grid coordinate values indicate a square whose size decreases with the increase in the number of digits used in specifying the easting-northing pair. A single-digit pair indicates a 10,000 metre square whereas a five-digit pair (ten digits total) indicates a 1 metre square.
A complete MGRS coordinate of maximal resolution is 15 characters in length (13 characters in the case of a polar region) with the first three (or just one in the case of a polar region) specifying the Grid Zone Designation, the next two the 100,000-metre Square Identification, and the final 2-10 characters (always digits) the grid coordinates up to 1 metre resolution.
5.3.3.2.2	World Geographic Reference System
The World Geographic Reference System (GEOREF) is a DoD-standard used for position reporting. It is not a military grid, and therefore does not replace military grids (e.g., MGRS). It is an area-designation method used for inter-service and inter-allied position reporting for air defence and strategic air operations. Positions are expressed in a form suitable for reporting and plotting on any map or chart graduated in latitude and longitude (with Greenwich as prime meridian) regardless of map projection.
The system divides the surface of the Earth into 15° x 15° quadrangles; each quadrangle is identified by a simple systematic letter code giving positive identification with no risk of ambiguity. There are 24 longitudinal zones each of 15° width extending eastward from the 180° meridian; these zones are lettered eastwards from A to Z inclusive (omitting the letters “I” and “O”). There are 12 bands of latitude each of 15° height, extending northward from the South Pole; these bands are lettered northwards from A to M inclusive (omitting the letter “I”). Each member of the resulting set of 288 15° quadrangles is identified by two letters. The first letter is that of the 15° longitude zone and the second letter that of the 15° latitude band; for example: “MK”.
Each 15° x 15° quadrangle is further sub-divided into 15 1° zones of longitude, ordered eastward from the western meridian of the quadrangle; these 1° zones are lettered from A to Q inclusive (omitting the letters “I” and “O”). Each 15° quadrangle is also subdivided into 15 1° bands of latitude, ordered northward from the southern parallel of the quadrangle; these 1° bands are lettered northwards from A to Q inclusive (omitting the letters “I” and “O”). A nested 1° quadrangle may thus be identified by four letters; the third letter is that of the 1° longitude zone and the fourth letter that of the 1° latitude band; for example: “MKPG”.
Each 1° x 1° quadrangle is further sub-divided into 60 1’ zones of longitude, numbered eastward from its western meridian, and 60 1’ bands of latitude, numbered northward from its southern parallel. This direction of numbering is used wherever the 1° quadrangle is located; i.e., it does not vary even though the location may be west of the prime meridian or south of the equator. A unique reference defining the position of a point to a resolution of 1’ in latitude and longitude (i.e., 2 kilometres or less) can now be given by specifying four letters and four digits; for example: “MKPG1204”. The four letters identify the 1° quadrangle. The first two digits are the number of minutes of longitude by which the point lies eastward of the western meridian of the 1° quadrangle, and the last two digits are the number of minutes of latitude by which the point lies northward of the southern parallel of the 1° quadrangle. If the number of minutes is less than 10 minutes, then the first digit will be a zero and must be written, e.g., “04”.
Each of the 1° x 1° quadrangles may also be further divided into decimal parts (1/10th or 1/100th) eastward and northward. Thus, four letters and six digits will define a location to 0.1-minute resolution (6 arc seconds, approximately 185 metres or less); four letters and eight digits will define a location to 0.01-minute resolution (0.6 arc seconds, approximately 18.5 metres or less).
5.3.3.3	Horizontal Position Presentation
5.3.3.3.1	Introduction
The TSPI Schema defines the tspi-core:HorizontalPresentationType as a means for specifying one of five  supported horizontal position presentation types and specifying the applicable CRS to ensure that the horizontal position presentation is unambiguous as regards the spatial position being represented. The specified presentation type may occur one or more times – this allows the presentation of multi-position sets in a consistent manner.
Figure 2 illustrates the tspi-core:HorizontalPresentationType.
<complexType name="HorizontalPresentationType">
 <choice>
  <element name="sexagesimalLocation" type="tspi-core:SexagesimalPresentationType" 
           maxOccurs="unbounded"/>
  <element name="gridMetreLocation" type="tspi-core:GridMetrePresentationType"
           maxOccurs="unbounded"/>
  <element name="zoneMetreLocation" type="tspi-core:ZoneMetrePresentationType"
           maxOccurs="unbounded"/>
  <element name="quadrangleLocation" type="tspi-core:QuadranglePresentationType"
           maxOccurs="unbounded"/>
  <element name="numericBitLocation" type="tspi-core:NumericBitPresentationType"
           maxOccurs="unbounded"/>
 </choice>

 <!-- mandatory specification of the CRS -->
 <attribute name="srsName" type="anyURI" use="required"/>
</complexType>
Figure 2 – TSPI Horizontal Presentation Type
The following sections of this specification describe the five alternative horizontal position presentations supported by the TSPI Schema.
5.3.3.3.2	Sexagesimal
The widely employed sexagesimal position presentation is based on 60 arc seconds (") comprising an arc minute and 60 arc minutes (') comprising an arc degree (°). The presentation consists of two component strings, one each for the geodetic latitude and longitude coordinates, which are identical excepting differences in the maximum value of latitude (90°) and longitude (180°) and the allowed value of hemisphere (N/S vs. E/W).
For each coordinate there are 15 presentation components with at least two, and up to five, components that shall be employed to present a given coordinate. A coordinate tuple therefore has 30 presentation components (a separate set for the geodetic latitude and then the geodetic longitude) with at least four, and up to ten, components employed. The values for arc degrees and the hemispheres are mandatory components. Section 5.3.5.1.2 identifies the equivalent linear resolution for each applicable component.
For presentations including a fractional component the intended radix point mark is also specified.  The radix point mark  is the symbol used in numerical representations to separate the integral part of the number (to the left of the radix) from its fractional part (to the right of the radix). The radix point is usually a small dot, either placed on the baseline or halfway between the baseline and the top of the numerals. In base-10, the radix point is more commonly called the decimal point.  In many non-English speaking countries, a comma ',' is used instead of a point '.' The TSPI Schema supports the internationalization of sexagesimal presentations by allowing the radix point mark to be specified; the default is the point (“period”).
Based on the requirements of United States Message Text Format (USMTF), Table 4 summarizes the allowed combinations of the 15 presentation components and presents an example for each allowed combination. The conventional symbols for the arc degree, minute, and second are inserted for ease of comprehension.
Table 4 – Legal Single Coordinate Sexagesimal Encodings
Degrees	Decidegrees	Centidegrees	Millidegrees	Deci-Millidegrees	Microdegrees	Minutes	Deciminutes	Milliminutes	Deci-Milliminutes	Seconds	Deciseconds	Centiseconds	Milliseconds	Hemisphere	




Example
															45°N
															45.6°N
															45.64°N
															45.635°N
															45.6349°N
															45.63489°N
															45°38'N
															45°38.1'N
															45°38.09'N
															45°38.093'N
															45°38'6"N
															45°38'5.6"N
															45°38'5.60"N
															45°38'5.604"N

Figure 3 summarizes the structure of tspi-core:SexagesimalPresentationType.
<complexType name="SexagesimalPresentationType">
  <!-- Schematron assertions omitted from this illustration -->
  <sequence>
    <!-- Geodetic location in arc degrees -->
    <element name="geoDegree">
      <complexType>
        <sequence>
          <element name="latitude" type="tspi-core:GeoLatitudeDegreeType"/>
          <element name="longitude" type="tspi-core:GeoLongitudeDegreeType"/>
        </sequence>
      </complexType>
    </element>

    <!-- Geodetic location in fractional arc degrees -->
    <element name="geoDegreeFraction" minOccurs="0">
      <complexType>
        <choice>
          <element name="decidegree">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:DecaType"/>
                <element name="longitude" type="tspi-core:DecaType"/>
              </sequence>
            </complexType>
          </element>
          <element name="centidegree">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:HectoType"/>
                <element name="longitude" type="tspi-core:HectoType"/>
              </sequence>
            </complexType>
          </element>
          <element name="millidegree">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:KiloType"/>
                <element name="longitude" type="tspi-core:KiloType"/>
              </sequence>
            </complexType>
          </element>
          <element name="decimillidegree">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:DecakiloType"/>
                <element name="longitude" type="tspi-core:DecakiloType"/>
              </sequence>
            </complexType>
          </element>
          <element name="centimillidegree">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:HectokiloType"/>
                <element name="longitude" type="tspi-core:HectokiloType"/>
              </sequence>
            </complexType>
          </element>
          <element name="microdegree">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:MegaType"/>
                <element name="longitude" type="tspi-core:MegaType"/>
              </sequence>
            </complexType>
          </element>
        </choice>
      </complexType>
    </element>

    <!-- Geodetic location in arc minutes -->
    <element name="geoMinute" minOccurs="0">
      <complexType>
        <sequence>
          <element name="latitude" type="tspi-core:SexagesimalType"/>
          <element name="longitude" type="tspi-core:SexagesimalType"/>
        </sequence>
      </complexType>
    </element>

    <!-- Geodetic location in fractional arc minutes -->
    <element name="geoMinuteFraction" minOccurs="0">
      <complexType>
        <choice>
          <element name="deciminute">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:DecaType"/>
                <element name="longitude" type="tspi-core:DecaType"/>
              </sequence>
            </complexType>
          </element>
          <element name="centiminute">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:HectoType"/>
                <element name="longitude" type="tspi-core:HectoType"/>
              </sequence>
            </complexType>
          </element>
          <element name="milliminute">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:KiloType"/>
                <element name="longitude" type="tspi-core:KiloType"/>
              </sequence>
            </complexType>
          </element>
          <element name="decimilliminute">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:DecakiloType"/>
                <element name="longitude" type="tspi-core:DecakiloType"/>
              </sequence>
            </complexType>
          </element>
        </choice>
      </complexType>
    </element>

    <!-- Geodetic location in arc seconds -->
    <element name="geoSecond" minOccurs="0">
      <complexType>
        <sequence>
          <element name="latitude" type="tspi-core:SexagesimalType"/>
          <element name="longitude" type="tspi-core:SexagesimalType"/>
        </sequence>
      </complexType>
    </element>

    <!-- Geodetic location in fractional arc seconds -->
    <element name="geoSecondFraction" minOccurs="0">
      <complexType>
        <choice>
          <element name="decisecond">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:DecaType"/>
                <element name="longitude" type="tspi-core:DecaType"/>
              </sequence>
            </complexType>
          </element>
          <element name="centisecond">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:HectoType"/>
                <element name="longitude" type="tspi-core:HectoType"/>
              </sequence>
            </complexType>
          </element>
          <element name="millisecond">
            <complexType>
              <sequence>
                <element name="latitude" type="tspi-core:KiloType"/>
                <element name="longitude" type="tspi-core:KiloType"/>
              </sequence>
            </complexType>
          </element>
        </choice>
      </complexType>
    </element>
  
    <!-- Geodetic Latitude and Longitude hemispheres -->
    <element name="geoLatHemisphere" type="tspi-core:LatitudeHemisphereType"/>
    <element name="geoLongHemisphere" type="tspi-core:LongitudeHemisphereType"/>

    <!-- Internationalized radix marker -->
    <element name="radixPointMark" type="tspi-core:RadixPointMarkType" 
             minOccurs="0" default="."/>
  </sequence>
</complexType>
Figure 3 – tspi-core:SexagesimalPresentationType
The precise semantics of individual components, constraints on their domains, and co-constraints on their values are specified in the TSPI Schema files.
An example XML instance illustrating the use of tspi-core:SexagesimalPresentationType appears in Figure 14.
5.3.3.3.3	Grid-Metre
The grid-metre position presentation is based on the requirements of the MGRS position reporting system (see Section 5.3.3.2.1). Grid squares are used as a means of identifying 100,000-metre by 100,000-metre spatial regions on the Earth within which a position is specified as an easting-northing positive-offset value-pair, in metres, from the southwest corner. The presentation consists of a single component string integrating both the easting and northing coordinate values.
For each coordinate tuple there are 14 presentation components with at least three, and up to six, components that shall be employed to present a given tuple. The values for grid column/row and square column/row are mandatory components. Section 5.3.5.1.2 identifies the equivalent linear resolution for each applicable component.
Based on the requirements of United States Message Text Format (USMTF), Table 5 summarizes the allowed combinations of the 14 presentation components and presents an example for each allowed combination.
Table 5 – Legal Grid-Metre Encodings
Grid Square	Easting	Northing	






Example
Zone Column 	Zone Row	Square Column	Square Row	Decakilometre	Kilometre	Hectometre	Decametre	Metre	Decakilometre	Kilometre	Hectometre	Decametre	Metre	
														34KAB
														34KAB27
														34KAB2371
														34KAB235710
														34KAB23507109
														34KAB2350271099

Figure 4 summarizes the structure of tspi-core:GridMetrePresentationType.
<complexType name="GridMetrePresentationType">
  <!-- Schematron assertion(s) omitted from this illustration -->
  <sequence>
    <!-- Zone Designation -->
    <element name="zoneColumn" type="tspi-core:GridZoneColumnType" minOccurs="0"/>
    <element name="zoneRow" type="tspi-core:GridZoneRowType"/>

    <!-- Square Identification -->
    <element name="squareColumn" type="tspi-core:GridSquareColumnType"/>
    <element name="squareRow" type="tspi-core:GridSquareRowType"/>

    <!-- Relative location in metres -->
    <element name="relativeLocation" minOccurs="0">
      <complexType>
        <choice>
          <element name="decakilometre">
            <complexType>
              <sequence>
                <element name="easting" type="tspi-core:DecaType"/>
                <element name="northing" type="tspi-core:DecaType"/>
              </sequence>
            </complexType>
          </element>
          <element name="kilometre">
            <complexType>
              <sequence>
                <element name="easting" type="tspi-core:HectoType"/>
                <element name="northing" type="tspi-core:HectoType"/>
              </sequence>
            </complexType>
          </element>
          <element name="hectometre">
            <complexType>
              <sequence>
                <element name="easting" type="tspi-core:KiloType"/>
                <element name="northing" type="tspi-core:KiloType"/>
              </sequence>
            </complexType>
          </element>
          <element name="decametre">
            <complexType>
              <sequence>
                <element name="easting" type="tspi-core:DecakiloType"/>
                <element name="northing" type="tspi-core:DecakiloType"/>
              </sequence>
            </complexType>
          </element>
          <element name="metre">
            <complexType>
              <sequence>
                <element name="easting" type="tspi-core:HectokiloType"/>
                <element name="northing" type="tspi-core:HectokiloType"/>
              </sequence>
            </complexType>
          </element>
        </choice>
      </complexType>
    </element>
  </sequence>
</complexType>
Figure 4 – tspi-core:GridMetrePresentationType
The precise semantics of individual components, constraints on their domains, and co-constraints on their values are specified in the TSPI Schema files. Note that tspi-core:DecaType,  tspi-core:HectoType,  tspi-core:KiloType,  tspi-core:DecakiloType, and tspi-core:HectokiloType are fixed-length encodings which include leading zeros, as necessary.
An example XML instance illustrating the use tspi-core:GridMetrePresentationType appears in Figure 17.
5.3.3.3.4	Zone-Metre
The zone-metre position presentation meets the requirements of the universal grid position reporting systems based on UTM and UPS (see Sections 5.3.3.2.1 and 5.3.2.6.2). Zones and hemispheres are used as a means of identifying spatial regions on the Earth within which a position is specified as an easting-northing positive-offset value-pair, in metres, from a reference location.  The reference location is assigned a positive offset-value to ensure that all legal offset values in a zone are positive. The presentation consists of a single component string integrating both the geodetic latitude and longitude coordinate values.
For each coordinate tuple there are 5 presentation components with exactly four components that shall be employed to present a given tuple. The values for grid column/hemisphere and easting are mandatory components; one of two alternative components for northing must be employed as well. Section 5.3.5.1.2 identifies the equivalent linear resolution for each applicable component.
Based on the requirements of United States Message Text Format (USMTF), Table 6 summarizes the allowed combinations of the 5 presentation components and presents an example for each allowed combination.
Table 6 – Legal Zone-Metre Encodings
Grid Column	Hemisphere	Metre
Easting	Metre
Northing	Metre
Northing
Extended	


Example
					34N 235025   4010990
					04S 995025 10010990

Figure 5 summarizes the structure of tspi-core:ZoneMetrePresentationType.
<complexType name="ZoneMetrePresentationType">
  <sequence>
    <!-- Zone and Hemisphere Designation -->
    <element name="zoneColumn" type="tspi-core:GridZoneColumnType"/>
    <element name="hemisphere" type="tspi-core:LatitudeHemisphereType"/>

    <!-- Easting in metres -->
    <element name="metreEasting" type="tspi-core:MegaType"/>

    <!-- Northing in metres -->
    <element name="metreNorthing">
      <complexType>
        <choice>
          <element name="basicNorthing" type="tspi-core:DecamegaType">
          <element name="extendedNorthing" type="tspi-core:HectomegaExtendedType"/>
        </choice>
      </complexType>
    </element>
  </sequence>
</complexType>
Figure 5 – tspi-core:ZoneMetrePresentationType
The precise semantics of individual components, constraints on their domains, and co-constraints on their values are specified in the TSPI Schema files. Note that tspi-core:MegaType, tspi-core:DecamegaType, and tspi-core:HectomegaExtendedType are fixed-length encodings which include leading zeros, as necessary.
An example XML instance illustrating the use of tspi-core:ZoneMetrePresentationType appears in Figure 25.
5.3.3.3.5	Quadrangle
The quadrangle position presentation is based on the requirements of the GEOREF area-designation system (see Section 5.3.3.2.2). Quadrangles are used as a means of identifying 1° by 1° spatial regions which are then subdivided in accordance with sexagesimal notation based on 60 arc minutes comprising an arc degree. The presentation consists of a single component string integrating both the geodetic latitude and longitude coordinate values.
For each coordinate tuple there are 8 presentation components with at least two, and up to six, components that shall be employed to present a given tuple. The values for quadrangle and zone are mandatory components. Section 5.3.5.1.2 identifies the equivalent linear resolution for each applicable component.
Based on the requirements of United States Message Text Format (USMTF), Table 7 summarizes the allowed combinations of the 8 presentation components and presents an example for each allowed combination.
Table 7 – Legal Quadrangle Encodings
Quadrangle	Zone	Easting Minutes	Easting Deciminutes	Easting Centiminutes	Northing Minutes	Northing Deciminutes	Northing Centiminutes	




Example
								HJMN
								HJMN2541
								HJMN255418
								HJMN25504180

Figure 6 summarizes the structure of tspi-core:QuadranglePresentationType.
<complexType name="QuadranglePresentationType">
  <!-- Schematron assertion(s) omitted from this illustration -->
  <sequence>
    <!-- Quadrangle and Zone -->
    <element name="quadrangle" type="tspi-core:GeoQuadType"/>
    <element name="zone" type="tspi-core:GeoZoneType"/>

    <!-- Subzone in arc minutes -->
    <element name="subZoneMinute" minOccurs="0">
      <complexType>
        <sequence>
          <element name="eastingMinute" type="tspi-core:SexagesimalType"/>
          <element name="northingMinute" type="tspi-core:SexagesimalType"/>
        </sequence>
      </complexType>
    </element>

    <!-- Subzone in fractional arc minutes -->
    <element name="subZoneFraction" minOccurs="0">
      <complexType>
        <choice>
          <element name="deciminute">
            <complexType>
              <sequence>
                <element name="eastingDeciminute" type="tspi-core:DecaType"/>
                <element name="northingDeciminute" type="tspi-core:DecaType"/>
              </sequence>
            </complexType>
          </element>
          <element name="centiminute">
            <complexType>
              <sequence>
                <element name="eastingCentiminute" type="tspi-core:HectoType"/>
                <element name="northingCentiminute" type="tspi-core:HectoType"/>
              </sequence>
            </complexType>
          </element>
        </choice>
      </complexType>
    </element>
  </sequence>
</complexType>
Figure 6 – tspi-core:QuadranglePresentationType
The precise semantics of individual components, constraints on their domains, and co-constraints on their values are specified in the TSPI Schema files. Note that the tspi-core:DecaType and tspi-core:HectoType are fixed-length encodings which include leading zeros, as necessary.
An example XML instance illustrating the use of tspi-core:QuadranglePresentationType appears in Figure 33.
5.3.3.3.6	Numeric-Bit
Variable Message Format (VMF) encodes values of geodetic latitude and longitude as numeric data fields – multi-bit fields whose bit configurations represent actual numeric values. The least significant bit value and range are described in the applicable message description. A negative number is coded and transmitted with twos complement coding and identified by the number one in the most significant bit of the data field.
For each coordinate tuple there are 10 presentation components with exactly two components that shall be employed to present a given tuple – one for latitude and one for longitude. Section 5.3.5.1.2 identifies the equivalent linear resolution for each applicable component.
Based on the requirements of VMF, Figure 7 summarizes the structure of tspi-core:NumericBitPresentationType.
<complexType name="NumericBitPresentationType">
  <sequence>
    <choice>
      <!-- 20-bit: 90/524,287 arc degree resolution -->
      <element name="encoded20Bit">
        <complexType>
          <sequence>
            <element name="latitude" type="tspi-core:Latitude20BitType"/>
            <element name="longitude" type="tspi-core:Longitude21BitType"/>
          </sequence>
        </complexType>
      </element>
      <!-- 21-bit: 90/1,048,575 arc degree resolution -->
      <element name="encoded21Bit">
        <complexType>
          <sequence>
            <element name="latitude" type="tspi-core:Latitude21BitType"/>
            <element name="longitude" type="tspi-core:Longitude22BitType"/>
          </sequence>
        </complexType>
      </element>
      <!-- 23-bit: 90/4,194,303 arc degree resolution -->
      <element name="encoded23Bit">
        <complexType>
          <sequence>
            <element name="latitude" type="tspi-core:Latitude23BitType"/>
            <element name="longitude" type="tspi-core:Longitude24BitType"/>
          </sequence>
        </complexType>
      </element>
      <!-- 25-bit: 90/16,777,215 arc degree resolution -->
      <element name="encoded25Bit">
        <complexType>
          <sequence>
            <element name="latitude" type="tspi-core:Latitude25BitType"/>
            <element name="longitude" type="tspi-core:Longitude26BitType"/>
          </sequence>
        </complexType>
      </element>
      <!-- 31-bit: 90/1,073,741,823 arc degree resolution -->
      <element name="encoded31Bit">
        <complexType>
          <sequence>
            <element name="latitude" type="tspi-core:Latitude31BitType"/>
            <element name="longitude" type="tspi-core:Longitude32BitType"/>
          </sequence>
        </complexType>
      </element>
    </choice>
  </sequence>
</complexType>
Figure 7 – tspi-core:NumericBitPresentationType
The precise semantics of individual components, constraints on their domains, and co-constraints on their values are specified in the TSPI Schema files.
An example XML instance illustrating the use of tspi-core:NumericBitPresentationType appears in Figure 20.
5.3.3.4	Vertical Position Presentation
This TSPI specification supports the specification of elevation, height, altitude and depth in a suitable one-dimensional “vertical” frame of reference (e.g., Earth Gravitational Model 1996). Ideally these vertical positions are integrated with horizontal position information as part of a Compound CRS (see Section 5.3.2 in general and Sections 5.3.2.7 and 5.3.2.8 in particular). It is, however, often the case that many legacy DoD/IC information systems specify and communicate vertical position information separately from horizontal position information.  See Section 5.3.4 regarding the independent reporting of vertical position.
As specified in Section 5.3.2.5, this specification supports three Vertical CRS: Earth Gravitational Model 1996 (EGM96), Earth Gravitational Model 2008 (EGM08) and Mean Sea Level (MSL). For each, both height (in metres) and depth (in metres) are allowed – resulting in six distinct Vertical CRS.
In different contexts it is desirable to support the presentation of vertical position information using alternative units of measure drawn from the “length” category of mutually comparable physical quantities. These include both metric (e.g., metre and hectometre) and English (e.g., foot and hectofoot) units. In the case of the “metre” unit of measure, this identification is by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/uom/length/metre
See Section A.5.4.6 for the proper specification of URIs for units of measure in the TSPI Schema.
Also used as a basis for specifying vertical distance in the aeronautical community is the Flight Level (FL) – a surface of constant atmospheric pressure that is related to a specific world-wide fixed pressure datum (1013.25 hectoPascal)  and is separated from other such surfaces by specific pressure intervals. It is conventionally given a numerical value to the nearest 1000 feet in units of 100 feet in accordance with the structure of the International Civil Aviation Organization (ICAO) Standard Atmosphere.  For example, the 500-hPa level is written as “FL 180” where the corresponding ICAO standard height is 18,289 feet.
See Section A.5.4.4 for the proper method for specifying measures in the TSPI Schema. 
The TSPI Schema defines the tspi-core:VerticalPresentationType as a means for specifying one of three  supported vertical position presentation types and specifying the applicable CRS to ensure that the vertical position presentation is unambiguous as regards the spatial position being represented. The specified presentation type may occur one or more times – this allows the presentation of multi-position sets in a consistent manner.
Figure 8 illustrates the tspi-core:VerticalPresentationType.
<complexType name="VerticalPresentationType">
 <choice>
  <!-- Height, conventionally measured from an ellipsoid (HAE) -->
  <element name="height" type="gml:MeasureType" maxOccurs="unbounded"/>

  <!-- Altitude, conventionally measured from Mean Sea Level (MSL) or a geoid -->
  <!--   Any "length" UoM & the noncomparable UoM "flightLevel" may be used   -->
  <element name="altitude" type="gml:MeasureType" maxOccurs="unbounded"/>

  <!-- Depth, conventionally measured from Mean Sea Level (MSL) or a geoid -->
  <!--      May also be measured from a Tidal Datum or River Datum         -->
  <element name="depth" type="gml:MeasureType" maxOccurs="unbounded"/>
 </choice>

 <!-- mandatory specification of the CRS -->
 <attribute name="srsName" type="anyURI" use="required"/>
</complexType>
Figure 8 – TSPI Vertical Presentation Type
In an XML instance document the following cases might exist:
<height uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/kilofeet">18</height>

<altitude uom=" http://metadata.ces.mil/mdr/ns/GSIP/uom/noncomparable/flightLevel">180</height>

<depth uom=" http://metadata.ces.mil/mdr/ns/GSIP/uom/length/metre">60.0</height>

Note that the Flight Level unit of measure is categorized as “noncomparable” as it is not a member of the category of mutually comparable physical quantities that are “lengths”.
5.3.3.5	TSPI Presentation Elements
The TSPI Schema consolidates the presentation of horizontal and vertical presentation information into the tspi-core:presentationGroup, as illustrated in Figure 9. This model group may be used wherever it is desired that a position representation be accompanied by position presentation information.
<group name="presentationGroup">
  <sequence>
    <element name="horizPresentation" 
             type="tspi-core:HorizontalPresentationType" minOccurs="0">
             <!-- Schematron assertion(s) omitted from this illustration -->
    <element name="vertPresentation" 
             type="tspi-core:VerticalPresentationType" minOccurs="0">
             <!-- Schematron assertion(s) omitted from this illustration -->
  </sequence>
</group>
Figure 9 – TSPI Position Presentation Model Group
5.3.4	Earth-referenced Elevation, Height, Altitude and Depth
It is a recommended practice to employ either a 3D CRS or a Compound 2D + 1D CRS when the information regarding a position is sufficient to specify a CRS that has been registered in the MDR. Where the information is incomplete, the CRS has not been registered, or the context of use is such that employing a registered CRS is not feasible (or appropriate) then the TSPI Schema specifies a suitable XML type for use in specifying Earth-referenced elevation, height, altitude and depth.
As noted in Annex A.5.4.4, ISO 19136:2007 (GML) specifies the gml:MeasureType to support recording an amount encoded as a value of XML Schema xsd:double, together with a unit of measure indicated by an XML attribute uom – short for “unit of measure”. The value of the uom attribute identifies a reference system for the measured amount, usually a ratio or interval scale. Suitable units of measure for the “length” category of mutually comparable physical quantities have been registered in the DoD Data Services Environment (DSE) Metadata Registry (MDR) for use in this application.
The TSPI Schema extends this type to add an additional XML attribute to specify the datum that serves as the zero-point for the measurement. There are separate extension types for the “upward’ (elevation, height and altitude) and “downward” (depth) cases, paralleling the structure/use of the Vertical CRS (see Section 5.3.2.5). The allowed values of the verticalDatum are those well-known surfaces used by the military Services in various applications. It is mandatory that the verticalDatum XML attribute value be populated.
The TSPI Schema additionally extends this type to add an additional XML attribute to specify the resolution of the vertical position (see Section 5.3.5.2). It is optional that the verticalResolutionCategory XML attribute value be populated.
Figure 10 illustrates these aspects of the TSPI Schema that are all XML types in the ‘tspi-core’ XML namespace.
<!-- Height, conventionally measured from an ellipsoid (HAE)                -->
<!-- Altitude, conventionally measured from Mean Sea Level (MSL) or a geoid -->
<!--   Any "length" UoM & the noncomparable UoM "flightLevel" may be used   -->
<complexType name="AltitudeMeasureType">
  <simpleContent>
    <extension base="gml:MeasureType">
      <attribute name="verticalDatum" type="tspi-core:VerticalDatumType" use="required"/>
      <attribute name="verticalResolutionCategory" type="tspi-core:VerticalResolutionType" use="optional"/>
    </extension>
  </simpleContent>
</complexType>

<!-- Depth, conventionally measured from Mean Sea Level (MSL) or a geoid -->
<!--      May also be measured from a Tidal Datum or River Datum         -->
<!--      Any "length" UoM may be used                                   -->
<complexType name="DepthMeasureType">
  <simpleContent>
    <extension base="gml:MeasureType">
      <attribute name="verticalDatum" type="tspi-core:VerticalDatumType" use="required"/>
      <attribute name="verticalResolutionCategory" type="tspi-core:VerticalResolutionType" use="optional"/>
    </extension>
  </simpleContent>
</complexType>

<simpleType name="VerticalDatumType">
  <restriction base="string">
    <enumeration value="wgs84Egm96Geoid"/>
    <enumeration value="wgs84Egm08Geoid"/>
    <enumeration value="meanSeaLevel"/>
    <enumeration value="navd88"/>
    <enumeration value="ngvd29"/>
    <enumeration value="groundLevel"/>
    <enumeration value="waterLevel"/>
    <enumeration value="lowestAstronomicalTide"/>
    <enumeration value="lowestLowWaterSprings"/>
    <!-- some enumerants omitted from this illustration -->
    <enumeration value="wgs84Ellipsoid"/>
  </restriction>
</simpleType>
Figure 10 – Extending the GML Measure Type with Vertical Reference Information
5.3.5	Coordinate Resolution
5.3.5.1	Horizontal Coordinate Resolution
5.3.5.1.1	Introduction
DoD/IC information systems employ a variety of mechanisms for specifying horizontal spatial position. In this TSPI specification these are all treated as alternative presentations of a single spatial position that individually vary by their style and horizontal coordinate resolution.
Since the fundamental representation of coordinates within this specification is as a tuple of real values, these differences in presentation are not directly reflected in horizontal coordinate values. However, when coordinates have been expressed and exchanged in accordance with a specific presentation style there is necessarily an inherent style-specific limit on the horizontal resolution of those coordinates (e.g., geodetic arc minutes or decametres). It is important to capture this horizontal resolution information explicitly so that the “apparent real-valued resolution” of the resulting encoded two-dimensional coordinates in the data exchange is not misunderstood.
Table 8 illustrates the relationship between distance along a meridian or parallel on the surface of an oblate ellipsoid Earth model as measured in arc degrees and as measured in metres. An apparent “fixed coordinate resolution” specified in geodetic latitude and longitude corresponds to significant variation in “ground resolution”.
Table 8 – Ellipsoidal Distance
Parallel	Ellipsoidal Distance per 1° Latitude	Ellipsoidal Distance per 1° Longitude
0°	110,574 metres	111,320 metres
15°	110,649 metres	107,551 metres
30°	110,852 metres	96,486 metres
45°	111,132 metres	78,847 metres
60°	111,412 metres	55,800 metres
75°	111,618 metres	28,902 metres
90°	111,694 metres	0 metres

5.3.5.1.2	Resolution Values
The TSPI Schema supports the following explicit resolutions for horizontal coordinates whose unit of measure is a planar angle – geodetic latitude and longitude coordinates:
Geodetic Arc Degree	(maximum of 	111,694		metres)
Geodetic Arc Decidegree	(maximum of	   11,169	.4	metres)
Geodetic Arc Centidegree	(maximum of	1,116	.94	metres)
Geodetic Arc Millidegree	(maximum of	111	.694	metres)
Geodetic Arc Decimillidegree	(maximum of	 11	.1694	metres)
Geodetic Arc Centimillidegree	(maximum of	1	.11694	metres)
Geodetic Arc Microdegree	(maximum of	0	.111694	metres)
Geodetic Arc Minute	(maximum of	1,861	.6	metres)
Geodetic Arc Deciminute	(maximum of	186	.16	metres)
Geodetic Arc Centiminute	(maximum of	18	.616	metres)
Geodetic Arc Milliminute	(maximum of	1	.8616	metres)
Geodetic Arc Decimilliminute	(maximum of	0	.18616 	metres)
Geodetic Arc Second	(maximum of	31.	03	metres)
Geodetic Arc Decisecond	(maximum of	3	.103	metres)
Geodetic Arc Centisecond	(maximum of	0	.3103	metres)
Geodetic Arc Millisecond	(maximum of	0	.03103	metres)
Based on the requirements of Variable Message Format (VMF), the TSPI Schema supports the following explicit resolutions for horizontal coordinates whose unit of measure is a bit-encoded planar angle – geodetic latitude and longitude coordinates:
20-bit: 90/524,287	Geodetic Arc Degree	[~0.618	Arc Seconds	(maximum of	19	.17	metres)]
21-bit: 90/1,048,575	Geodetic Arc Degree	[~0.309	Arc Seconds	(maximum of	9	.587	metres)]
23-bit: 90/4,194,303	Geodetic Arc Degree	[~0.0772	Arc Seconds	(maximum of	2	.397	metres)]
25-bit: 90/16,777,215	Geodetic Arc Degree	[~0.0193	Arc Seconds	(maximum of	0	.5992	metres)] 
31-bit: 90/1,073,741,823	Geodetic Arc Degree	[~0.000302	Arc Seconds	(maximum of	0	.009362	metres)] 
The TSPI Schema supports the following explicit resolutions for horizontal coordinates whose unit of measure is a length – projection-based coordinates:
Hectokilometre	(	100,000	metres)
Decakilometre	(	10,000	metres)
Kilometre	(	1,000	metres)
Hectometre	(	100	metres)
Decametre	(	10	metres)
Metre	(	1	metre)
5.3.5.1.3	Resolution Interpretation
Not all DoD/IC information systems are careful to specify a consistent and unambiguous interpretation of the relationship between “real world location” and the corresponding “reported location”.
In general, reported locations using the sexagesimal notation are understood to be “nearest” and therefore it is assumed that the real-world value has been rounded in accordance with normal practices to a value that is allowed by the resolution of the specific sexagesimal notation employed.   For example, while the real-world value may be established to a three-digit resolution (and presumed accuracy) of 345 milliminutes, in a reporting mechanism only supporting a sexagesimal notation resolution of centiminutes the value will be 34 centiminutes. The real-world location lies within a range extending from [the reported value minus one-half of the value of the resolution of the reporting notation] to [the reported value plus one-half of the value of the resolution of the reporting notation].
In the case of the overtly similar quadrangle-based GEOREF reporting notation there is an important difference. GEOREF is an area-designation system (see Section 5.3.3.2.2) and in this system a reported “location” is the south-west corner of a cell that contains the real-world position. For example, while the real-world value may be established to a resolution of 350 centiminutes, in a reporting notation only supporting a resolution of arc minutes the reported value should be 3 arc minutes. The real-world value should properly be truncated, not rounded, when using GEOREF. Application of the “normal practice” rounding procedure would introduce a positional bias as the reported value would be 4 arc minutes – which is the south-west corner of a cell containing the values 400 … 499 centiminutes. When GEOREF is correctly employed the real-world location lies within a range extending from [the reported value] to [the reported value plus the full value of the resolution of the reporting notation].
In general, reported locations using the zone-metre notation (e.g., UTM/UPS) are understood to be “nearest” and therefore it is assumed that the real-world value has been rounded in accordance with normal practices to a value that is allowed by the resolution of the specific zone-metre notation employed  For example, while the real-world value may be established to a resolution of 355 metres in a reporting mechanism only supporting a zone-metre notation resolution of decametres, the value will be 36 decametres (rounded up). The real-world location lies within a range extending from [the reported value minus one-half of the value of the resolution of the reporting notation] to [the reported value plus one-half of the value of the resolution of the reporting notation].
In the case of the overtly similar zone-grid MGRS reporting notation there is an important difference. In this system (see Section 5.3.3.2.1) a reported “location” is the south-west corner of a cell that contains the real-world position. For example, while the real-world value may be established to a resolution of 355 metres, in a reporting mechanism only supporting a zone-grid notation resolution of hectometres the value will be 3 hectometres. The real-world value should properly be truncated, not rounded, when using MGRS. Application of the “normal practice” rounding procedure would introduce a positional bias as the reported value would be 4 hectometres (rounded up) – which is the south-west corner of a cell containing the values 400 … 499 metres. When MGRS is correctly employed the real-world location lies within a range extending from [the reported value] to [the reported value plus the full value of the resolution of the reporting notation].
Because of these ambiguities it is a recommended practice to avoid the use of “presentation locations”. Where “presentation locations” are deemed necessary then it is necessary that business rules be established to ensure that coordinates reported using these mechanisms are correctly computed.
5.3.5.2	Vertical Coordinate Resolution
DoD/IC information systems employ a variety of mechanisms for specifying vertical spatial position. In this TSPI specification these are all treated as alternative presentations of a single position that individually vary by their style and vertical coordinate resolution.
Since the fundamental representation of coordinates within this specification is as a tuple of real values, these differences in presentation are not directly reflected in vertical coordinate values. However, when coordinates have been expressed and exchanged in accordance with a specific presentation style there is necessarily an inherent style-specific limit on the vertical resolution of those coordinates (e.g., kiloyards or hectometres). It is important to capture this vertical resolution information explicitly so that the “apparent real-valued resolution” of the resulting encoded one-dimensional coordinate in the exchange data is not misunderstood.
The TSPI Schema supports the following explicit resolutions for vertical coordinates whose unit of measure is a length:
Kilometre	(	1,000	.0	metres)
Hectometre	(	100	.0	metres)
Decametre	(	10	.0	metres)
Metre	(	1	.0	metre)
Decimetre	(	0	.1	metres)
Centimetre	(	0	.01	metres)
Millimetre	(	0	.001	metres)
Nautical Mile	(	1,852	.0	metres) 
Mile (U.S. Survey)	(	1,609	.347	metres)
Statute Mile	(	1,609	.344	metres)
Kiloyard	(	914	.4	metres)
Kilofoot	(	304	.8	metres)
Hectofoot	(	30	.48	metres)
QuarterHectofoot	(	7	.62	metres)
Decafoot	(	3	.048	metres)
Fathom	(	1	.8288	metres)
Yard	(	0	.9144	metres)
Foot (U.S. Survey)	(	0	.3048006	metres)
Foot	(	0	.3048	metres)
Half-foot	(	0	.1524	metres)
Decifoot	(	0	.03048	metres)
Inch	(	0	.0254 	metres)
The TSPI Schema supports an explicit resolution for vertical coordinates whose unit of measure is a bit-encoded length:
22-bit: 10,000/1,280,000	Metre	(	0	.0078125	metres)
In addition, the TSPI Schema supports the explicit vertical resolution of “Flight Level” which is nominally equivalent to a kilofoot but is reported as equivalent to a hectofoot:
Flight Level (as reported)	(	30	.48	metres)
5.3.5.3	TSPI Resolution Elements
The TSPI Schema consolidates the representation of horizontal and vertical position resolution information into the tspi-core:resolutionGroup, as illustrated in Figure 11. This model group may be used wherever it is desired that a position representation be accompanied by position resolution information.
<group name="resolutionGroup">
  <sequence>
    <element name="horizResolutionCategory" 
             type="tspi-core:HorizontalResolutionType" minOccurs="0"/>
             <!-- Schematron assertion(s) omitted from this illustration -->
    <element name="vertResolutionCategory" 
             type="tspi-core:VerticalResolutionType" minOccurs="0"/>
             <!-- Schematron assertion(s) omitted from this illustration -->
  </sequence>
</group>

<simpleType name="HorizontalResolutionEnumerationType">
  <restriction base="string">
    <enumeration value="arcDegree"/>
    <enumeration value="arcMinute"/>
    <enumeration value="arcSecond"/>
    <enumeration value="decametre"/>
    <enumeration value="metre"/>
    <!-- some enumerants omitted from this illustration -->
  </restriction>
</simpleType>

<complexType name="HorizontalResolutionType">
  <simpleContent>
    <extension base="tspi-core:HorizontalResolutionEnumerationType">
      <attribute name="codeList" type="anyURI" use="optional"/>
      <attribute name="codeListValue" type="anyURI" use="optional"/>
    </extension>
  </simpleContent>
</complexType>

<simpleType name="VerticalResolutionEnumerationType">
  <restriction base="string">
    <enumeration value="kilometre"/>
    <enumeration value="kiloyard"/>
    <enumeration value="foot"/>
    <!-- some enumerants omitted from this illustration -->
    <enumeration value="flightLevel"/>
  </restriction>
</simpleType>

<complexType name="VerticalResolutionType">
  <simpleContent>
    <extension base="tspi-core:VerticalResolutionEnumerationType">
      <attribute name="codeList" type="anyURI" use="optional"/>
      <attribute name="codeListValue" type="anyURI" use="optional"/>
    </extension>
  </simpleContent>
</complexType>
Figure 11 – TSPI Position Resolution Model Group
Both categorical coordinate resolutions are specified as flexible enumerations (see Annex A.5.3.2). 
It is a recommended practice that the tspi-core:horizResolutionCategory is specified when the TSPI Presentation Information is employed and a horizontal two-dimensional or compound three-dimensional CRS is specified.
It is a recommended practice that the tspi-core:vertResolutionCategory is specified when the TSPI Presentation Information is employed and a vertical one-dimensional or compound three-dimensional CRS is specified.
5.3.6	Positional Uncertainty
5.3.6.1	Introduction
Assessment of the quality of spatial data includes characterization of the precision of data values as well as quantitative and qualitative estimates of the accuracy and/or uncertainty of spatial characteristics. Section 5.3.5 addressed the characterization of the resolution of the coordinate tuple specifying a position.
Several efforts have established alternative approaches.  These include IETF RFC 5870 (‘geo’ URI), UncertML (an XML schema for describing uncertain information), and NGA.STND.0012-2_1.0 NSG Metadata Foundation (NMF) – Part 2: Quality Metadata. Each is described in the following subsections.
5.3.6.2	 ‘geo’ URI
IETF RFC 5870 A Uniform Resource Identifier for Geographic Locations (’geo’ URI), develops one framework for characterizing the uncertainty of a spatial position. In it the 'u' ("uncertainty") parameter indicates the amount of uncertainty in the position as a value in metres. Where a 'geo' URI is used to identify the position of a particular object, ‘u’ indicates the uncertainty with which the identified position is known.
The 'u' parameter is optional and it can appear only once.  If ‘u’ is not specified, this indicates that uncertainty is unknown or unspecified.  If the intent is to indicate a specific point in space, uncertainty may be set to zero.  Zero uncertainty and absent uncertainty are never the same thing.
The single uncertainty value is applied to all coordinates given in the URI.
The IETF RFC notes that number of digits of the value in the 'coordinates' component must not be interpreted as an indication to uncertainty. In this TSPI specification this “digit count” information is represented as the horizontal and/or vertical position resolution (see Section 5.3.5).
5.3.6.3	UncertML
UncertML (OGC 08-122r2) is an XML schema for describing uncertain information, and which is capable of describing a range of uncertain quantities. Its descriptive capabilities range from summaries, such as simple statistics (e.g., the mean and variance of an observation), to more complex representations such as parametric distributions at each point of a regular grid, or even jointly over the entire grid.
The ISO/IEC Guide 98:1995 Guide to the expression of uncertainty in measurement (GUM)  outlines the importance of quantifying uncertainty by stating that it is “obligatory that some quantitative indication of the quality of the result be given so that those who use it can assess its reliability” when discussing observations. The guide further states that it is necessary to have a readily implemented and generally accepted procedure for characterizing the quality of a result of a measurement; however, it does not outline a mechanism for describing this information via an exchangeable medium. The GUM recommends developing a worldwide consensus on the evaluation and expression of uncertainty in measurement, not dissimilar to the International System of Units.
The UncertML standard, and its accompanying dictionary (http://dictionary.uncertml.org), is an effort to develop such a consensus.
5.3.6.4	NMF Quality Metadata
The National System for Geospatial Intelligence (NSG)  Metadata Foundation (NMF) is a profile of the conceptual schema for metadata defined by International Organization for Standardization (ISO) Technical Committee 211 (TC 211) Geographic Information / Geomantics.  Part 1 of the NMF profiles ISO 19115:2003/Cor 1:2006 to specify the minimum and recommended set of metadata elements required for the discovery and exchange of geospatial datasets in the NSG.
NGA.STND.0012-2_1.0 NSG Metadata Foundation (NMF) – Part 2: Quality Metadata extends that core to include descriptions of quality metadata associated with an NSG resource, where “quality” is defined in ISO 19101:2002 as “the totality of characteristics of a product that bear on its ability to satisfy stated and implied needs”. Data may be considered to be of high quality if it correctly represents the real-world construct to which it refers, e.g., positional accuracy.
In coordination with the finalization of NGA.STND.0012-2_1.0, a Data Quality Measures information resource is being established in the DoD Data Services Environment (DSE) Metadata Registry (MDR); Annex A.5.5 describes those resources. Its initial content is based on ISO/DIS 19157-1, Geographic information – Data quality, a consolidation and revision of ISO 19113:2002,  ISO 19114:2006  and ISO/TS 19138:2006. 
Quality Measures relevant to positional accuracy include:
•	Linear error probable (Table D.35)
•	Standard linear error (Table D.36)
•	Near certainty linear error (Table D.40)
•	Root mean square error (Table D.41)
•	Absolute linear error at 90% significance level of biased vertical data (Table D.42)
•	Absolute linear error at 90% significance level of biased vertical data (Table D.43)
•	Circular standard deviation (Table D.44)
•	Circular error probable (Table D.45)
•	Circular error at 95% significance level (Table D.47)
•	Circular near certainty error (Table D.48)
•	Absolute circular error at 90% significance level of biased data (Table D.50)
•	Absolute circular error at 90% significance level of biased data (Table D.51)
Also included are relative accuracy versions of many of these measures. Quality Measures relevant to positional uncertainty include:
•	Uncertainty ellipse (Table D.52)
•	Confidence ellipse (Table D.53)
The TSPI Schema shall only use those data quality measures that have been registered in this component of the GSIP Governance Namespace in the MDR.
[this section currently being revised in coordination with the ongoing review of the final-draft standard]
5.4	Spatial Extent
5.4.1	Introduction
The TSPI Schema specifies XML types for use in the exchange of zero-, one-, two- and three-dimensional extent (shape) information. These types are derived from the following ISO 19136:2007 (GML) and its extension OGC GML 3.3 (which defines “compact encodings” of many geometry types):  
•	gml:PointType;
•	gml:LineStringType and  gmlce:SimpleArcByCenterPointType; and
•	gml:PolygonType, gmlce:SimplePolygonType, and gmlce:SimpleRectangleType.
These are all in the substitution group of the abstract GML element gml:AbstractGeometry. Note that the gmlce:SimplePolygonType eliminates the ability to represent polygons with interior “islands” (sometimes referred to as “doughnut holes”).
The TSPI-specified extensions to these GML types are specified in the following subsections. In each case the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace. XML component definitions in the ‘tspi-core’ XML namespace shall always be used as specified without further restriction unless documented by, and accomplished using, Schematron assertions.
5.4.2	TSPI Point Position
5.4.2.1	Introduction
Systems and applications in the DoD/IC support a variety of mechanisms for specifying spatial position. In this TSPI specification these are all treated as alternative presentations of a single spatial position that individually vary by their coordinate resolution and presentation style. Since the fundamental representation of coordinates within this specification is as a tuple of real values, these differences in presentation are not directly reflected in coordinate values. However, presentation differences do directly limit the resolution of coordinates and it is desirable to capture this resolution information explicitly.
The following sections of this specification describe the profiled structure and use(s) of the:
•	gml:Point and gml:PointType with TSPI-conformant Coordinate Reference Systems (CRS);
•	tspi-core:PointType extension of gml:PointType for characterizing coordinate resolution and supporting alternative presentations.
The design pattern specified here for the 0-dimensional point position is subsequently extended and applied to one-, two- and three-dimensional representations of spatial extent in this specification.
5.4.2.2	GML Point
The XML element gml:Point and type gml:PointType (ISO 19136:2007, Clause 10.3.1) components implement ISO 19107 GM_Point (ISO 19107:2003, Clause 6.3.11), a 0-dimensional geometric primitive. A gml:Point is defined by a single coordinate tuple which is the value of its gml:pos element. The complete content model of gml:Point is as follows:
<element name="Point" type="gml:PointType"
                      substitutionGroup="gml:AbstractGeometricPrimitive"/>

<complexType name="PointType">
 <complexContent>
  <extension base=" gml:AbstractGeometricPrimitiveType">
   <sequence>
    <element ref="gml:pos"/>
    <element ref="gml:coordinates"/> 
   </sequence>
  </extension>
 </complexContent>
</complexType>

In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the spatial position defining the gml:Point is indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR). 
Figure 12 illustrates the proper specification of gml:Point instances for several of the multi-dimensional CRS types in the TSPI Schema.
<gml:Point gml:id="pointGeodetic2dExample"
           srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
	<gml:pos>53.809394 2.12955</gml:pos>
</gml:Point>

<gml:Point gml:id="pointGeodetic3dExample"
           srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_3D">
	<gml:pos>53.809394 2.12955 73.0</gml:pos>
</gml:Point>

<gml:Point gml:id="pointGeocentric3dExample"
           srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84C_3D">
	<gml:pos>3771793.97 140253.34 5124304.35</gml:pos>
</gml:Point>

<gml:Point gml:id="pointProjected2dExample"
           srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30S">
	<gml:pos>307758.89 4000329.42</gml:pos>
</gml:Point>

<gml:Point gml:id="pointGeodetic2dVertical1dExample" 
           srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_EGM96_H">
	<gml:pos>53.809394 2.12955 7345.2</gml:pos>
</gml:Point>

<gml:Point gml:id="pointProjected2dVertical1dExample" 
           srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30S_EGM96_H">
	<gml:pos>307758.89 4000329.42 130.5</gml:pos>
</gml:Point>
Figure 12 – Examples of Point Positions Specified using GML
Note that in conformance with ISO 19136:2007 (GML) a geometry element (e.g., gml:Point) shall have an identifying XML attribute (gml:id); the scope of uniqueness of the value of this attribute is the XML instance document.  The presence of this XML attribute ensures that specified geometries may be reused by reference from elsewhere within the XML instance document.
5.4.2.3	GML Point Extension
The TSPI Schema extends gml:Point to support the optional specification of coordinate resolution and position presentation information. 
Figure 13 illustrates the tspi:Point that employs these extensions. Note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace; note also that tspi:Point is in the gml:AbstractGeometricPrimitive substitution group (which in turn is in the gml:AbstractGeometry substitution group).
<element name="Point" type="tspi-core:PointType"
                      substitutionGroup="gml:AbstractGeometricPrimitive"/>

<complexType name="PointType">
  <complexContent>
    <extension base="gml:PointType">
      <sequence>
        <group ref="tspi-core:resolutionGroup"/>
        <group ref="tspi-core:presentationGroup"/>
      </sequence>
    </extension>
  </complexContent>
</complexType>
Figure 13 – Extending the GML Point to include Resolution and Presentation Information
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.2.4	Extension Example
Figure 14 illustrates an instance of a tspi:Point representing a commonly reported position – one based on the WGS 84 horizontal datum but vertically referenced to Mean Sea Level (MSL).
The reported location is 53°48'33.818"N 2°7'46.38"W with an altitude of 15000 feet; this airspace position is located in central England, roughly midway between Preston and Leeds.
The following sequence of encoding decisions is made:
1.	This constitutes a Compound Geodetic 2D + Vertical CRS, and as specified in Section 5.3.2.7 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_MSL_H
2.	The geodetic latitude and geodetic longitude are both converted to decimal degrees and the altitude is converted to metres; the resulting coordinate tuple is:
{ 53.8093938   -2.12955   4572 }
3.	The horizontal resolution is, by inspection, one thousandth of an arc second (i.e., arcMillisecond).
4.	The vertical resolution is not specifically stated therefore one can not be authoritatively specified, however for the purposes of this example we will assume that the location was reported by an aircraft pilot and such are conventionally reported in hundreds of feet (i.e., hectofoot).
5.	The CRS of the horizontal position presentation is necessarily the Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
6.	The CRS of the vertical position presentation  is necessarily a Vertical CRS, and as specified in Section 5.3.2.5 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/MSL_H
The reverse sequence of encoding decisions would be made in the case that the location was originally reported as the tuple and the corresponding horizontal and vertical position presentations were being derived.
<tspi:Point gml:id="PointGeodetic2D+VSexagesimalExample"
            srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_MSL_H">
 <gml:pos>53.8093938 -2.12955 4572</gml:pos>
 <tspi-core:horizResolutionCategory>arcMillisecond</tspi-core:horizResolutionCategory>
 <tspi-core:vertResolutionCategory>hectofoot</tspi-core:vertResolutionCategory>
 <tspi-core:horizPresentation>
 <tspi-core:sexagesimalLocation srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
   <tspi-core:geoDegree>
    <tspi-core:latitude>53</tspi-core:latitude>
    <tspi-core:longitude>002</tspi-core:longitude>
   </tspi-core:geoDegree>
   <tspi-core:geoMinute>
    <tspi-core:latitude>48</tspi-core:latitude>
    <tspi-core:longitude>07</tspi-core:longitude>
   </tspi-core:geoMinute>
   <tspi-core:geoSecond>
    <tspi-core:latitude>33</tspi-core:latitude>
    <tspi-core:longitude>46</tspi-core:longitude>
   </tspi-core:geoSecond>
   <tspi-core:geoSecondFraction>
    <tspi-core:millisecond>
     <tspi-core:latitude>818</tspi-core:latitude>
     <tspi-core:longitude>380</tspi-core:longitude>
    </tspi-core:millisecond>
   </tspi-core:geoSecondFraction>
   <tspi-core:geoLatHemisphere>north</tspi-core:geoLatHemisphere>
   <tspi-core:geoLongHemisphere>west</tspi-core:geoLongHemisphere>
   <tspi-core:radixPointMark>.</tspi-core:radixPointMark>
  </tspi-core:sexagesimalLocation>
 </tspi-core:horizPresentation>
 <tspi-core:vertPresentation srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/MSL_H">
  <tspi-core:altitude 
      uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/hectofoot">150</tspi-core:altitude>
 </tspi-core:vertPresentation>
</tspi:Point>
Figure 14 – Example of a Point Position with Sexagesimal Presentation
5.4.3	TSPI Line String
5.4.3.1	Introduction
A gml:LineString is a special curve that consists of a single segment with two or more coordinate tuples (gml:pos), with linear interpolation between them.  The content model of gml:LineString is as follows:
<element name="LineString" type="gml:LineStringType"
                           substitutionGroup="gml:AbstractCurve"/>

<complexType name="LineStringType">
 <complexContent>
  <extension base="gml:AbstractCurveType">
   <sequence>
    <element ref="gml:pos" minOccurs="2" maxOccurs="unbounded"/>
    <choice>
      <choice minOccurs="2" maxOccurs="unbounded">
        <element ref="gml:pos"/>
        <element ref="gml:pointProperty"/> 
        <element ref="gml:pointRep"/> 
      </choice>
      <element ref="gml:posList"/>
      <element ref="gml:coordinates"/> 
    </choice>
   </sequence>
  </extension>
 </complexContent>
</complexType>

In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the positions defining the gml:LineString may be indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
Figure 15 illustrates the proper specification of a gml:LineString instance for a Geodetic 2D CRS.
<gml:LineString gml:id="LineStringGeodetic2DExample"
                srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
	<gml:pos>52.0 -1.75</gml:pos>
	<gml:pos>51.25 -1.4667</gml:pos>
</gml:LineString>
Figure 15 – Example of a Line String Specified using GML
5.4.3.2	GML Line String Extension
The TSPI Schema extends gml:LineString to support the optional specification of coordinate resolution and position presentation information.
Figure 16 illustrates the tspi:LineString that employs these extensions. Note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace; also that tspi:LineString is in the tspi:AbstractCurve substitution group (which in turn is in the gml:AbstractGeometricPrimitive and then gml:AbstractGeometry substitution groups).
<element name="LineString" type="tspi-core:LineStringType" 
                           substitutionGroup="tspi:AbstractCurve"/>

<complexType name="LineStringType">
  <complexContent>
    <extension base="gml:LineStringType">
      <sequence>
        <group ref="tspi-core:resolutionGroup"/>
        <group ref="tspi-core:presentationGroup"/>
      </sequence>
    </extension>
  </complexContent>
</complexType>
Figure 16 – Extending the gml:LineString to include Resolution and Presentation Information
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.3.3	Extension Example
Figure 17 illustrates an instance of a tspi:LineString using a Geodetic 2D CRS whose grid-metre presentation supports the Military Grid Reference System (MGRS) – see Sections 5.3.3.2.1 and 5.3.3.3.3. 
The reported line is specified by three locations, which are 52°N -1°45'W, 52°5'N -1°40'W and 52°15'N -1°28'W; this roughly north-south line generally bisects the region between Bristol and London in England and is approximately 86 kilometres in length. We assume the use of WGS 84.
The following sequence of encoding decisions is made:
1.	These positions are referenced to a Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
2.	The geodetic latitudes and longitudes are converted to corresponding MGRS zone/square pairs, remembering to handle the coordinates so as to obtain the southwest corner of the applicable square. The maximally resolved relative location encoding, metre, is selected; the resulting coordinate presentations are:
{ 30U WC 85812 61776 }, { 30U WC 91362 71146 }  and { 30U XB 07011 78743 }
3.	The horizontal resolution is, by inspection, one arc minute (i.e., arcMinute).
4.	The CRS of the horizontal position presentations are a Projected 2D CRS as specified by MGRS, and as specified in Section 5.3.2.6.3 since both positions are in Zone 30 and the Northern Hemisphere it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30N
The reverse sequence of encoding decisions would be made in the case that the line string was originally reported as the presentation-set (MGRS) and the corresponding coordinate tuples were being derived. Note that in this situation it is possible that the presentation-set in MGRS is heterogenous with repect to its tspi-core:zoneColumn and/or the hemisphere of its tspi-core:zoneRow. It remains necessary to specify the single fixed CRS URI for all position presentations.
It is a recommended practice to select the presentation CRS that contains the majority of the “real world” line, noting that “majority” is based on the actual line represented by the presentation locations and not simply the set of positions that taken pairwise specify a series of connected line segments. The intent is to minimize the use of what amounts to “range extension” from the primary CRS.
The same considerations apply if the intended tspi:LineString CRS is either a Projected CRS or a Compound CRS that includes a Projected CRS component.
<tspi:LineString gml:id="LineString2DGridMetreExample" 
                 srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
  <gml:pos>52.0 -1.75</gml:pos>
  <gml:pos>52.08334 -1.6667</gml:pos>
  <gml:pos>51.25 -1.4667</gml:pos>
  <tspi-core:horizResolutionCategory>arcMinute</tspi-core:horizResolutionCategory>
  <tspi-core:horizPresentation 
             srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30N">

  <!-- first position -->
  <tspi-core:gridMetreLocation>
   <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
   <tspi-core:zoneRow>U</tspi-core:zoneRow>
   <tspi-core:squareColumn>W</tspi-core:squareColumn>
   <tspi-core:squareRow>C</tspi-core:squareRow>
   <tspi-core:relativeLocation>
    <tspi-core:metre>
     <tspi-core:easting>85812</tspi-core:easting>
     <tspi-core:northing>61776</tspi-core:northing>
    </tspi-core:metre>
   </tspi-core:relativeLocation>
  </tspi-core:gridMetreLocation>

  <!-- second position -->
  <tspi-core:gridMetreLocation>
   <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
   <tspi-core:zoneRow>U</tspi-core:zoneRow>
   <tspi-core:squareColumn>W</tspi-core:squareColumn>
   <tspi-core:squareRow>C</tspi-core:squareRow>
   <tspi-core:relativeLocation>
    <tspi-core:metre>
     <tspi-core:easting>91362</tspi-core:easting>
     <tspi-core:northing>71146</tspi-core:northing>
    </tspi-core:metre>
   </tspi-core:relativeLocation>
  </tspi-core:gridMetreLocation>

  <!-- third position -->
  <tspi-core:gridMetreLocation>
   <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
   <tspi-core:zoneRow>U</tspi-core:zoneRow>
   <tspi-core:squareColumn>X</tspi-core:squareColumn>
   <tspi-core:squareRow>B</tspi-core:squareRow>
   <tspi-core:relativeLocation>
    <tspi-core:metre>
     <tspi-core:easting>07011</tspi-core:easting>
     <tspi-core:northing>78743</tspi-core:northing>
    </tspi-core:metre>
   </tspi-core:relativeLocation>
  </tspi-core:gridMetreLocation>

 </tspi-core:horizPresentation>
</tspi:LineString>
Figure 17 – Example of a LineString Position with Grid-Metre Presentation
5.4.4	TSPI Circle
5.4.4.1	Introduction
OGC® Geography Markup Language (GML) – Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1), defines a gmlce:SimpleCircleByCenterPoint as a special case of the gml:AbstractCurve that is closed by properly specifying its start and end angles. Like the gml:ArcByCenterPoint, this representation can be used only in 2D. It extends the content model of gmlce:SimpleArcByCenterPoint by adding constraints on its start and end angles.
The content model of gmlce:SimpleArcByCenterPoint is as follows:
<element name="SimpleArcByCenterPoint" type="gmlce:SimpleArcByCenterPointType"
               substitutionGroup="gmlce:AbstractSimpleArcString"/>

<complexType name="SimpleArcByCenterPointType">
 <complexContent>
  <extension base="gml:AbstractCurveType">
   <sequence>
    <choice>
     <choice>
      <element ref="gml:pos"/>
      <element ref="gml:pointProperty"/> 
     </choice>
     <element ref="gml:posList"/>
    </choice>
    <element name="radius" type="gml:LengthType"/>
    <element name="startAngle" type="gml:AngleType"/>
    <element name="endAngle" type="gml:AngleType"/>
   </sequence>
   <attribute name="interpolation" type="gml:CurveInterpolationType"
              fixed="circularArcCenterPointWithRadius"/>
   <attribute name="numArc" type="integer" use="required" fixed="1"/>
  </extension>
 </complexContent>
</complexType>

The content model of gmlce:SimpleCircleByCenterPoint is then as follows:
<element name="SimpleCircleByCenterPoint" type="gmlce:SimpleArcByCenterPointType"
         substitutionGroup="gmlce:AbstractSimpleArcString"/>
The gmlce:radius element specifies the radius of the arc; gmlce:startAngle specifies the bearing of the arc at its start, and gmlce:endAngle specifies the bearing of the arc at its end. Start and end angles are mandatory and should not be identical, instead differing by exactly 360 arc degrees. The angles are measured counter-clockwise from the first axis of the Coordinate Reference System (CRS) and may be negatively-valued.
The unit of measure referenced by the gmlce:radius attribute uom shall be one of those registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR) as being in the ‘length‘ category of mutually comparable physical quantities; the unit of measure referenced by the gmlce:startAngle and gmlce:endAngle attribute uom shall be one of those registered  as being in the ‘planeAngle‘ category of mutually comparable physical quantities.
All curves have the XML attribute interpolation with type gml:CurveInterpolationType  specifying the curve interpolation mechanism that is used. The position of the curve is determined by the use of control points and control parameters (in this case, a center point, a radius, and two angles). gml:CurveInterpolationType is a list of codes that are used to identify the interpolation mechanism to be used; here it takes a fixed value and may be ignored in encodings.
Since this gmlce:SimpleCircleByCenterPoint is always single curve, the gml:numArc is fixed to the value "1" (and must be explicitly set in instance documents). 
In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the position defining the gml:SimpleCircleByCenterPoint may be indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
Figure 18 illustrates the proper specification of a gmlce:SimpleCircleByCenterPoint instance for a Geodetic 2D CRS. 
<gmlce:SimpleCircleByCenterPoint
       srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D"
       numArc="1">
 <gml:pos 53.81 2.10</gml:pos>
 <gmlce:radius 
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/kilometre">20</gmlce:radius>
 <gmlce:startAngle 
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/planeAngle/arcDegree">0</gmlce:startAngle>
 <gmlce:endAngle 
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/planeAngle/arcDegree">360</gmlce:endAngle>
</gmlce:SimpleCircleByCenterPoint>
Figure 18 – Example of a Simple Circle by Center Point Position Specified using GML
5.4.4.2	GML Circle by Center Point Extension
The TSPI Schema extends gmlce:SimpleCircleByCenterPoint to support the optional specification of coordinate resolution and position presentation information.
Figure 19 illustrates the tspi:Circle that employs these extensions. Note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace; also that tspi:Circle is in the tspi:AbstractCurve substitution group (which in turn is in the gml:AbstractGeometricPrimitive and then gml:AbstractGeometry substitution groups).
<element name="Circle" type="tspi-core:CircleType" 
                       substitutionGroup="gml:AbstractCurve"/>

<complexType name="CircleType">
  <complexContent>
    <extension base="gmlce:SimpleCircleByCenterpointType">
      <sequence>
        <group ref="tspi-core:resolutionGroup"/>
        <group ref="tspi-core:presentationGroup"/>
      </sequence>
    </extension>
  </complexContent>
</complexType>
Figure 19 – Extending the gml:Circle to include Resolution and Presentation Information
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.4.3	Extension Example
Figure 20 illustrates an instance of a tspi:Circle representing a commonly reported position – one based on the WGS 84 horizontal datum.
The reported location is somewhere along a circle of 40 kilometres in diameter that is centered at 53°48'35.987"N 2°5'59.995"W; this curve is located in central England, in the area between Preston and Leeds.
The following sequence of encoding decisions is made:
1.	The center position is referenced to a Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
2.	The geodetic latitude and geodetic longitude are converted to 23-bit and 24-bit representations (one of several resolution-pairs that are used in VMF messages), respectively; the resulting coordinate tuple is:
{ 2507727 8486476 }
3.	The horizontal resolution is necessarily arcDegree23Bit.
4.	The circle radius is 20 kilometres.
5.	The CRS of the horizontal position presentation is necessarily the Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
The reverse sequence of encoding decisions would be made in the case that the circle center point was originally reported as the tuple and the corresponding horizontal position presentation was being derived.
<tspi:Circle gml:id="CircleGeodetic2DNumericBitExample" 
             srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D"
             numArc="1">
 <gml:pos>53.809997 -2.10<gml:pos>
 <gmlce:radius 
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/kilometre">20</gmlce:radius>
 <gmlce:startAngle 
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/planeAngle/arcDegree">0</gmlce:startAngle>
 <gmlce:endAngle 
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/planeAngle/arcDegree">360</gmlce:endAngle>

 <tspi-core:horizResolutionCategory>arcDegree23Bit</tspi-core:horizResolutionCategory>
 <tspi-core:horizPresentation 
            srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
  <tspi-core:numericBitLocation>
   <tspi-core:encoded23Bit>
    <tspi-core:latitude>2507727</tspi-core:latitude>
    <tspi-core:longitude>8486476</tspi-core:longitude>
   </tspi-core:encoded23Bit>
  </tspi-core:numericBitLocation>
 </tspi-core:horizPresentation>
</tspi:Circle>
Figure 20 – Example of a Circle Position with Numeric-Bit Presentation
5.4.5	TSPI Ellipse
5.4.5.1	Introduction
Neither ISO 19136:2007 nor OGC® Geography Markup Language (GML) – Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1) specify an ellipse-based curve geometry, therefore the TSPI Schema develops a content model that is analagous to tspi:Circle  in the substitution group of gml:AbstractCurve (and thus the gml:AbstractGeometry substitution group); it includes support for the optional specification of coordinate resolution and position presentation information.
5.4.5.2	Content Model
Figure 32 illustrates the content model of tspi:Ellipse; note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace:
<element name="Ellipse" type="tspi-core:EllipseType" 
                        substitutionGroup="gml:AbstractCurve"/>

<complexType name="EllipseType">
 <complexContent>
  <extension base="gml:AbstractCurveType">
   <sequence>
    <choice>
      <element ref="gml:pos"/>
      <element ref="gml:pointProperty"/> 
    </choice>
    <element name="semiMajorLength" type="tspi-core:LengthType">
    <element name="semiMinorLength" type="tspi-core:LengthType">
    <element name="orientation" type="tspi-core:PlaneAngleType">
   </sequence>
  </extension>
 </complexContent>
</complexType>

Figure 21 – The tspi:Ellipse (including Resolution and Presentation Information)
A tspi:Ellipse is defined by its center point, the lengths of its major and minor axes, and the direction of its major axis.
The tspi-core:semiMajorLength element specifies one-half of the length of the major axis of the ellipse. The major axis is the longest axis of an ellipse; it passes through the two foci. The tspi-core:semiMinorLength element specifies one-half of the length of the minor axis of the ellipse. The minor axis is the shortest axis of an ellipse; it is perpendicular to the major axis.
The tspi-core:orientation element specifies the direction of the major axis of the ellipse; its value is measured counter-clockwise from the first axis of the Coordinate Reference System (CRS) and may be negatively-valued. In a Geodetic 2D CRS the value “0” would be eastwards,  the value of“90” would be northwards and the values “-90” and “270” would be southwards.
The unit of measure referenced by the tspi-core:semiMajorLength and tspi-core:semiMajorLength attribute uom shall be one of those registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR) as being in the ‘length‘ category of mutually comparable physical quantities; the unit of measure referenced by the tspi-core:orientation attribute uom shall be one of those registered  as being in the ‘planeAngle‘ category of mutually comparable physical quantities.
In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the position defining the tspi:Ellipse may be indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.5.3	Example
Figure 22 illustrates an instance of a tspi:Ellipse representing a commonly reported position – one based on the WGS 84 horizontal datum.
The reported location is somewhere along an ellipse of 10 kilometres in width, 15 kilometres in length, oriented south-southeasterly, and is centered at 53°48'35.987"N 2°5'59.995"W; this curve is located in central England, in the area between Preston and Leeds.
The following sequence of encoding decisions is made:
1.	The center position is referenced to a Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
2.	The geodetic latitude and geodetic longitude are converted to 23-bit and 24-bit representations (one of several resolution-pairs that are used in VMF messages), respectively; the resulting coordinate tuple is:
{ 2507727 8486476 }
3.	The horizontal resolution is necessarily arcDegree23Bit.
4.	The ellipse semi-major axis length is 7.5 kilometres.
5.	The ellipse semi-minor axis length is 5 kilometres.
6.	The ellipse orientation is -67.5 arcDegrees.
7.	The CRS of the horizontal position presentation is necessarily the Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
The reverse sequence of encoding decisions would be made in the case that the ellipse center point was originally reported as the tuple and the corresponding horizontal position presentation was being derived.
<tspi:Ellipse gml:id="EllipseGeodetic2DNumericBitExample" 
             srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D"
             numArc="1">
 <gml:pos>53.809997 -2.10<gml:pos>
 <tspi-core:semiMajorLength
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/kilometre">7.5</tspi-core:semiMajorLength>
 <tspi-core:semiMinorLength
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/kilometre">5</tspi-core:semiMinorLength >
 <tspi-core:orientation
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/planeAngle/arcDegree">-67.5</tspi-core:orientation>

 <tspi-core:horizResolutionCategory>arcDegree23Bit</tspi-core:horizResolutionCategory>
 <tspi-core:horizPresentation 
            srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
  <tspi-core:numericBitLocation>
   <tspi-core:encoded23Bit>
    <tspi-core:latitude>2507727</tspi-core:latitude>
    <tspi-core:longitude>8486476</tspi-core:longitude>
   </tspi-core:encoded23Bit>
  </tspi-core:numericBitLocation>
 </tspi-core:horizPresentation>
</tspi:Ellipse>
Figure 22 – Example of a Ellipse Position with Numeric-Bit Presentation
5.4.6	TSPI Polygon
5.4.6.1	Introduction
The XML element gml:Polygon and type gml:PolygonType (ISO 19136:2007, Clause 10.5.4) components implement ISO 19107 GM_Polygon (ISO 19107:2003, Clause 6.3.17.1), a special surface that is defined by a single surface patch (a homogenous portion of a surface). The boundary of this patch is coplanar and the polygon uses planar interpolation in its interior.  The elements gml:exterior and gml:interior describe the surface boundary(ies) of the polygon. A boundary of a surface consists of a number of rings. In the normal 2D case, one of these rings is distinguished as being the exterior boundary. The "interior" rings separate the surface/surface patch from the area enclosed by the rings.
The content model of gml:Polygon is as follows:
<element name="Polygon" type="gml:PolygonType" substitutionGroup="gml:AbstractSurface"/>

<complexType name="PolygonType">
 <complexContent>
  <extension base="gml:AbstractSurfaceType">
   <sequence>
    <element ref="gml:exterior" minOccurs="0”/> 
    <element ref="gml:interior" minOccurs="0" maxOccurs="unbounded"/>
   </sequence>
  </extension>
  </complexContent>
</complexType>
The elements gml:exterior and gml:interior are implemented in terms of gml:LinearRing; its content model is as follows:
<element name="LinearRing" type="gml:LinearRingType"
                           substitutionGroup="gml:AbstractRing"/>

<complexType name=" LinearRingType">
 <complexContent>
  <extension base="gml:AbstractRingType">
   <sequence>
    <choice>
      <choice minOccurs="4" maxOccurs="unbounded">
         <element ref="gml:pos"/>
         <element ref="gml:pointProperty"/> 
         <element ref="gml:pointRep"/> 
      </choice>
      <element ref="gml:posList"/>
      <element ref="gml:coordinates"/> 
    </choice>
   </sequence>
  </extension>
 </complexContent>
</complexType>
A gml:LinearRing is defined by four or more coordinate tuples (which are the values of its gml:pos elements or single gml:posList element), with linear interpolation between them; the first and last coordinates shall be coincident.
In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the positions defining the gml:Polygon may be indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
Figure 23 illustrates the proper specification of a gml:Polygon instance for a Geodetic 2D CRS.
<gml:Polygon gml:id="PolygonGeodetic2DExample"
             srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
	<gml:exterior>
		<gml:LinearRing>
			<gml:pos>51.0667 -1.8</gml:pos>
			<gml:pos>52.0 -1.75</gml:pos>
			<gml:pos>52.75 -1.2</gml:pos>
			<gml:pos>51.25 -1.4667</gml:pos>
			<gml:pos>51.0667 -1.8</gml:pos>
		</gml:LinearRing>
	</gml:exterior>
	<gml:interior>
		<gml:LinearRing>
			<gml:pos>51.19 -1.78</gml:pos>
			<gml:pos>51.9 -1.73</gml:pos>
			<gml:pos>52.6 -1.3</gml:pos>
			<gml:pos>51.25 -1.51</gml:pos>
			<gml:pos>51.19 -1.78</gml:pos>
		</gml:LinearRing>
	</gml:interior>
</gml:Polygon>
Figure 23 – Example of a Polygon Specified using GML
5.4.6.2	GML Polygon Extension
The TSPI Schema extends gml:Polygon to support the optional specification of coordinate resolution and position presentation information. Note that the horizontal presentation components shall be in 1:1 correspondence with the positions defining the exterior ring of the polygon.
Figure 24 illustrates the tspi:Polygon that employs these extensions. Note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace; also that tspi:Polygon is in the tspi:AbstractSurface substitution group (which in turn is in the gml:AbstractGeometry substitution group).
<element name="Polygon" type="tspi-core:PolygonType" 
                        substitutionGroup="tspi:AbstractSurface"/>

<complexType name="PolygonType">
  <complexContent>
    <extension base="gml:PolygonType">
      <sequence>
        <group ref="tspi-core:resolutionGroup"/>
        <group ref="tspi-core:presentationGroup"/>
      </sequence>
    </extension>
  </complexContent>
</complexType>
Figure 24 – Extending the gml:Polygon to include Resolution and Presentation Information
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.6.3	Extension Example
Figure 25 illustrates an instance of a tspi:Polygon using a Geodetic 2D CRS whose zone-metre presentation supports the UTM universal grid – see Sections 5.3.2.6.2 and 5.3.3.3.4. 
The reported polygon is specified by four locations, which are 51°4'N -1°48'W, 52°N -1°45'W, 52°45'N -1°12'W and 51°15'N -1°28'W; this trapezoidal region is located west and northwest of London, England and is approximately 187 kilometres in north-south dimension and 42 kilometres in east-west dimension. We assume the use of WGS 84. It excludes an interior trapezoidal region specified by four locations, which are 51°11.4'N -1°46.8'W, 51°54'N -1°43.8'W, 52°36'N -1°18'W and 51°15'N -1°30.6'W.
The following sequence of encoding decisions is made:
1.	These positions are referenced to a Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
2.	The geodetic latitudes and longitudes are converted to corresponding UTM easting/northing pairs; the resulting coordinate presentations share zone 30 in the northern hemisphere and their easting/northing pairs are:
Exterior: { 584082 5657923 }, { 585812 5761776 }, { 621490 5845980 } and { 607011 5678743 }
Interior: { 585255 5671661 }, { 587379 5750678 }, { 615135 5829132 } and { 603987 5678681 }
3.	The horizontal resolution is, by inspection, one arc minute (i.e., arcMinute).
4.	The CRS of the horizontal position presentations are a Projected 2D CRS as specified by UTM, and as specified in Section 5.3.2.6.3 since all positions are in Zone 30 and the Northern Hemisphere it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30N
5.	When populating the gml:LinearRing and the tspi-core:horizPresentation the first position/presentation is replicated as the last position/presentation to ensure explicit closure of the polygonal boundary (this is mandatory in GML and the position presentations follow that practice).
The reverse sequence of encoding decisions would be made in the case that the polygon was originally reported as the presentation-set (UTM) and the corresponding coordinate tuples were being derived. Note that in this situation it is possible that the presentation-set in UTM is heterogenous with repect to its tspi-core:zoneColumn and/or its tspi-core:hemisphere. It remains necessary to specify the single fixed CRS URI for all position presentations.
It is a recommended practice to select the presentation CRS that contains the majority of the “real world” polygon, noting that “majority” is based on the actual polygonal region represented by the presentation locations and not simply the set of positions that taken pairwise specify a series of connected line segments defining the boundary of the polygonal region. The intent is to minimize the use of what amounts to “range extension” from the primary CRS.
The same considerations apply if the intended tspi:Polygon CRS is either a Projected CRS or a Compound CRS that includes a Projected CRS component.
<tspi:Polygon gml:id="PolygonGeodetic2DZoneMetreExample" 
              srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
  <gml:exterior>
   <gml:LinearRing>
    <gml:pos>51.0667 -1.8</gml:pos>
    <gml:pos>52.0 -1.75</gml:pos>
    <gml:pos>52.75 -1.2</gml:pos>
    <gml:pos>51.25 -1.4667</gml:pos>
    <gml:pos>51.0667 -1.8</gml:pos>
   </gml:LinearRing>
  </gml:exterior>
  <gml:interior>
   <gml:LinearRing>
    <gml:pos>51.19 -1.78</gml:pos>
    <gml:pos>51.9 -1.73</gml:pos>
    <gml:pos>52.6 -1.3</gml:pos>
    <gml:pos>51.25 -1.51</gml:pos>
    <gml:pos>51.19 -1.78</gml:pos>
   </gml:LinearRing>
  </gml:interior>
  <tspi-core:horizResolutionCategory>arcMinute</tspi-core:horizResolutionCategory>
  <tspi-core:horizPresentation 
             srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30N">

   <!-- first position of the exterior ring -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>584082</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5657923</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

   <!-- second position of the exterior ring -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>585812</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5761776</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

   <!-- third position of the exterior ring -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>621490</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5845980</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

   <!-- fourth position of the exterior ring -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>607011</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5678743</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

   <!-- fifth (closure) position of the exterior ring -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>584082</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5657923</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

 </tspi-core:horizPresentation>
</tspi:Polygon>
Figure 25 – Example of a Polygon Position with Zone-Metre Presentation
5.4.7	TSPI Simple Polygon
5.4.7.1	Introduction
OGC® Geography Markup Language (GML) – Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1), defines a gmlce:SimplePolygon as a specialized form of the gml:Polygon that has a simplified encoding of the logically equivalent gml:Surface with a single gml:PolygonPatch as its surface patch consisting of a single gml:LinearRing as its exterior boundary and which does not have any interior boundary. The boundary of a gmlce:SimplePolygon is coplanar and the polygon uses planar interpolation in its interior.
The usage of the term “simple” here refers to a specialized polygon with a simplified encoding, which is simply connected (no interior rings) and uses a simple closed curve (no self-crossings) to represent its single boundary ring. The content model of gmlce:SimplePolygon is as follows:
<element name="SimplePolygon" type="gmlce:Simple PolygonType"
                              substitutionGroup="gmlce:AbstractSimplePolygon"/>

<complexType name="SimplePolygonType">
 <complexContent>
  <extension base="gml:AbstractSurfaceType">
   <sequence>
    <choice>
      <choice minOccurs="3" maxOccurs="unbounded">
        <element ref="gml:pos"/>
        <element ref="gml:pointProperty"/> 
      </choice>
      <element ref="gml:posList"/>
    </choice>
   </sequence>
  </extension>
  </complexContent>
</complexType>

The last coordinate does not have to repeat the first coordinate in this simplified encoding, so only three control points are required to specify a simple polygon. For this reason, the inner choice declaration above has the corresponding occurrence constraint minOccurs="3".
In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the positions defining the gmlce:SimplePolygon may be indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
Figure 26 illustrates two proper specifications of a gmlce:SimplePolygon instance for a Geodetic 2D CRS, where the second example uses gml:posList for additional compactness instead of a sequence of gml:pos.
<gmlce:SimplePolygon gml:id="SimplePolygonGeodetic2DExample"
                     srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
	<gml:pos>51.0667 -1.8</gml:pos>
	<gml:pos>52.0 -1.75</gml:pos>
	<gml:pos>52.75 -1.2</gml:pos>
</gmlce:SimplePolygon>

<gmlce:SimplePolygon gml:id="SimplePolygonGeodetic2DListExample"
                     srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
	<gml:posList>51.0667 -1.8 52.0 -1.75 52.75 -1.2</gml:posList>
</gmlce:SimplePolygon>
Figure 26 – Examples of a Simple Polygon Specified using GML 3.3
5.4.7.2	GML Simple Polygon Extension
The TSPI Schema extends gmlce:SimplePolygon to support the optional specification of coordinate resolution and position presentation information. Note that the horizontal presentation components shall be in 1:1 correspondence with the positions defining the simple polygon.
Figure 27 illustrates the tspi:SimplePolygon that employs these extensions. Note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace; also that tspi:SimplePolygon is in the tspi:AbstractSurface substitution group (which in turn is in the gml:AbstractGeometricPrimitive and then gml:AbstractGeometry substitution groups).
<element name="SimplePolygon" type="tspi-core:SimplePolygonType" 
                              substitutionGroup="tspi:AbstractSurface"/>

<complexType name="SimplePolygonType">
  <complexContent>
    <extension base="gmlce:SimplePolygonType">
      <sequence>
        <group ref="tspi-core:resolutionGroup"/>
        <group ref="tspi-core:presentationGroup"/>
      </sequence>
    </extension>
  </complexContent>
</complexType>
Figure 27 – Extending the gmlce:SimplePolygon to include Resolution and Presentation Information
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.7.3	Extension Example
Figure 28 illustrates an instance of a tspi:SimplePolygon using a Geodetic 2D CRS whose zone-metre presentation supports the UTM universal grid – see Sections 5.3.2.6.2 and 5.3.3.3.4. 
The reported polygon is specified by three locations, which are 51°4'N -1°48'W, 52°N -1°45'W, and 52°45'N -1°12'W; this triangular region is located west and northwest of London, England. We assume the use of WGS 84.
The following sequence of encoding decisions is made:
1.	These positions are referenced to a Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
2.	The geodetic latitudes and longitudes are converted to corresponding UTM column/hemisphere pairs; the resulting coordinate presentations share zone 30 in the northern hemisphere and their easting/northing pairs are:
{ 584082 5657923 }, { 585812 5761776 }, and { 621490 5845980 }
3.	The horizontal resolution is, by inspection, one arc minute (i.e., arcMinute).
4.	The CRS of the horizontal position presentations are a Projected 2D CRS as specified by UTM, and as specified in Section 5.3.2.6.3 since all positions are in Zone 30 and the Northern Hemisphere it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30N
The reverse sequence of encoding decisions would be made in the case that the polygon was originally reported as the presentation-set (UTM) and the corresponding coordinate tuples were being derived. Note that in this situation it is possible that the presentation-set in UTM is heterogenous with repect to its tspi-core:zoneColumn and/or its tspi-core:hemisphere. It remains necessary to specify the single fixed CRS URI for all position presentations.
It is a recommended practice to select the presentation CRS that contains the majority of the “real world” polygon, noting that “majority” is based on the actual polygonal region represented by the presentation locations and not simply the set of positions that taken pairwise specify a series of connected line segments defining the boundary of the polygonal region. The intent is to minimize the use of what amounts to “range extension” from the primary CRS.
The same considerations apply if the intended tspi:SimplePolygon CRS is either a Projected CRS or a Compound CRS that includes a Projected CRS component.
<tspi:SimplePolygon gml:id="SimplePolygonGeodetic2DZoneMetreExample" 
                    srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
  <gml:pos>51.0667 -1.8</gml:pos>
  <gml:pos>52.0 -1.75</gml:pos>
  <gml:pos>52.75 -1.2</gml:pos>
  <tspi-core:horizResolutionCategory>arcMinute</tspi-core:horizResolutionCategory>
  <tspi-core:horizPresentation 
             srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30N">

   <!-- first position -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>584082</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5657923</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

   <!-- second position -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>585812</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5761776</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

   <!-- third position -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>621490</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5845980</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

 </tspi-core:horizPresentation>
</tspi:SimplePolygon>
Figure 28 – Example of a Simple Polygon Position with Zone-Metre Presentation
5.4.8	TSPI Simple Rectangle
5.4.8.1	Introduction
OGC® Geography Markup Language (GML) – Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1), defines a gmlce:SimpleRectangle as a special case of the gmlce:SimplePolygon that has exactly 4 control points in its boundary encoding representing the 4 corners of the rectangle. The boundary of a  gmlce:SimpleRectangle is coplanar and the polygon uses planar interpolation in its interior.
The content model of gmlce:SimpleRectangle is as follows:
<element name="SimpleRectangle" type="gmlce:SimpleRectangleType"
                                substitutionGroup="gmlce:AbstractSimplePolygon"/>

<complexType name="SimpleRectangleType">
 <complexContent>
  <extension base="gml:AbstractSurfaceType">
   <sequence>
    <choice>
      <choice minOccurs="4" maxOccurs="4">
        <element ref="gml:pos"/>
        <element ref="gml:pointProperty"/> 
      </choice>
      <element ref="gml:posList"/>
    </choice>
   </sequence>
  </extension>
  </complexContent>
</complexType>

The last coordinate does not have to repeat the first coordinate in this simplified encoding, so only four control points are required to specify a simple rectangle. For this reason, the inner choice declaration above has the corresponding occurrence constraint minOccurs="4" and maxOccurs="4".
In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the positions defining the gmlce:SimpleRectangle may be indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
Figure 29 illustrates two proper specifications of a gmlce:SimpleRectangle instance for a Geodetic 2D CRS, where the second example uses gml:posList for additional compactness instead of a sequence of gml:pos.
<gmlce:SimpleRectangle gml:id="SimpleRectangleGeodetic2DExample"
                     srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
	<gml:pos>51.0667 -1.8</gml:pos>
	<gml:pos>52.0 -1.75</gml:pos>
	<gml:pos>52.0 -1.2</gml:pos>
	<gml:pos>51.0667 -1.2</gml:pos>
</gmlce:SimpleRectangle>

<gmlce:SimpleRectangle gml:id="SimpleRectangleGeodetic2DListExample"
                     srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
	<gml:posList>51.0667 -1.8 52.0 -1.75 52.0 -1.2 51.0667 -1.2</gml:posList>
</gmlce:SimpleRectangle>
Figure 29 – Examples of a Simple Rectangle Specified using GML 3.3
5.4.8.2	GML Simple Rectangle Extension
The TSPI Schema extends gmlce:SimpleRectangle to support the optional specification of coordinate resolution and position presentation information. Note that the horizontal presentation components shall be in 1:1 correspondence with the positions defining the rectangle.
Figure 30 illustrates the tspi:SimpleRectangle that employs these extensions. Note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace; also that tspi:SimpleRectangle is in the tspi:AbstractSurface substitution group (which in turn is in the gml:AbstractGeometricPrimitive and then gml:AbstractGeometry substitution groups).
<element name="SimpleRectangle" type="tspi-core:SimpleRectangleType" 
                                substitutionGroup="tspi:AbstractSurface"/>

<complexType name="SimpleRectangleType">
  <complexContent>
    <extension base="gmlce:SimpleRectangleType">
      <sequence>
        <group ref="tspi-core:resolutionGroup"/>
        <group ref="tspi-core:presentationGroup"/>
      </sequence>
    </extension>
  </complexContent>
</complexType>
Figure 30 – Extending the gmlce:SimpleRectangle to include Resolution and Presentation Information
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.8.3	Extension Example
Figure 31 illustrates an instance of a tspi:SimpleRectangle using a Geodetic 2D CRS whose zone-metre presentation supports the UTM universal grid – see Sections 5.3.2.6.2 and 5.3.3.3.4. 
The reported rectangle is specified by four locations, which are 51°4'N -1°48'W, 52°N -1°48'W, 52°N -1°12'W and 51°4'N -1°12'W; this rectangular region is located west and northwest of London, England. We assume the use of WGS 84.
The following sequence of encoding decisions is made:
1.	These positions are referenced to a Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
2.	The geodetic latitudes and longitudes are converted to corresponding UTM column/hemisphere pairs; the resulting coordinate presentations share zone 30 in the northern hemisphere and their easting/northing pairs are:
{ 584082 5657923 }, { 582379 5761718 }, { 623566 5762568} and { 626120 5658780 }
3.	The horizontal resolution is, by inspection, one arc minute (i.e., arcMinute).
4.	The CRS of the horizontal position presentations are a Projected 2D CRS as specified by UTM, and as specified in Section 5.3.2.6.3 since all positions are in Zone 30 and the Northern Hemisphere it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30N
The reverse sequence of encoding decisions would be made in the case that the rectangle was originally reported as the presentation-set (UTM) and the corresponding coordinate tuples were being derived. Note that in this situation it is possible that the presentation-set in UTM is heterogenous with repect to its tspi-core:zoneColumn and/or its tspi-core:hemisphere. It remains necessary to specify the single fixed CRS URI for all position presentations.
It is a recommended practice to select the presentation CRS that contains the majority of the “real world” polygon, noting that “majority” is based on the actual polygonal region represented by the presentation locations and not simply the set of positions that taken pairwise specify a series of connected line segments defining the boundary of the polygonal region. The intent is to minimize the use of what amounts to “range extension” from the primary CRS.
The same considerations apply if the intended tspi:SimpleRectangle CRS is either a Projected CRS or a Compound CRS that includes a Projected CRS component.
<tspi:SimpleRectangle gml:id="SimpleRectangleGeodetic2DZoneMetreExample" 
                      srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
  <gml:pos>51.0667 -1.8</gml:pos>
  <gml:pos>52.0 -1.75</gml:pos>
  <gml:pos>52.0 -1.2</gml:pos>
  <gml:pos>51.0667 -1.2</gml:pos>
  <tspi-core:horizResolutionCategory>arcMinute</tspi-core:horizResolutionCategory>
  <tspi-core:horizPresentation 
             srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_UTM30N">

   <!-- first position -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>584082</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5657923</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

   <!-- second position -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>582379</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5761718</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

   <!-- third position -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>623566</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5762568</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

   <!-- fourth position -->
   <tspi-core:zoneMetreLocation>
    <tspi-core:zoneColumn>30</tspi-core:zoneColumn>
    <tspi-core:hemisphere>north</tspi-core:hemisphere>
    <tspi-core:metreEasting>626120</tspi-core:metreEasting>
    <tspi-core:metreNorthing>
     <tspi-core:basicNorthing>5658783</tspi-core:basicNorthing>
    </tspi-core:metreNorthing>
   </tspi-core:zoneMetreLocation>

 </tspi-core:horizPresentation>
</tspi:SimpleRectangle>
Figure 31 – Example of a Simple Rectangle Position with Zone-Metre Presentation
5.4.9	TSPI Envelope
5.4.9.1	Introduction
The element gml:Envelope (ISO 19136:2007, Clause 10.1.4.6) implements ISO 19107 GM_Envelope (ISO 19107:2003, Clause 6.4.3), a 2-dimensional geometric primitive. The gml:Envelope defines an extent using a pair of positions defining opposite corners in a space of unlimited dimensions. The first direct position is the "lower corner" (a coordinate position consisting of all the minimal ordinates for each dimension for all positions within the envelope), the second one the "upper corner" (a coordinate position consisting of all the maximal ordinates for each dimension for all positions within the envelope).
Regardless of dimension, an envelope can be represented without ambiguity as two positions (coordinate tuples) provided the ordering of those positions adheres to the specified rule. An envelope is often referred to as a “minimum bounding box” or “rectangle”. However, such an envelope will not always specify the minimum rectangular bounding region, for example if the referenced CRS is a Geodetic CRS. Specifically, the envelope will not specify the minimum rectangular bounding region of a geometry whose set of points span the value discontinuity in an angular coordinate axis. Such axes include the Longitude and Latitude of ellipsoidal coordinate systems. Such a geometry could lie within a small region on the surface of the ellipsoid yet could appear to extend completely “around” the ellipsoid by crossing the 180th meridian or a pole.
The content model of gml:Envelope is as follows, where the lowerCorner and upperCorner XML attributes are functionally equivalent to a gml:pos:
<element name="Envelope" type="gml:EnvelopeType" substitutionGroup="gml:AbstractObject"/>

<complexType name=" EnvelopeType ">
 <choice>
  <sequence>
   <element name="lowerCorner" type="gml:DirectPositionType"/>
   <element name="upperCorner" type="gml:DirectPositionType"/>
  </sequence>
  <element ref="gml:pos" minOccurs="2" maxOccurs="2"/> 
  <element ref="gml:coordinates"/> 
 </choice> 
 <attributeGroup ref="gml:SRSReferenceGroup"/>
</complexType>

Note, however that the gml:Envelope is in the substitution group of gml:AbstractObject rather than gml:AbstractGeometry; it therefore fails to model a position as used in the TSPI.
5.4.9.2	GML Envelope Replacement
Because of shortfalls in the gml:Envelope content model with respect to TSPI requirements, the TSPI Schema develops an analogous content model in the substitution group of gml:AbstractSurface (and thus AbstractGeometry); it includes support for the optional specification of coordinate resolution and position presentation information.
In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the positions defining the tspi:Envelope may be indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
Figure 32 illustrates the tspi:Envelope. Note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace; also that tspi:Envelope is in the tspi:AbstractSurface substitution group (which in turn is in the gml:AbstractGeometricPrimitive and then gml:AbstractGeometry substitution groups).
<element name="Envelope" type="tspi-core:EnvelopeType"
                         substitutionGroup="tspi:AbstractSurface"/>

<complexType name="EnvelopeType">
  <complexContent>
    <extension base="gml:AbstractSurfaceType">
      <sequence>
        <element name="lowerCorner">
          <complexType>
            <choice>
              <element ref="gml:pos"/>
              <element ref="gml:pointProperty"/> 
            </choice>
          </complexType>
        </element>
        <element name="upperCorner“ >
          <complexType>
            <choice>
              <element ref="gml:pos"/>
              <element ref="gml:pointProperty"/>
            </choice>
          </complexType>
        </element>
        <group ref="tspi-core:resolutionGroup"/>
        <element name="horizPresentation" minOccurs="0">
          <element name="lowerCorner" type="tspi-core:HorizontalPresentationType">
          <element name="upperCorner" type="tspi-core:HorizontalPresentationType">
        </element>
        <element name="vertPresentation" minOccurs="0">
          <element name="lowerCorner" type="tspi-core:VerticalPresentationType">
          <element name="upperCorner" type="tspi-core:VerticalPresentationType">
        </element>
      </sequence>
    </extension>
  </complexContent>
</complexType>
Figure 32 – Replacing the gml:Envelope (to include Resolution and Presentation Information)
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.9.3	Extension Example
Figure 33 illustrates an instance of a tspi:Envelope using a Geodetic 2D CRS whose quadrangle presentation supports the World Geographic Reference System (GEOREF) – see Sections 5.3.3.2.2 and 5.3.3.3.5. 
The reported corners are 51°4'N -1°48'W and 52°45'N -1°12'W; this region encompasses an area of Wiltshire, England. We assume the use of WGS 84.
The following sequence of encoding decisions is made:
1.	These positions are referenced to a Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
2.	The geodetic latitudes and longitudes are converted to corresponding quadrangle/zone pairs, remembering to handle the coordinates so as to obtain the southwest corner of the applicable zone. The remaining offsets are integral values in arc minutes; the resulting coordinate presentations are:
{ MKPG1204 } and { MKPH4845 }
3.	The horizontal resolution is, by inspection, one arc minute (i.e., arcMinute).
4.	The CRS of the horizontal position presentation is necessarily the same Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
The reverse sequence of encoding decisions would be made in the case that the envelope was originally reported as the presentation-pair (GEOREF) and the corresponding coordinate tuples were being derived.
<tspi:Envelope srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
  <tspi-core:lowerCorner>50.067 -1.80</tspi-core:lowerCorner>
  <tspi-core:upperCorner>52.750 -1.20</tspi-core:upperCorner>

  <tspi-core:horizResolutionCategory>arcMinute</tspi-core:horizResolutionCategory>
  <tspi-core:horizPresentation>

   <tspi-core:lowerCorner srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
    <tspi-core:quadrangleLocation>
     <tspi-core:quadrangle>MK</tspi-core:quadrangle>
     <tspi-core:zone>PG</tspi-core:zone>
     <tspi-core:subZoneMinute>
      <tspi-core:eastingMinute>12</tspi-core:eastingMinute>
      <tspi-core:northingMinute>04</tspi-core:northingMinute>
     </tspi-core:subZoneMinute>
    </tspi-core:quadrangleLocation>
   </tspi-core:lowerCorner>

   <tspi-core:upperCorner srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
    <tspi-core:quadrangleLocation>
     <tspi-core:quadrangle>MK</tspi-core:quadrangle>
     <tspi-core:zone>PH</tspi-core:zone>
     <tspi-core:subZoneMinute>
      <tspi-core:eastingMinute>45</tspi-core:eastingMinute>
      <tspi-core:northingMinute>48</tspi-core:northingMinute>
     </tspi-core:subZoneMinute>
    </tspi-core:quadrangleLocation>
   </tspi-core:upperCorner>

 </tspi-core:horizPresentation>
</tspi:Envelope>
Figure 33 – Example of an Envelope Position with Quadrangle Presentation
5.4.10	TSPI Circular Surface
5.4.10.1	Introduction
Neither ISO 19136:2007 nor OGC® Geography Markup Language (GML) – Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1) specify a circular surface geometry, therefore the TSPI Schema develops a content model that is analagous to tspi:Circle but within in the substitution group of gml:AbstractSurface (and thus the gml:AbstractGeometry substitution group);  it includes support for the optional specification of coordinate resolution and position presentation information.
5.4.10.2	Content Model
Figure 34 illustrates the content model of tspi:CircularSurface; note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace:
<element name="CircularSurface" type="tspi-core:CircularSurfaceType" 
                                substitutionGroup="gml:AbstractSurface"/>

<complexType name="CircularSurfaceType">
 <complexContent>
  <extension base="gml:AbstractSurfaceType">
   <sequence>
    <choice>
      <element ref="gml:pos"/>
      <element ref="gml:pointProperty"/> 
    </choice>
    <element name="radius" type="tspi-core:LengthType">
   </sequence>
  </extension>
 </complexContent>
</complexType>

Figure 34 – The tspi:CircularSurface (including Resolution and Presentation Information)
A tspi:CircularSurface is defined by its center point and radius.
The unit of measure referenced by the tspi-core:radius attribute uom shall be one of those registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR) as being in the ‘length‘ category of mutually comparable physical quantities.
In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the position defining the tspi:CircularSurface may be indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.10.3	Example
Figure 35 illustrates an instance of a tspi:CircularSurface representing a commonly reported position – one based on the WGS 84 horizontal datum.
The reported location is somewhere within a circle of 40 kilometres in diameter that is centered at 53°48'35.987"N 2°5'59.995"W; this region is located in central England, in the area between Preston and Leeds.
The following sequence of encoding decisions is made:
1.	The center position is referenced to a Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
2.	The geodetic latitude and geodetic longitude are converted to 23-bit and 24-bit representations (one of several resolution-pairs that are used in VMF messages), respectively; the resulting coordinate tuple is:
{ 2507727 8486476 }
3.	The horizontal resolution is necessarily arcDegree23Bit.
4.	The circle radius is 20 kilometres.
5.	The CRS of the horizontal position presentation is necessarily the Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
The reverse sequence of encoding decisions would be made in the case that the circle center point was originally reported as the tuple and the corresponding horizontal position presentation was being derived.
<tspi:CircularSurface gml:id="CircularSurfaceGeodetic2DNumericBitExample" 
             srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
 <gml:pos>53.809997 -2.10<gml:pos>
 <tspi-core:radius 
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/kilometre">20</tspi-core:radius>

 <tspi-core:horizResolutionCategory>arcDegree23Bit</tspi-core:horizResolutionCategory>
 <tspi-core:horizPresentation 
            srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
  <tspi-core:numericBitLocation>
   <tspi-core:encoded23Bit>
    <tspi-core:latitude>2507727</tspi-core:latitude>
    <tspi-core:longitude>8486476</tspi-core:longitude>
   </tspi-core:encoded23Bit>
  </tspi-core:numericBitLocation>
 </tspi-core:horizPresentation>
</tspi:CircularSurface>
Figure 35 – Example of a CircularSurface Position with Numeric-Bit Presentation
5.4.11	TSPI Elliptical Surface
5.4.11.1	Introduction
Neither ISO 19136:2007 nor OGC® Geography Markup Language (GML) – Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1) specify an elliptical surface geometry, therefore the TSPI Schema develops a content model that is analagous to tspi:Ellipse but within in the substitution group of gml:AbstractSurface (and thus the gml:AbstractGeometry substitution group);  it includes support for the optional specification of coordinate resolution and position presentation information.
5.4.11.2	Content Model
Figure 32 illustrates the content model of tspi:EllipticalSurface; note that the underlying XML type is in the ‘tspi-core’ XML namespace whereas the XML element is in the ‘tspi’ XML namespace:
<element name="EllipticalSurface" type="tspi-core:EllipticalSurfaceType" 
                                  substitutionGroup="gml:AbstractSurface"/>

<complexType name="EllipticalSurfaceType">
 <complexContent>
  <extension base="gml:AbstractSurfaceType">
   <sequence>
    <choice>
      <element ref="gml:pos"/>
      <element ref="gml:pointProperty"/> 
    </choice>
    <element name="semiMajorLength" type="tspi-core:LengthType">
    <element name="semiMinorLength" type="tspi-core:LengthType">
    <element name="orientation" type="tspi-core:PlaneAngleType">
   </sequence>
  </extension>
 </complexContent>
</complexType>

Figure 36 – The tspi:EllipticalSurface (including Resolution and Presentation Information)
A tspi:EllipticalSurface is defined by its center point, the lengths of its major and minor axes, and the direction of its major axis.
The tspi-core:semiMajorLength element specifies one-half of the length of the major axis of the ellipse. The major axis is the longest axis of an ellipse; it passes through the two foci. The tspi-core:semiMinorLength element specifies one-half of the length of the minor axis of the ellipse. The minor axis is the shortest axis of an ellipse; it is perpendicular to the major axis.
The tspi-core:orientation element specifies the direction of the major axis of the ellipse; its value is measured counter-clockwise from the first axis of the Coordinate Reference System (CRS) and may be negatively-valued. In a Geodetic 2D CRS the value “0” would be eastwards,  the value of“90” would be northwards and the values “-90” and “270” would be southwards.
The unit of measure referenced by the tspi-core:semiMajorLength and tspi-core:semiMajorLength attribute uom shall be one of those registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR) as being in the ‘length‘ category of mutually comparable physical quantities; the unit of measure referenced by the tspi-core:orientation attribute uom shall be one of those registered  as being in the ‘planeAngle‘ category of mutually comparable physical quantities.
In common with all geometry elements derived from gml:AbstractGeometryType, the CRS used for the position defining the tspi:EllipticalSurface may be indicated using the optional XML attribute srsName (defined as a URI). The srsName attribute shall be populated with a valid CRS reference that has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
It is a recommended practice that Flight Level not be used as a basis for a Vertical Datum in specifying a three-dimensional CRS, however this specification does support this use. Instead, it is a recommended practice that a 2D CRS be employed and the vertical position be separately represented (see Section 5.3.4 ).
5.4.11.3	Example
Figure 37 illustrates an instance of a tspi:Ellipse representing a commonly reported position – one based on the WGS 84 horizontal datum.
The reported location is somewhere within an ellipse of 10 kilometres in width, 15 kilometres in length, oriented south-southeasterly, and is centered at 53°48'35.987"N 2°5'59.995"W; this region is located in central England, roughly midway between Preston and Leeds.
The following sequence of encoding decisions is made:
1.	The center position is referenced to a Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
2.	The geodetic latitude and geodetic longitude are converted to 23-bit and 24-bit representations (one of several resolution-pairs that are used in VMF messages), respectively; the resulting coordinate tuple is:
{ 2507727 8486476 }
3.	The horizontal resolution is necessarily arcDegree23Bit.
4.	The ellipse semi-major axis length is 7.5 kilometres.
5.	The ellipse semi-minor axis length is 5 kilometres.
6.	The ellipse orientation is -67.5 arcDegrees.
7.	The CRS of the horizontal position presentation is necessarily the Geodetic 2D CRS, and as specified in Section 5.3.2.2 it is identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
The reverse sequence of encoding decisions would be made in the case that the ellipse center point was originally reported as the tuple and the corresponding horizontal position presentation was being derived.
<tspi:EllipticalSurface gml:id="EllipseGeodetic2DNumericBitExample" 
             srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D"
             numArc="1">
 <gml:pos>53.809997 -2.10<gml:pos>
 <tspi-core:semiMajorLength
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/kilometre">7.5</tspi-core:semiMajorLength>
 <tspi-core:semiMinorLength
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/kilometre">5</tspi-core:semiMinorLength >
 <tspi-core:orientation
     uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/planeAngle/arcDegree">-67.5</tspi-core:orientation>

 <tspi-core:horizResolutionCategory>arcDegree23Bit</tspi-core:horizResolutionCategory>
 <tspi-core:horizPresentation 
            srsName="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D">
  <tspi-core:numericBitLocation>
   <tspi-core:encoded23Bit>
    <tspi-core:latitude>2507727</tspi-core:latitude>
    <tspi-core:longitude>8486476</tspi-core:longitude>
   </tspi-core:encoded23Bit>
  </tspi-core:numericBitLocation>
 </tspi-core:horizPresentation>
</tspi:EllipticalSurface>
Figure 37 – Example of a Elliptical Surface Position with Numeric-Bit Presentation
5.5	Spatial Relations
5.5.1	Measured Direction
This TSPI specification supports specification of horizontal direction (bearing or heading) between two positions in a suitable frame of reference. It does so by extending gml:MeasureType(see Annex A.5.4.4) to support recording an amount encoded as a value of XML Schema xsd:double, together with a unit of measure indicated by an XML attribute uom – short for “unit of measure”. The value of the uom attribute identifies a reference system for the measured amount, usually a ratio or interval scale. Suitable units of measure for the “plane angle” category of mutually comparable physical quantities have been registered in the DoD Data Services Environment (DSE) Metadata Registry (MDR) for use in this application.
The TSPI Schema extends this type to add an additional XML attribute to specify the datum that serves as the zero-point for the angular measurement. The allowed values of the referenceDatum are those used by the military Services in various applications. The measured direction with respect to this reference direction is:
•	located in the horizontal plane, and
•	positive in a clockwise direction as viewed from “above”.
Figure 38 illustrates this aspect of the TSPI Schema.
<complexType name="DirectionMeasureType">
  <simpleContent>
    <extension base="gml:MeasureType">
      <attribute name="referenceDatum" type="tspi-core:DirectionDatumType" use="required"/>
    </extension>
  </simpleContent>
</complexType>

<simpleType name="DirectionDatumType">
  <restriction base="string">
    <enumeration value="geodetic"/>
    <enumeration value="magnetic"/>
    <enumeration value="militaryGrid"/>
    <enumeration value="relative"/>
  </restriction>
</simpleType>
Figure 38 – Extending the GML Measure Type with an Angle Reference Datum
5.5.2	Cardinal Direction
In some cases only a rough indication of horizontal direction (bearing or heading) is required. The TSPI Schema specifies an alternative to the tspi-core:DirectionMeasureType that replaces the uom and measured value with an enumeration based on the cardinal points of the compass. Figure 39 illustrates this aspect of the TSPI.
<complexType name="CardinalDirectionType">
  <simpleContent>
    <extension base="tspi-core:CompassDirectionType">
      <attribute name="referenceDatum" type="tspi-core:DirectionDatumType" use="required"/> 
    </extension>
  </simpleContent>
</complexType>

<simpleType name="CompassDirectionType">
  <restriction base="string">
    <enumeration value="north"/>
    <enumeration value="northNortheast"/>
    <enumeration value="northeast"/>
    <enumeration value="eastNortheast"/>
    <!-- some enumerants omitted from this illustration -->
    <enumeration value="noInformation"/>
  </restriction>
</simpleType>
Figure 39 – Cardinal Directions with an Angle Reference Datum
5.5.3	Topology
This TSPI specification does not support topologic relations between/among spatial extents (shapes).
5.6	Spatial Measures
This TSPI specification supports spatial measures (“size”: e.g., length, width, height, depth, radius; “direction”: e.g., vertical angle) in a suitable frame of reference. It does so by extending gml:MeasureType(see Annex A.5.4.4).
The TSPI Schema defines a set of specific measure types as limited extensions of gml:MeasureType. A prototypical definition is illustrated in Figure 40; this particular content model supports the description of a length (or distance) quantity, with its unit. The unit of measure referenced by uom shall be suitable for a length, e.g., metre or foot.
<complexType name="LengthType">
  <annotation>
    <appinfo>
      <sch:pattern id="LengthType_AllowableUOM">
        <sch:rule context="tspi-core:LengthType">
          <sch:assert test="starts-with(@uom, concat($GSIP, '/uom/length'))">
            The UOM must be from the set for the physical quantity 'length' that is that is registered in the MDR GSIP Governance Namespace.</sch:assert>
          <sch:assert test="document(@uom)">
            The specified unit of measure must reference a net-accessible resource in the MDR GSIP Governance Namespace.</sch:assert>
          <!-- Verify that the content of the resource matches the instance document -->
          <sch:assert test="concat(concat(substring-before(@uom, 'uom/'),'uom/'),substring-before(substring-after(@uom, 'uom/'),'/')) = document(@uom)//gml:identifier/@codeSpace">
            The body of the uom must match the codeSpace of the identifier in the resource.</sch:assert>
          <sch:assert test="substring-after(substring-after(@uom, 'uom/'),'/') = document(@uom)//gml:identifier">
            The tail of the uom ('<sch:value-of select="substring-after(substring-after(@uom, 'uom/'),'/')"/>') must match the value of the identifier in the resource.</sch:assert>
        </sch:rule>
      </sch:pattern>
    </appinfo>
  </annotation>
  <simpleContent>
    <extension base="gml:MeasureType"/>
  </simpleContent>
</complexType>
Figure 40 – Example Length Type Schema Fragment
Other TSPI measure types that are defined following this pattern include: tspi-core:AreaType, tspi-core:VolumeType, and tspi-core:PlaneAngleType.
For example, an XML schema may contain element declarations using these types, as follows: 
<element name="height" type="tspi-core:LengthType"/>
<element name="floorCover" type="tspi-core:AreaType"/>
<element name="tankCapacity" type="tspi-core:VolumeType"/>
<element name="barrelElevation" type="tspi-core:PlaneAngleType"/>

Elements corresponding to these might appear in an XML instance document as follows:
<height
   uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/length/metre">1.76</height>
<floorCover 
   uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/area/squareFoot">550</floorCover>
<tankCapacity 
   uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/area/usGallon">80</tankCapacity>
<barrelElevation 
   uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/planeAngle/arcDegree">50.6</ 
   barrelElevation>
5.7	Spatial Change
This TSPI specification supports measures of rates of change in spatial characteristics (e.g., linear speed, angular velocity, acceleration) in a suitable frame of reference. It does so by extending gml:MeasureType(see Annex A.5.4.4).
The TSPI Schema defines a set of specific measure types as limited extensions of gml:MeasureType using the method specified in Section 5.6. Types that are defined following this pattern are: tspi-core:SpeedType.
For example, an XML schema may contain an element declaration using this type: 
<element name="averageAdvanceRate" type="tspi-core:SpeedType"/>

An element corresponding to this might appear in an XML instance document as follows:
<averageAdvanceRate 
   uom="http://metadata.ces.mil/mdr/ns/GSIP/uom/speed/milesPerHour">23.6</ 
   averageAdvanceRate>
5.8	Spatial Position Extension
5.8.1	Introduction
The TSPI Schema includes the ‘tspi-ext’ XML namespace as a basis for extension to include additional representations for spatial position. It is populated with initial high-value extensions, but is dynamically maintained on the MDR. Its use is conditional on the requirements of a given system/application and its accompanying business requirements.
Informative Annex E describes the procedures to be followed when extending the TSPI through a process of registering new XML components in the ‘tspi-ext’ XML namespace.
All registered extensions for spatial position shall meet the requirements specified by ISO 19136:2007 (GML):
21.4.2.1 User-defined geometry types
Authors of application schemas may create their own geometry types if GML lacks the desired construct. To do this, authors shall ensure that the object elements of these concrete geometry and geometry collection types are in the substitution group (either directly or indirectly) of the corresponding GML object element: gml:AbstractGeometry.
EXAMPLE The following element and complex type definition in an application schema extends gml:Point and adds a bearing (e.g. for the orientation of a symbol in portrayal).
<element name="PointWithBearing" type="ex:PointWithBearingType" substitutionGroup="gml:Point">
<complexType name="PointWithBearingType">
    <complexContent>
       <extension base="gml:PointType">
          <sequence>
             <element name="bearing" type="gml:AngleType"/>
          </sequence>
       </extension>
    </complexContent>
</complexType>
Any user-defined geometry subtypes shall inherit the elements and attributes of the base GML geometry types without restriction, but may extend these base types to meet application requirements, such as providing a finer degree of interoperability with legacy systems and data sets.
All rules specified in Clause 7, Clause 10, 10.5.10 and Clause 11 shall be followed.
21.4.2.2 User-defined geometry property types
Furthermore, authors of application schemas may create their own geometry property types that encapsulate geometry types which are defined in Clause 10, 10.5.10 or Clause 11 or which they have defined in accordance with 21.4.2.1. They shall ensure that these properties follow the pattern used by gml:GeometryPropertyType for standard properties and gml:GeometryArrayPropertyType for array properties. The target type shall be a bona fide geometry object element.
A geometry property type may be a restriction of gml:GeometryPropertyType, but this is not a requirement. Nevertheless, every geometry property shall follow the pattern of this type. An application schema may support the choice between an inline or a by-reference semantic or it may restrict the use to either inline (prohibit the use of the Xlink attributes) or by-reference (prohibit the containment of the geometry in the feature).
A geometry array property type may be a restriction of gml:GeometryArrayPropertyType, but this is not a requirement. Nevertheless, every geometry property shall follow the pattern of this type. All geometry elements in the array are contained inline in the containing object, only inline semantics is supported by array properties.
EXAMPLE The following complex type definitions in an application schema define a "standard" property type for a user-defined geometry type and an array property type for the same geometry type. 
<complexType name="MyGeometryPropertyType">
    <sequence>
       <element ref="foo:PointWithBearingType" minOccurs="0"/>
    </sequence>
    <attributeGroup ref="gml:AssociationAttributeGroup" />
    <attributeGroup ref="gml:OwnershipAttributeGroup" />
 </complexType>
 <complexType name="MyGeometryArrayPropertyType">
    <sequence>
       <element ref="foo:PointWithBearingType" minOccurs="0" maxOccurs="unbounded" />
    </sequence>
 </complexType>
All registered extensions for spatial position shall support the optional specification of coordinate resolution (see Section 5.3.5) and position presentation (see Section 5.3.3) information.
All registered extensions for spatial position shall use <annotation> to document all elements and types, as well as the inclusion of comments as appropriate, to ensure that all technical aspects of the extension are clear to potential users.
The following sections document current community-specific representations for spatial position in the ‘tspi-ext’ XML namespace.
5.8.2	CRS-restricted Point (WGS84E_3D)
5.8.2.1	Introduction
In some data-exchange environments it is desirable to employ Efficient XML Interchange (EXI) in order to achieve  efficient encodings of XML event streams.  EXI employs a schema-aware processing strategy that maximally benefits from eliminating variable-values from the stream.  The employment of URIs as a means to enable flexible determination of the Coordinate Reference System (CRS) that is referenced by the srsName attribute in GML-based spatial position representations is a source of sub-optimization when employing EXI with GML-based schemas.
5.8.2.2	Specification
tspi-ext:Point_WGS84E_3D specifies a point as profiled from ISO 19136:2007 (GML) for use in the TSPI Schema but limited to the WGS84E_3D coordinate reference system; it has been extended to include both assessments of the accuracy and/or resolution of the coordinate tuple as well as optional specification of one or more character-oriented presentations of the coordinate tuple based on the sexagesimal, grid-metre, zone-metre, quadrangle and/or numeric-bit location forms.
Figure 41 illustrates the content model of tspi-ext:Point_WGS84E_3D (which may be compared to that of tspi:Point in Section 5.4.2.3). Because this content model does not strictly follow the conformance requirements of ISO 19136:2007 the resulting element and types must be employed with care.

    <element name="Point_WGS84E_3D" type="tspi-ext:PointType_WGS84E_3D"
                                                                   substitutionGroup="gml:AbstractGeometricPrimitive"/>

    <!-- A restricted version of tspi:PointType that is technically incorrect, but which most GML-aware
          applications should process identically to that defined in ISO 19136. ISO 19136 Clause 21.4.2.1
          (User-defined geometry types) states: "Any user-defined geometry subtypes shall inherit the
          elements and attributes of the base GML geometry types without restriction, but may extend
          these base types to meet application requirements, such as providing a finer degree of
          interoperability with legacy systems and data sets." This complex type may be used in lieu
          of gml:PointType. 
     -->
    <complexType name="PointType_WGS84E_3D">
        <complexContent>
            <extension base="tspi-ext:PointType_WGS84E_3D_primitive">
                <sequence>
                    <group ref="tspi-core:resolutionGroup"/>
                    <group ref="tspi-core:presentationGroup"/>
                </sequence>
            </extension>
        </complexContent>
    </complexType>

    <!-- A simple type restricting the GML attribute srsName (whose type is 'anyURI') to allow
          only a single, fixed value. WGS84_3D is a geodetic (geographic) coordinate reference
          system that is based on the World Geodetic System 1984 (WGS84) ellipsoid, extended
          by an ellipsoid (geodetic) height position ('Height Above the Ellipsoid': HAE).
     -->
   <simpleType name="srsName_WGS84E_3D">
        <restriction base="anyURI">
            <enumeration value="http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_3D"/>
        </restriction>
    </simpleType>

    <!-- A restricted version of gml:PointType that is technically incorrect, but which most GML-aware 
          applications should process identically to that defined in ISO 19136. ISO 19136 Clause 21.4.2.1
          (User-defined geometry types) states: "Any user-defined geometry subtypes shall inherit the
          elements and attributes of the base GML geometry types without restriction, but may extend
          these base types to meet application requirements, such as providing a finer degree of
          interoperability with legacy systems and data sets." This complex type may be used in lieu
          of gml:PointType.
     -->
    <complexType name="PointType_WGS84E_3D_primitive">
        <complexContent>
            <!-- The substitution group chain in ISO 19136 (GML 3.2.1; OGC 07-036) proceeds
                   from gml:PointType to gml:AbstractGeometricPrimitiveType to gml:AbstractGeometryType.
                   All geometry elements are derived directly or indirectly from the gml:AbstractGeometryType
                   abstract supertype. A geometry element shall have an identifying attribute (gml:id), may have
                   one or more names (elements gml:identifier and gml:name) and a description (elements
                   gml:description and gml:descriptionReference). It may be associated with a spatial reference
                   system (attribute group gml:SRSReferenceGroup). The following rules shall be adhered to:
                        (1) Every geometry type shall derive from this abstract type.
                        (2) Every geometry element (i.e. an element of a geometry type) shall be directly
                                 or indirectly in the substitution group of AbstractGeometry.
             -->
            <restriction base="gml:PointType">
                <sequence>
                    <!-- The group gml:StandardObjectProperties is inherited from gml:AbstractGMLType;
                           it is provided for convenience in the construction of application schema, particularly
                           when it is desired to define types derived by restriction from gml:AbstractGMLType and 
                           gml:AbstractFeatureType. Derivation by restriction requires that all components that
                           are used unchanged are copied down into the new type definition.
                     -->
                    <group ref="gml:StandardObjectProperties"/>
                    <choice>
                        <element ref="gml:pos"/>
                        <!-- Note that the following element is deprecated, but included in ISO 19136:2007
                              for backwards compatibility
                         -->
                        <element ref="gml:coordinates"/>
                    </choice>
                </sequence>
                <!-- The attribute group gml:SRSReferenceGroup is a reference to the CRS used
                       by this geometry, with optional  additional information to simplify the processing
                       of the coordinates when a more complete definition of the CRS is not needed.
                       gml:SRSReferenceGroup is inherited from gml:AbstractGeometryType.

                       In this use we restrict the gml:SRSReferenceGroup to only use attribute srsName,
                       and that with a fixed value.
                 -->
                <attribute name="srsName" type="tspi-ext:srsName_WGS84E_3D" use="required"/>
            </restriction>
        </complexContent>
    </complexType>

Figure 41 – Specification of tspi-ext:Point_WGS84E_3D and its supporting types
6	Where – Geographic Location
6.1	Introduction
Ideally, spatial information is based on the specification of exact position and geometry with respect to a well-defined coordinate reference system. However, it is the case that other types of spatial reference systems are used for identifying “place” (see Section 1.7). These include the use of geographic identifiers (e.g., place names) in which a spatial reference in the form of a label or code is used to identify a location (“an identifiable geographic place”)  that may then be more rigorously tied to a position.
A spatial reference system is established based on the structure of the geographic identification scheme that relates identified locations to positions. Gazetteers are then used to establish directories of (geographically) identified locations along with their corresponding positions (e.g., "Mountain View, CA" and {37.423021, -122.083739}, a geodetic latitude/ longitude position).
ISO 19112:2003 Geographic information – Spatial referencing by geographic identifiers specifies a conceptual schema for spatial references based on geographic identifiers – the relationship to a location that is determined by a geographic feature or features (for example a named country, administrative subdivision, town, property, or river basin). It establishes a general model for spatial referencing using geographic identifiers, defines the components of a spatial reference system and defines the essential components of a gazetteer (a directory of geographic identifiers describing location instances). Its conceptual schema enables consistent application of Web Feature Services (WFS) with gazetteer data, which is further elaborated by draft OGC Best Practices Document: Gazetteer Service - Application Profile of the Web Feature Service Implementation Specification, OGC 11-122r1, Version: 0.9.4.
The TSPI specification adopts ISO 19112:2003 and extends selected portions of OGC 11-122r1 as its basis for geographic identification of location. This specification does not specify mechanisms for converting between geographically-identified locations and positions.
6.2	Abstract Geographically-identified Location
The TSPI Schema defines the abstract XML element tspi:AbstractGeographicLocation as the head of a substitution group of which all TSPI-allowed elements that represent geographically-identified locations are members. Those include the elements specified in Section 6.3 as well as any ‘tspi-ext’ elements that represent address (see Section 6.4).
When defining Information Exchange Specifications (IES) that <import> the TSPI Schema it is therefore sufficient to use the abstract XML element tspi:AbstractGeographicLocation wherever it is intended to represent a geographically-identified location.
No elements shall be allowed as members of the tspi:AbstractPhysicalAddress substitution group other than those in the ‘si’ ("http://www.isotc211.org/19112"), ‘tspi, ‘tspi-core’ and ‘tspi-ext’ XML namespaces.
6.3	Geographic Identifiers
A location instance in a spatial reference system, e.g., a particular "county" (“Alleghany County”), "town" (“Town of Milford”), "property" (“Tammany Hall Parcel”), or "river" (“Danube River”). The location that is specified is characterized by a location type, e.g., the general concept of a "county", a "town", a "property", or a "river".
Figure 42 illustrates the content model for SI_LocationInstanceType that is derived by Draft OGC Best Practices Document: Gazetteer Service - Application Profile of the Web Feature Service Implementation Specification, OGC 11-122r1, Version: 0.9.4, from ISO 19112:2003, as illustrated in Figure 42. In order to specify a particular (instance) geographic identifier there are four mandatory properties, as follows:
•	geographicIdentifier (the value, e.g., a name or code)
•	position (the position of the identified-thing, which may be specified once and referenced many times)
•	locationType (which specifies the nature of the identifier and its associated geographic location); and
•	administrator (who is responsible for this identifier, metadata which may be specified once and referenced many times).
    <xsd:element name="SI_LocationInstance" type="iso19112:SI_LocationInstanceType" 
                                                                          substitutionGroup="gml:AbstractFeature"/>

    <xsd:complexType name="SI_LocationInstanceType">
        <xsd:complexContent>
            <xsd:extension base="gml:AbstractFeatureType">
                <xsd:sequence>
                    <!-- Note that identifiers may be localized to a specific language -->
                    <xsd:element name="geographicIdentifier" type="iso19112:LanguageStringType"/>
                    <xsd:element name="alternativeGeographicIdentifiers" 
                                           type="iso19112:AlternativeGeographicIdentifiersPropertyType" minOccurs="0"/>
                    <xsd:element name="position" type="gml:PointPropertyType"/>
                    <xsd:element name="geographicExtent" type="gml:GeometryPropertyType"
                                           minOccurs="0" maxOccurs="unbounded"/>
                    <xsd:element name="dateOfCreation" type="xsd:date" minOccurs="0"/>
                    <xsd:element name="administrator" type="gmd:CI_ResponsibleParty_PropertyType"/>
                    <xsd:element name="spatialObject" type="xsd:anyURI" minOccurs="0"/>
                    <xsd:element name="parent" type="gml:ReferenceType" minOccurs="0" maxOccurs="unbounded"/>
                    <xsd:element name="child" type="gml:ReferenceType" minOccurs="0" maxOccurs="unbounded"/>
                    <xsd:element name="locationType" type="gml:ReferenceType"/>
                </xsd:sequence>
            </xsd:extension>
        </xsd:complexContent>
    </xsd:complexType>

    <xsd:complexType name="LanguageStringType">
        <!-- See OGC 11-122r1 Annex F: Language and Script domains,
                                    and Annex G: Dialect domains, which document a subset of
                                    ISO 639-3:2007 Codes for the representation of names of languages. -->
        <!-- See OGC 11-122r1 Annex E: Transliteration domains. -->
        <xsd:simpleContent>
            <xsd:extension base="xsd:string">
                <xsd:attribute ref="xml:lang"/> 
                <xsd:attribute name="transliterationDomain" type="xsd:string"/> 
            </xsd:extension>
        </xsd:simpleContent>
    </xsd:complexType>
Figure 42 – Specification of si:SI_LocationInstanceType and supporting types
Figure 43 illustrates the content model for SI_LocationType that is derived by OGC 11-122r1 from ISO 19112:2003. In order to specify the nature (type) of a geographic identifier there are five mandatory properties, as follows:
•	name (the name of the location type)
•	definition (the meaning of the location type)
•	territoryOfUse (geographic area within which the location type occurs)
•	identification (the nature of the geographic identifier, e.g., name or code)
•	owner (who is responsible for this location type, metadata which may be specified once and referenced many times).
    <xsd:element name="SI_LocationType" type="iso19112:SI_LocationTypeType" 
                                                                     substitutionGroup="gml:AbstractFeature"/>

    <xsd:complexType name="SI_LocationTypeType">
        <xsd:complexContent>
            <xsd:extension base="gml:AbstractFeatureType">
                <xsd:sequence>
                    <!-- Note that names and definitions may be localized to a specific language -->
                    <xsd:element name="name" type="iso19112:LanguageStringType/>
                    <xsd:element name="identification" type="gml:CodeType" minOccurs="1" maxOccurs="unbounded"/>
                    <xsd:element name="definition" type="iso19112:LanguageStringType"/>
                    <xsd:element name="territoryOfUse" type="gml:GeometryPropertyType"/>
                    <xsd:element name="owner" type="gmd:CI_ResponsibleParty_PropertyType"/>
                    <xsd:element name="spatialObjectType" type="xsd:anyURI" minOccurs="0"/>
                    <xsd:element name="parent" type="gml:ReferenceType" minOccurs="0" maxOccurs="unbounded"/>
                    <xsd:element name="child" type="gml:ReferenceType" minOccurs="0" maxOccurs="unbounded"/>
                </xsd:sequence>
            </xsd:extension>
        </xsd:complexContent>
    </xsd:complexType>
Figure 43 – Specification of si:SI_LocationType
Then, in accordance with ISO 19112:2003, location types may be organized into Spatial Reference Systems (SRS) using si:SI_SpatialReferenceSystemUsingGeographicIdentifiers, and location instances may be organized into gazetters using si:SI_Gazetteer.
6.4	Geographic Location Extension
The TSPI Schema includes the ‘tspi-ext’ XML namespace as a basis for extension to include additional representations for geographic location. It is populated with initial high-value extensions, but is dynamically maintained on the MDR. Its use is conditional on the requirements of a given system/application and its accompanying business requirements.
Informative Annex E describes the procedures to be followed when extending the TSPI through a process of registering new XML components in the ‘tspi-ext’ XML namespace.
All registered extensions for geographic identifiers shall be based on valid extensions of si:SI_LocationInstanceType.
The following sections document current community-specific representations for geographic identification of location in the ‘tspi-ext’ XML namespace.
6.4.1	Geographic Location (GEOLOC) Identifiers
6.4.1.1	Introduction
 [this section currently being revised in coordination with the applicable governance authority]
6.4.1.2	Specification
[this section currently being revised in coordination with the applicable governance authority]
7	Where – Physical Address
7.1	Introduction
Ideally, spatial information is based on the specification of exact position and geometry with respect to a well-defined coordinate reference system. However, it is the case that other types of spatial reference systems are used for identifying “place” (see Section 1.7). These include the use of (physical) addressing schemes (e.g., postal addresses) in which a spatial reference in the form of a label or code is used to identifiy a location (“an identifiable geographic place”)  that may then be more rigorously tied to a position. Physical addresses are the location identifiers that are most widely used by the public, and by state and local government, being critical for emergency response, homeland security, and disaster management.
A systematic mapping may be established based on the structure of the physical addressing scheme that allows for geocoding, the process of converting addresses (e.g., "1600 Amphitheatre Parkway, Mountain View, CA") into positions (e.g., geodetic latitude/ longitude {37.423021, -122.083739}).
Federal Geographic Data Committee (FGDC) United States Thoroughfare, Landmark, and Postal Address Data Standard, FGDC-STD-016-2011, February 2011, specifies a comprehensive U.S. address data standard that meets a wide range of addressing requirements: postal delivery and census enumeration, local government administration and intergovernmental cooperation, emergency dispatch, the creation and administration of master address repositories by local address authorities, and the aggregation of local records into larger regional, state, and national address databases.
In the absence of a recognized international standard for addressing,  the TSPI specification adopts selected portions of FGDC-STD-016-2011 as its basis for physical addressing. Those portions are specified in subsequent sections of this specification.
This TSPI specification does not specify mechanisms for converting between addresses and positions.
7.2	Abstract Address
The TSPI Schema defines the abstract XML element tspi:AbstractPhysicalAddress as the head of a substitution group of which all TSPI-allowed elements that represent (physical) addresses are members. Those include the elements specified in Section 7.3 as well as any ‘tspi-ext’ elements that represent address (see Section 7.4).
When defining Information Exchange Specifications (IES) that <import> the TSPI Schema it is therefore sufficient to use the abstract XML element tspi:AbstractPhysicalAddress wherever it is intended to represent a (physical) address.
No elements shall be allowed as members of the tspi:AbstractPhysicalAddress substitution group other than those in the ‘addr’ ("http://www.fgdc.gov/schema/address/addr"), ‘tspi, ‘tspi-core’ and ‘tspi-ext’ XML namespaces.
7.3	Thoroughfare, Landmark, and Postal Addressing
7.3.1	Address Components
FGDC-STD-016-2011 establishes the following basic types of physical address components: 
•	Complete Address Number (complex element): An Address Number, alone or with an Address Number Prefix and/or Address Number Suffix, which identifies a location along a thoroughfare or within a community.
 Syntax: { Address Number Prefix } + { Address Number *} + { Address Number Suffix }
 For example: “123 A North Main Street Extended”.
•	Complete Street Name (complex element): Official name of a thoroughfare as assigned by a governing authority, or an alternate (alias) name that is used and recognized.
 Syntax: { Street Name Pre Modifier } + { Street Name Pre Directional } + {Street Name Pre Type } + 
	    { Separator Element } + { Street Name *} + { Street Name Post Type } + 
                  { Street Name Post Directional } + {Street Name Post Modifier }
 For example: “123 A North Main Street Extended”.
•	Landmark Name: The name of a relatively permanent feature of the manmade landscape that has recognizable identity within a particular cultural context.
 For example: “U.S. Capitol Building”
•	USPS Box (complex element): A container for the receipt of USPS mail uniquely identified by the combination of a USPS Box Type (the name of the class of the container used for receipt of USPS mail) and a USPS Box ID (the numbers or letters distinguishing one box from another within a post office or route).
 Syntax: { USPSBox Type *} + { USPSBox ID *}
 For example: “PO Box 1137 Saipan MP 96950-1137”
•	USPS Route (complex element): A USPS postal delivery point identified by a USPS Route (a collection of boxes served from a signle distribution point, and uniquely identified by a USPS Box Group Type and a USPS Box Group ID) and a USPS Box.
 Syntax: { USPSBox Group Type *} + { USPSBox Group ID *}
 For example: “RR 2 Box 223G Dardanelle AR 72834”
•	USPS General Delivery Point: A central point where mail may be picked up by the addressee. Two values are permitted: "General Delivery" (for post offices), and ship's names (for overseas military addresses).
 For example: “USCGC Hamilton, FPO AP 96667-3931”
•	Delivery Address: The entire address, unparsed, except for the Place Name, State Name, Zip Code, Zip Plus 4, Country Name, and, optionally, Complete Subaddress. 
 For example: “GENERAL DELIVERY”
•	Place Name: The name of an area, sector, or development (such as a neighborhood or subdivision in a city, or a rural settlement in unincorporated area); incorporated municipality or other general-purpose local governmental unit; county; or region within which the address is physically located; or the name given by the U.S. Postal Service to the post office from which mail is delivered to the address.
 For example: “Salt Lake City”
•	State Name: The name of a U.S. state or state equivalent: the fifty US states, the District of Columbia, and all U.S. territories and outlying possessions. A state (or equivalent) is "a primary governmental division of the United States." The names may be spelled out in full or represented by their two-letter USPS or ANSI abbreviation.
 For example: “Virginia” or “VA”
•	Zip Code: A system of 5-digit codes that identifies the individual Post Office or metropolitan area delivery station associated with an address.
 For example: “35305”
•	Zip Plus 4: A 4-digit extension of the 5-digit Zip Code (preceded by a hyphen) that, in conjunction with the Zip Code, identifies a specific range of USPS delivery addresses.
 For example: “3426”
•	Country Name: The name of the country in which the address is located. A country is "an independent, self-governing, political entity."
 For example: “USA” or “GBR”
These, and other, components are used to specify different types of thoroughfare, landmark, and postal addresses.
7.3.2	Address Types
FGDC-STD-016-2011 establishes the following “class formats” (types) of physical address:
•	Numbered Thoroughfare Address: A physical address that:
1.	includes a Complete Address Number and a Complete Street Name;
2.	includes a Place Name and a State Name; and
3.	a Zip Code and/or Country Name are recommended but not mandatory.
•	Unnumbered Thoroughfare Address: A physical address that:
1.	contains a Complete Street Name without a Complete Address Number preceding it;
2.	includes a Place Name and a State Name; and
3.	a Zip Code and/or Country Name are recommended but not mandatory.
•	Intersection Address: A physical address that:
1.	contains two or more Complete Street Names, each separated by a Separator Element;
2.	includes a Place Name and a State Name; and
3.	a Zip Code and/or Country Name are recommended but not mandatory.
•	Two Number Address Range: A physical address that:
1.	contains two Complete Address Numbers separated by a hyphen, where the first Complete Address Number must be less than or equal to the second and the pair are followed by a Complete Street Name;
2.	includes a Place Name and a State Name; and
3.	a Zip Code and/or Country Name are recommended but not mandatory.
•	Landmark Address: A physical address that:
1.	includes a Complete Landmark Name without a Complete Address Number preceding it and without a Complete Street Name following it;
2.	includes a Place Name and a State Name; and
3.	a Zip Code and/or Country Name are recommended but not mandatory.
•	USPS Postal Delivery Box: A physical address that:
1.	includes a USPS Box in the required format with no USPS Route;
2.	includes a Place Name and a State Name; and
3.	a Zip Code and/or Country Name are recommended but not mandatory.
•	USPS Postal Delivery Route: A physical address that:
1.	includes a USPS Address in the specified rural route (RR) or highway contract (HC) or overseas military delivery format;
2.	includes a Place Name and a State Name; and
3.	a Zip Code and/or Country Name are recommended but not mandatory.
•	USPS General Delivery Office: A physical address that:
1.	includes a USPS General Delivery Point in the specified format;
2.	includes a Place Name and a State Name; and
3.	a Zip Code and/or Country Name are recommended but not mandatory.
•	General Address Class: A physical address that:
1.	includes a Delivery Address that is unparsed;
2.	includes a Place Name and a State Name; and
3.	a Zip Code and/or Country Name are recommended but not mandatory.
NOTE: This class may include addresses that do not conform to any of the thoroughfare, landmark, or postal class formats, including non-U.S. addresses that do not fit into one those class formats.
TSPI does not support the Four Number Address Range class format, which is unique to U.S. Census Bureau TIGER/Line file street data. TSPI also does not support the Address Reference System  class format, which is a set of rules and geometries that define how addresses are assigned along thoroughfares and/or within a given area (Address Reference System Extent).
The use of the Numbered Thoroughfare Address is a recommended practice.
The use of the General Address Class is allowed only when a more specific address type is not applicable; it will be replaced when a suitable international addressing standard (e.g., ISO 19160) has been completed.
It is a recommended practice that the Country Name be populated, when applicable to the address type. When populated, it is a recommended practice that a three-character code from ISO 3166-1 be used (e.g., “USA”).
7.4	Physical Address Extension
The TSPI Schema includes the ‘tspi-ext’ XML namespace as a basis for extension to include additional representations for (physical) address. It is populated with initial high-value extensions, but is dynamically maintained on the MDR. Its use is conditional on the requirements of a given system/application and its accompanying business requirements.
Informative Annex E describes the procedures to be followed when extending the TSPI through a process of registering new XML components in the ‘tspi-ext’ XML namespace.
There are currently no community-specific representations for (physical) address in the ‘tspi-ext’ XML namespace.
8	When – Temporal Position
8.1	Overview
The unambiguous exchange of spatiotemporal data requires the specification of the temporal, and accompanying precision and quality assessment, characteristics of entities (e.g., equipment, combatants and targets).
Temporal information includes position (instant), extent (duration), and periodic recurrence characteristics. Unambiguous expression of the values of these characteristics requires the identification of a robust temporal reference system, such as Coordinated Universal Time (UTC),  and the ability to specify the values of such characteristics with respect to that temporal reference system.
The TSPI Schema specifies XML types for use in the exchange of the following categories of temporal information:
•	Position (instant) in an Earth-referenced temporal coordinate system; and
•	Extent (duration) in an Earth-referenced temporal coordinate system.
In each of these information categories, as appropriate, the TSPI Schema supports the specification of quality assessment information including the precision of data values as well as quantitative and qualitative estimates of the accuracy of temporal characteristics.
ISO 19136:2007 (GML) includes temporal schema components for specifying temporal reference systems, temporal geometry, temporal topology, and the temporal characteristics of geographic data. Temporal geometry is described in terms of time instants, periods, positions and lengths. OGC® Geography Markup Language (GML) - Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1) extends ISO 19136:2007 to specify enhancements to some basic temporal types.The model underlying these temporal representations constitutes a profile of the conceptual schema specified in ISO 19108:2002 Geographic information – Temporal schema.
The TSPI Schema profiles the GML temporal schema components to model these temporal-associated information types.
8.2	Temporal Reference Systems
Time is a dimension analogous to any of the spatial dimensions. Like space, time has geometry and topology. A point in time occupies a position that can be identified in relation to a temporal reference system. Distance can be measured. Unlike space, time has a single dimension. The “direction” of that dimension is implicitly “forward” (later).
ISO 8601:2004 Data elements and interchange formats – Information interchange – Representation of dates and times specifies numeric representations of information regarding date and time of day as well as formats of these numeric representations. Some of those formats are used by the TSPI Schema.
ISO 8601:2004 specifies the use of the Gregorian calendar. The Gregorian calendar has a reference point that assigns 20 May 1875 to the calendar day that the “Convention du Mètre” was signed in Paris. Consecutive calendar years are assigned a year number. The Gregorian calendar distinguishes common years of 365 consecutive calendar days and leap years of 366 consecutive calendar days. A leap year is a calendar year whose year number is divisible by four an integral number of times. 
In the Gregorian calendar the calendar year is divided into 12 consecutive calendar months, each consisting of a specific number of calendar days, as follows: January (31), February (28, unless a leap year in which case 29), March (31), April (30), May (31), June (30), July (31), August (31), September (30), October (31), November (30), and December (31).
In the Gregorian calendar the calendar year has either 52, or in the case of a leap year, 53 calendar weeks.  A calendar week consists of 7 consecutive calendar days as follows: Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, and Sunday. The date of 1 January 2000 is assigned the calendar day of Saturday.
ISO 8601 recommends the use of time-scales applying the 24-hour time keeping system for the identification of time points within a calendar day. ISO 8601 specifies the use of Coordinated Universal Time (UTC) as the basis for determining the time of day. 
Each calendar day contains 24 hours and each hour contains 60 minutes, but the number of seconds in a minute may vary – normally 60, but sometimes 61 or 59.  The time of day is represented by the number of hours elapsed after midnight, the number of minutes elapsed after the last full hour, and the number of seconds elapsed after the last full minute, with decimal (fractional) parts of a second if necessary. Most calendar days contain exactly 86,400 SI seconds, with exactly 60 seconds in each minute; occasionally the last minute of a calendar day will have 61 seconds. 
This TSPI specification conforms to ISO 8601:2004, using the Gregorian calendar and UTC as its basis for specifying temporal position.
In ISO 19136:2007 (GML) the method for identifying a temporal position is specific to each temporal reference system; this specification restricts itself to representations using the the Gregorian- and UTC-based temporal reference system.
gml:TimePosition supports the description of temporal position in accordance with the subtypes specified in ISO 19108:2002, Clause 5.4.2 TM_Position. The content model of gml:TimePosition and its associated type as restricted for use in the TSPI Schema (see Section 8.4) is as follows:
<element name="timePosition" type="gml:TimePositionType"/>

<complexType name="TimePositionType" final="#all">
 <simpleContent>
  <extension base="gml:TimePositionUnion">
   <attribute name="frame" type="anyURI" default="#ISO-8601"/>
   <attribute name="indeterminatePosition"
type="gml:TimeIndeterminateValueType" />
  </extension>
 </simpleContent>
</complexType>

A time value shall be associated with a temporal reference system through the frame XML attribute that provides a URI reference that identifies a specification of the reference system. The Gregorian calendar with UTC is the default reference system and is indicated by the URI fragment “#ISO-8601”. The TSPI Schema shall use only the Gregorian calendar (and UTC). No conforming use of the TSPI shall shall revise the frame XML attribute to other than its default value.
Inexact temporal positions may be expressed using the (optional) indeterminatePosition XML attribute; its use in the TSPI Schema is specified in Sections 8.5.3 and 8.6.2.
8.3	Time Zones
8.3.1	Introduction
Temporal positions are effectively meaningless without an unambiguous specification of their temporal reference system. A temporal reference system is determined by determining a reference time instant and a basis for determining temporal extent (duration).
ISO 8601:2004 Data elements and interchange formats – Information interchange – Representation of dates and times specifies numeric representations of information regarding date and time of day as well as formats of these numeric representations. ISO 8601 specifies the use of the Gregorian calendar and Coordinated Universal Time (UTC).
In practice, however, natural human and thus business rythms are linked to the position of the sun (e.g., sunrise and sunset) that necessarily vary globally when determined by an absolute global clock. Locations in relative proximity usually share a common “local time” despite variation in the local rising and setting of the sun as reflected by a global clock such as UTC.
8.3.2	Local Time
A time zone is a region of the Earth that has uniform standard time – the “local time”. Standard time zones (also known as “Winter Time” zones) can be roughly defined by geometrically subdividing the Earth's surface into 24 zones bordered by meridians each 15° of longitude apart. The local time in neighboring zones would differ by one hour. However, political boundaries, geographical practicalities, and convenience of inhabitants can result in irregularly-shaped zones. Moreover, in a few regions, half-hour or quarter-hour differences are in effect. Some zones north-south of each other in the mid Pacific differ by 24 hours in time; they have the same time of day but differ by a full calendar day.
By convention, time zones compute their local time as an offset from UTC. Local time is UTC plus the current time zone offset for the specific location. Table 9 lists standard time zones, their relationship to UTC, and example locations where the time zone is used as local time. The first column “Code” identifies the designation assigned by USMTF in the TIME ZONE field.
Table 9 – Local Time and Standard Winter Time Zones
Code	Spoken	UTC Offset	Local Time	Example Locations
		UTC+14:00	02:00 (next day)	Line Islands (Kiribati)
		UTC+13:00	01:00 (next day)	Phoenix Islands Kiribati); Tonga
		UTC+12:45	00:45 (next day)	Chatham Islands (New Zealand)
M	Mike	UTC+12:00	00:00 (next day)	Antarctica; Gilbert Islands; New Zealand
6 (LM)		UTC+11:30	23:30	Norfolk Island (Pacific Island east of Australia)
L	Lima	UTC+11:00	23:00	Kosrae (Federated States of Micronesia); New Caladonia; Kuril Islands (Russia)
5 (KL)		UTC+10:30	22:30	Lord Howe Island (New South Wales, Australia)
K	Kilo	UTC+10:00	22:00	Queensland (Australia); Guan; Papua New Guinea
4 (IK)		UTC+09:30	21:30	New South Wales (Australia)
I	India	UTC+09:00	21:00	Japan; North Korea; South Korea
H	Hotel	UTC+08:00	20:00	Beijing (China); Hong Kong; Irkutsk (Russia); Phillipines
G	Golf	UTC+07:00	19:00	Laos; Thailand; Khovd (Mongolia); Vietnam;
3 (FG)		UTC+06:30	18:30	Cocos Islands; Myanmar
F	Foxtrot	UTC+06:00	18:00	Almaty (Kazakhstan); Bangladesh; Bhutan; Novosibirsk Oblast (Russia)
2 (EF)		UTC+05:30	17:30	India; Sri Lanka
E	Echo	UTC+05:00	17:00	Maldives; Pakistan; Uzbekistan; Volgograd Oblast (Russia)
1 (DE)		UTC+04:30	16:30	Afghanistan
D	Delta	UTC+04:00	16:00	Azerbaijan; Oman; Seychelles; United Arab Emirates
0 (CD)		UTC+03:30	15:30	Iran
C	Charlie	UTC+03:00	15:00	Bahrain; Ethiopia; Saudi Arabia; Sudan; Yemen
B	Bravo	UTC+02:00	14:00	Cyprus; Finland; Greece; Turkey; Ukraine
A	Alpha	UTC+01:00	13:00	Belgium; France; Germany; Spain; Tunisia
Z	Zulu	UTC (±0)	12:00	Ireland; Greenland; Morocco; United Kingdom
N	November	UTC-01:00	11:00	Azores (Portugal); Cape Verde 
O	Oscar	UTC-02:00	10:00	Fernando de Noronha (Brazil); South Georgia and the South Sandwich Islands 
P	Papa	UTC-03:00	9:00	Argentina; Brazil; French Guiana; Uruguay
7 (PQ)		UTC-03:30	8:30	Labrador (Canada); Newfoundland (Canada)
Q	Quebec	UTC-04:00	8:00	Bermuda; Bolivia; New Brunswick (Canada); Paraguay
R	Romeo	UTC-05:00	7:00	Columbia; Cuba; Peru; Toronto (Ontario, Canada); New York City (USA)
S	Sierra	UTC-06:00	6:00	Chicago (USA); Easter Island (Chile); Guatemala; Mexico City (Mexico)
T	Tango	UTC-07:00	5:00	Alberta (Canada); Montana (USA); Sonora (Mexico)
U	Uniform	UTC-08:00	4:00	Baja California (Mexico); Pitcairn Islands; Washington (USA); Yukon (Canada)
8 (UV)		UTC-08:30	3:30	Previous Standard Time of South Korea from 1954 to 1961.
V	Victor	UTC-09:00	3:00	Alaska (USA); Gambier Islands (French Polynesia)
9 (VW)		UTC-09:30	2:30	Marquesas Islands (French Polynesia)
W	Whiskey	UTC-10:00	2:00	Cook Islands; Hawaii (USA); Johnston Atoll; Tubai Islands (French Polynesia)
X	X-ray	UTC-11:00	1:00	American Samoa; Niue; Samoa
Y	Yankee	UTC-12:00	0:00	Baker and Howland Islands; Ships at sea within 7.5° east of 180°.

8.3.3	Local Time and UTC of Day
When it is required to indicate the difference between local time and UTC of day, the representation of the difference can be expressed in hours and minutes, or hours only. It shall be expressed as positive (i.e., with the leading plus sign ‘+’) if the local time is ahead of or equal to UTC of day and as negative (i.e., with the leading negative minus sign ‘-‘) if it is behind UTC of day. The minute time element of the difference may only be omitted if the difference between the local time of day and UTC time of day is exactly an integral number of hours.
The third column “UTC Offset” in Table 9 lists hour-and-minute offsets from UTC for well-known time zones.
For example, for the local time of 27 minutes and 46 seconds past 15 hours locally in Berlin, Germany (in winter UTC+01:00) and in New York City, USA (in winter UTC-05:00) the corresponding time values would be “15:27:46+01:00” and “15:27:46-05:00”, respectively. As ISO 8601 allows for more compact (“basic”) expressions, these are equivalently represented as “152746+01” and “152746-05”, respectively. 
8.3.4	Daylight Savings Time
Many countries, or parts of countries, adopt daylight saving time (also known as "Summer Time") during part of the year. Daylight Savings Time (DST) adjusts the local clock to better align clock-associated schedules with the then-current diurnal solar cycle.
This typically involves advancing clocks by an hour near the start of the spring season and retarding them correspondingly to the original setting in the fall season. Thus afternoons and evenings have longer daylight and mornings have shorter daylight than would otherwise be the case. Some countries also use “backward daylight saving” (retarding clocks during the winter period).
Despite questions as to its value, many countries use the method with details varying by location and changing occasionally. Most countries around the equator do not observe daylight saving time, since the seasonal difference in sunlight is minimal.
DST's clock shifts have the obvious disadvantage of complexity and introduce opportunities for error, both as regards the as-of-date local time offset from UTC and as regards the time offset between two as-of-date local times.
When DST is in effect the UTC offset specified for “Winter Time” will be different from that specified in Table 9. It is critical to keep this in mind, and determine/include the correction, when specifying a time instant in accordance with the TSPI Schema.
8.4	Time-related GML Restrictions
ISO 19136:2007 (GML) includes a temporal content model that supports a greater degree of flexibility than necessary to achieve spatiotemporal data interoperability throughout the U.S. Department of Defense (DoD) and Intelligence Community (IC). For example, it includes support for temporal reference systems other than than those based on calendars (and in particular the default Gregorian calendar, and UTC).
In consequence this TSPI specification establishes four time-related content-model exclusions, as follows:
1.	gml:TimePositionType: The XML attribute calendarEraName shall not be used.
o	The (optional) calendarEraName XML attribute provides the name of the calendar era for time values using a calendar containing more than one era. The TSPI Schema allows only the use of the Gregorian calendar.
2.	gml:TimePositionUnion: The simple types xsd:time, xsd:anyURI and xsd:decimal, in the set of allowed member types, shall not be used.
o	xsd:time is intended to be used to identify an instant of time that recurs every day – its lexical space is identical to the time part of xsd:dateTime: [-] hh:mm:ss[Z|(+|-)hh:mm]; it is a set of zero-duration daily time instances. This does not represent a valid instant on the temporal axis (it is a recurring instant – a set of temporal positions) and therefore is not suitable for use by the TSPI Schema (which follows ISO 8601).
o	xsd:anyURI is intended to be used to reference an ordinal era. The TSPI schema uses the Gregorian calendar and does not support ordinal eras.
o	xsd:decimal is used to indicate the distance from the temporal scale origin (e.g., UNIX time, GPS calendar). The TSPI Schema does not support the representation of time except in accordance with the Gregorian calendar (and UTC).
3.	gml:TimeIndeterminateValueType: The enumeration value now shall not be used.
o	The now enumeration value indicates that the specified value shall be replaced with the current temporal position whenever the value is accessed. This semantic is not appropriate for the purposes intended by the TSPI Schema.
4.	gml:TimeUnitType: The string-extension of the form "other:\w{2,}" shall not be used.
o	The string-extension of the form "other:\w{2,}" is intended to allow for the use of arbitrary units of measure. In the scope of the TSPI Schema this flexibility is undesirable as it leads to potential ambiguity and has not been demonstrated to be necessary.
8.5	Temporal Position
8.5.1	Position Encoding
8.5.1.1	Time Position
The gml:TimePositionType extends from the simple type gml:TimePositionUnion – a union of XML Schema simple types which instantiate the subtypes for temporal position described in ISO 19108:2002. Its content model as restricted for use in the TSPI Schema (see Section 8.4) is as follows:
<simpleType name="TimePositionUnion">
 <union memberTypes="gml:CalDate dateTime"/>
</simpleType>
Its memberTypes are intended to be employed as follows:
•	gml:CalDate is used to represent a calendar date (lexical representation:[-]CCYY-MM-DD [Z|(+|-)hh:mm]) of potentially reduced resolution.
•	xsd:dateTime is used to represent a calendar date and time of day – its lexical representation is the extended format: [-]CCYY-MM-DDThh:mm:ss[Z|(+|-)hh:mm].
XML Schema Part 2: Datatypes Second Edition (W3C Recommendation 28 October 2004) Section 3.2.7 specifies the characteristics of the xsd:dateTime encoding as follows:
[Definition:]   dateTime values may be viewed as objects with integer-valued year, month, day, hour and minute properties, a decimal-valued second property, and a boolean timezoned property. Each such object also has one decimal-valued method or computed property, timeOnTimeline, whose value is always a decimal number; the values are dimensioned in seconds, the integer 0 is 0001-01-01T00:00:00 and the value of timeOnTimeline for other dateTime values is computed using the Gregorian algorithm as modified for leap-seconds. The timeOnTimeline values form two related "timelines", one for timezoned values and one for non-timezoned values. Each timeline is a copy of the value space of decimal, with integers given units of seconds.
The value space of dateTime is closely related to the dates and times described in ISO 8601. For clarity, the text above specifies a particular origin point for the timeline. It should be noted, however, that schema processors need not expose the timeOnTimeline value to schema users, and there is no requirement that a timeline-based implementation use the particular origin described here in its internal representation. Other interpretations of the value space which lead to the same results (i.e., are isomorphic) are of course acceptable.
All timezoned times are Coordinated Universal Time (UTC, sometimes called "Greenwich Mean Time"). Other timezones indicated in lexical representations are converted to UTC during conversion of literals to values. "Local" or untimezoned times are presumed to be the time in the timezone of some unspecified locality as prescribed by the appropriate legal authority; currently there are no legally prescribed timezones which are durations whose magnitude is greater than 14 hours. The value of each numeric-valued property (other than timeOnTimeline) is limited to the maximum value within the interval determined by the next-higher property. For example, the day value can never be 32, and cannot even be 29 for month 02 and year 2002 (February 2002).
The lexical representation of the xsd:dateTime is as follows
The lexical space of dateTime consists of finite-length sequences of characters of the form: '-'? yyyy '-' mm '-' dd 'T' hh ':' mm ':' ss ('.' s+)? (zzzzzz)?, where
    ● '-'? yyyy is a four-or-more digit optionally negative-signed numeral that represents the year; if more than four digits, leading zeros are prohibited, and '0000' is prohibited (see the Note above (§3.2.7); also note that a plus sign is not permitted);
    ● the remaining '-'s are separators between parts of the date portion;
    ● the first mm is a two-digit numeral that represents the month;
    ● dd is a two-digit numeral that represents the day;
    ● 'T' is a separator indicating that time-of-day follows;
    ● hh is a two-digit numeral that represents the hour; '24' is permitted if the minutes and seconds represented are zero, and the dateTime value so represented is the first instant of the following day (the hour property of a dateTime object in the value space cannot have a value greater than 23);
    ● ':' is a separator between parts of the time-of-day portion;
    ● the second mm is a two-digit numeral that represents the minute;
    ● ss is a two-integer-digit numeral that represents the whole seconds;
    ● '.' s+ (if present) represents the fractional seconds;
    ● zzzzzz (if present) represents the timezone (as described below).
For example, 2002-10-10T12:00:00-05:00 (noon on 10 October 2002, Central Daylight Savings Time as well as Eastern Standard Time in the U.S.) is 2002-10-10T17:00:00Z, five hours later than 2002-10-10T12:00:00Z.
…
Timezones are durations with (integer-valued) hour and minute properties (with the hour magnitude limited to at most 14, and the minute magnitude limited to at most 59, except that if the hour magnitude is 14, the minute value must be 0); they may be both positive or both negative.
The lexical representation of a timezone is a string of the form: (('+' | '-') hh ':' mm) | 'Z', where
    ● hh is a two-digit numeral (with leading zeros as required) that represents the hours,
    ● mm is a two-digit numeral that represents the minutes,
    ● '+' indicates a nonnegative duration,
    ● '-' indicates a nonpositive duration.
The mapping so defined is one-to-one, except that '+00:00', '-00:00', and 'Z' all represent the same zero-length duration timezone, UTC; 'Z' is its canonical representation.
When a timezone is added to a UTC dateTime, the result is the date and time "in that timezone". For example, 2002-10-10T12:00:00+05:00 is 2002-10-10T07:00:00Z and 2002-10-10T00:00:00+05:00 is 2002-10-09T19:00:00Z.
The canonical representation of the xsd:dateTime is as follows
Except for trailing fractional zero digits in the seconds representation, '24:00:00' time representations, and timezone (for timezoned values), the mapping from literals to values is one-to-one. Where there is more than one possible representation, the canonical representation is as follows:
    ● The 2-digit numeral representing the hour must not be '24';
    ● The fractional second string, if present, must not end in '0';
    ● for timezoned values, the timezone must be represented with 'Z' (All timezoned dateTime values are UTC.).
As the XML Schema simpleType xsd:dateTime does not permit right-truncation, except for fractions of seconds, the additional XML Schema simpleTypes xsd:date, xsd:gYearMonth and xsd:gYear are required.
•	xsd:date may be used for Gregorian calendar dates as defined by ISO 8601 (i.e., a one-day-long period of time); its lexical representation follows the ISO 8601 syntax (i.e., [-]CCYY-MM-DD[Z|(+|-)hh:mm]) with an optional time zone.
•	xsd:gYearMonth may be used to specify the period of one calendar month in a specific year (e.g., July 2009); its lexical space follows the ISO 8601 syntax for such periods (i.e., [-]CCYY-MM[Z|(+|-)hh:mm]) with an optional time zone.
•	xsd:gYear may be used to specify successive periods of one calendar year (e.g., 2009); its lexical representation follows the ISO 8601 syntax for such periods (i.e., [-]CCYY[Z|(+|-)hh:mm]) with an optional time zone.
These three additional forms supporting the representation of time in accordance with the notation specified by ISO 8601 are specified using gml:CalDate as follows:
<simpleType name="CalDate">
 <union memberTypes="date gYearMonth gYear"/>
</simpleType>
Note that use of the optional leading minus sign, without a space, and optional trailing time zone in the types xsd:dateTime, xsd:date, xsd:gYear and xsd:gYearMonth are not conformant to the notation specified by ISO 8601, however their use is conformant to ISO 19136:2007 and this specification.
Table 10 lists the supported content of gml:timePosition in the TSPI Schema, the corresponding XML schema simple type, and an example of the content corresponding to that simple type.
Table 10 – Supported Date/Time Representations
gml:timePosition Content	XSD Type	Example
Year	xs:gYear	“2007”
Year and Month	xs:gYearMonth	“2007-03”
Date (Year, Month, and Day)	xs:date	“2007-03-20”
Date and Time	xs:dateTime	“2007-03-20T14:27:50Z”
“2007-03-20T14:27:50.0Z”

8.5.1.2	Disallowed Time-related XSD Types
Note that the XML Schema simpleTypes xsd:gMonth, xsd:gMonthDay, xsd:gDay and xsd:time are not used as none of these represents a valid instant on the temporal axis – all are, in fact, recurring instants (a set of temporal positions) and therefore are not suitable for use in this specification (which follows ISO 8601).
xsd:gMonth is a Gregorian month that recurs every year; its value space is a set of one-month long, yearly periodic instances and its lexical representation is the left and right truncated lexical representation for date: --MM. 
xsd:gMonthDay is a Gregorian date that recurs every year (e.g., the 3rd of May); its value space is a set of one-day long, annually periodic instances of calendar dates and its lexical representation is the left truncated lexical representation for date: --MM-DD. 
xsd:gDay is a Gregorian day that recurs every month (e.g., the 5th of the month); its value space is a set of one-day long, monthly periodic instances of calendar dates and its lexical representation is the left truncated lexical representation for date: ---DD.
xsd:time is an instant of time that recurs every day; its value space is a set of zero-duration daily time instances and its lexical representation is identical to the time part of xsd:dateTime: hh:mm:ss[Z|(+|-)hh:mm]. 
8.5.1.3	Local Time
The types xsd:dateTime, xsd:date, xsd:gYear and xsd:gYearMonth optionally include the specification of time zone. A time zone is a region of the Earths surface that has established a local clock that is offset from UTC by a specified time interval (either positive or negative); time zones are described in greater detail in Section 8.3.
It is a recommended practice that local time not be used in the TSPI Schema. Failure to specify the relationship between local time and UTC of day (Zulu time) renders such temporal positions ambiguous.
It is a recommended practice that UTC of day (Zulu time) always be used in the TSPI Schema. Doing so makes temporal positions unambiguous, maximally compact, and facilitates error-free comparison of time positions.
It is a deprecated practice that a time zone offset be used in the TSPI Schema. When doing so it is necessary that careful attention be paid to specifying an offset (difference between local time and UTC of Day) that includes the effect of any local Daylight Savings Time that may be in effect (see Section 8.3.4).
8.5.2	Exact Temporal Position
gml:TimeInstant implements ISO 19108:2002, Clause 5.2.3.2 TM_Instant and acts as a zero-dimensional geometric primitive that represents an identifiable position in time.
The method for identifying a temporal position (gml:TimePositionType) is specific to each temporal reference system. Values based on calendars and clocks use lexical formats that are based on ISO 8601. 
The content model for gml:TimeInstant and its associated type are as follows:
<element name="TimeInstant" type="gml:TimeInstantType" substitutionGroup="gml:AbstractTimeGeometricPrimitive"/>
<complexType name="TimeInstantType" final="#all">
 <complexContent>
  <extension base="gml:AbstractTimeGeometricPrimitiveType">
   <sequence>
    <element ref="gml:timePosition"/>
   </sequence>
  </extension>
 </complexContent>
</complexType>
In an example XML instance document, a gml:TimeInstant contains a gml:timePosition specifying January 1, 2007 at 1800 UTC, as follows:
<gml:TimeInstant gml:id="timeStampExample">
  <gml:timePosition>2007-01-10T18:00:00.0Z</gml:timePosition >
</gml:TimeInstant>
Since the Gregorian calendar with UTC is the default temporal reference system it is not necessary to specify a value for the frame XML attribute. Note that a gml:TimeInstant shall have an identifying XML attribute (gml:id); the scope of uniqueness of the value of this attribute is the instance document. 
The use of a gml:TimeInstant is analogous to that for a gml:Point – it specifies a position in a temporal reference system, as opposed to a coordinate reference system. It differs in that the gml:timePosition element may be directly used in application schemas (including those conforming to this TSPI specification) as it carries, through the frame XML attribute, sufficient information to unambiguously specify its temporal reference system. It is thus valid for a conforming schema to specify:
<ns:MyBigEventType
  <gml:timePosition>2007-01-10T18:00:00.0Z</gml:timePosition >
</ns:MyBigEventType>
The comparable construct based on the direct use of a gml:pos would generally be invalid as a gml:pos does not necessarily carry any information specifying its coordinate reference system.
It is a recommended practice that the “wrapper” gml:TimeInstant be used instead of direct use of the gml:timePosition, as doing so is necessary for the proper specification of temporal extents (see Section 8.6) and temporal relations.
8.5.3	Inexact Temporal Position
Inexact temporal positions may be expressed using the optional indeterminatePosition XML attribute of gml:TimePosition (see Section 8.2). The content model of gml:TimeIndeterminateValueType as restricted for use in the TSPI Schema (see Section 8.4) is as follows:
<simpleType name="TimeIndeterminateValueType">
 <restriction base="string">
  <enumeration value="after"/>
  <enumeration value="before"/>
  <enumeration value="unknown"/>
 </restriction>
</simpleType>
The semantic of these values is as follows:
•	unknown: indicates that no specific value for temporal position is provided;
•	before: indicates that the actual temporal position is unknown, but it is known to be before  the specified value; and
•	after: indicates that the actual temporal position is unknown, but it is known to be after  the specified value.
A value for indeterminatePosition may be used either alone, or to qualify a specific value for temporal position. For example, in an XML instance document:
<gml:timePosition indeterminatePosition="unknown"/>
<gml:timePosition indeterminatePosition="before">2012-07-04</gml:timePosition>
<gml:timePosition indeterminatePosition="after">1994</gml:timePosition>
Note that the first case is not meaningful when specifying a single gml:timePosition, but is used when specifying temporal extents.
It is a recommended practice that gml:TimeInstant not be used with a specified value of indeterminatePosition unless it is being used to specify an open-ended temporal extent using gml:TimePeriod (see Section 8.6.2). Doing so results in consistent XML representation of the related semantics “before” and “on or before” (as well as “after” and “on or after”) as syntactically-consistent temporal extents. It also eliminates inconsistent modelling choices for open-ended temporal extents by different developers.
8.6	Temporal Extent
8.6.1	Exact Temporal Extent
gml:TimePeriod implements ISO 19108:2002, Clause 5.2.3.3 TM_Period and acts as a one-dimensional temporal primitive that represents an identifiable extent in time. The location in time of a gml:TimePeriod is described by the temporal positions of the instants at which it begins and ends. The length of the period is equal to the temporal distance between the two bounding temporal positions.
A temporal extent may be either a closed period (both of the beginning and ending times are specified) or an open period (either the beginning or ending time is specified, but not both). A closed temporal extent uses the gml:TimePeriod object with a date and/or time specified for both gml:begin (start of the period) and gml:begin (end of the period).
The example instantiation in Figure 44 illustrates the temporal extent matching the statement “between January 1, 2007 and January 31, 2007”.
<gml:TimePeriod gml:id="myClosedPeriod">
  <gml:begin>
    <gml:TimeInstant gml:id="myClosedStart">
      <gml:timePosition>2007-01-01</gml:timePosition>
    </gml:TimeInstant>
  </gml:begin>

  <gml:end>
    <gml:TimeInstant gml:id="myClosedEnd">
      <gml:timePosition>2007-01-31</gml:timePosition>
    </gml:TimeInstant>
  </gml:end>
</gml:TimePeriod>
Figure 44 – Example Temporal Extent as a Closed Period
8.6.2	Inexact Temporal Extent
An open gml:TimePeriod may be used to report a temporal extent that covers the time “before” or “since” a known date/time; either the beginning or ending time is specified, but not both. For example, a resource that contains data that is current as of a certain date could have its temporal extent reported as an open period.
The example instantiation in Figure 45 illustrates the temporal extent matching the statement “before January 31, 2007”.
<gml:TimePeriod gml:id="myOpenPeriod">
  <gml:begin>
    <gml:TimeInstant gml:id="myOpenStart">
      <gml:timePosition indeterminatePosition="unknown"/>
    </gml:TimeInstant>
  </gml:begin>
  <gml:end>
    <gml:TimeInstant gml:id="myClosedEnd">
      <gml:timePosition>2007-01-31</gml:timePosition>
    </gml:TimeInstant>
  </gml:end>
</gml:TimePeriod>
Figure 45 – Example Temporal Extent as an Open Period
8.6.3	Reduced Temporal Resolution
When specifying a temporal extent (and temporal position) a degree of temporal coordinate resolution should be used that is consistent with applicable business practices.
However, in the context of enterprise-wide data search, discovery and access it is necessary to ensure that a consistent interpretation of reduced-precision values of gml:timePosition is shared. To this end the following is recommended practice:
1.	The date/times reported for a gml:TimePeriod shall be inclusive in the period.
2.	Given a truncated specification of date/time (xsd:date, xsd:gYearMonth and xsd:gYear) for the start of a temporal extent, it shall be understood that for the year specified the gml:TimePeriod begins at:
o	the first month of the year when the month is not specified,
o	the first day of the month when the day is not specified,
o	the exact specified time when the fractional seconds are not specified, and
o	00:00:00.0Z when the time is not specified.
3.	Given a truncated specification of date/time (xsd:date, xsd:gYearMonth and xsd:gYear) for the end of a temporal extent, it shall be understood that for the year specified the gml:TimePeriod ends at:
o	the last month of the year when the month is not specified,
o	the last day of the month when the day is not specified,
o	the specified time plus 0.9 seconds when the fractional seconds are not specified, and
o	23:59:59.9Z when the time is not specified.
Consideration of these rules when preparing or using TSPI instance documents will ensure a consistent understanding of temporal extents.
8.7	Temporal Duration and Interval
8.7.1	Introduction
In ISO 19136:2007 (GML) the length of a time period is described using the XML Schema group gml:timeLength, whose content model is a choice of two property elements, either gml:duration or gml:timeInterval, as follows:
<group name="timeLength">
 <choice>
  <element ref="gml:duration"/>
  <element ref="gml:timeInterval"/>
 </choice>
</group> 
8.7.2	Temporal Duration
gml:duration conforms to the ISO 8601:2004, Data elements and interchange formats – Information interchange – Representation of dates and times syntax for temporal length as implemented by the xsd:duration type.
XML Schema Part 2: Datatypes Second Edition (W3C Recommendation 28 October 2004) Section 3.2.7 specifies the characteristics of this encoding as follows:
[Definition:]   duration represents a duration of time. The value space of duration is a six-dimensional space where the coordinates designate the Gregorian year, month, day, hour, minute, and second components defined in § 5.5.3.2 of [ISO 8601], respectively. These components are ordered in their significance by their order of appearance i.e. as year, month, day, hour, minute, and second.
The lexical representation for duration is the [ISO 8601] extended format PnYn MnDTnH nMnS, where nY represents the number of years, nM the number of months, nD the number of days, 'T' is the date/time separator, nH the number of hours, nM the number of minutes and nS the number of seconds. The number of seconds can include decimal digits to arbitrary precision.
The values of the Year, Month, Day, Hour and Minutes components are not restricted but allow an arbitrary unsigned integer, i.e., an integer that conforms to the pattern [0-9]+.. Similarly, the value of the Seconds component allows an arbitrary unsigned decimal. Following [ISO 8601], at least one digit must follow the decimal point if it appears. That is, the value of the Seconds component must conform to the pattern [0-9]+(\.[0-9]+)?. Thus, the lexical representation of duration does not follow the alternative format of § 5.5.3.2.1 of [ISO 8601].
An optional preceding minus sign ('-') is allowed, to indicate a negative duration. If the sign is omitted a positive duration is indicated. See also ISO 8601 Date and Time Formats (§D).
For example, to indicate a duration of 1 year, 2 months, 3 days, 10 hours, and 30 minutes, one would write: P1Y2M3DT10H30M. One could also indicate a duration of minus 120 days as: -P120D.
Reduced precision and truncated representations of this format are allowed provided they conform to the following:
    ● If the number of years, months, days, hours, minutes, or seconds in any expression equals zero, the number and its corresponding designator may be omitted. However, at least one number and its designator must be present.
    ● The seconds part •may• have a decimal fraction.
    ● The designator 'T' must be absent if and only if all of the time items are absent. The designator 'P' must always be present. 
For example, P1347Y, P1347M and P1Y2MT2H are all allowed; P0Y1347M and P0Y1347M0D are allowed. P-1347M is not allowed although -P1347M is allowed. P1Y2MT is not allowed.
The content model of the gml:duration element is as follows:
<element name="duration" type="duration"/>
8.7.3	Temporal Interval
gml:timeInterval conforms to ISO/IEC 11404:2007, Information technology – General-Purpose Datatypes (GPD), which is based on floating point values for temporal length. The content model of gml:timeInterval and its associated type, are as follows:
<element name="timeInterval" type="gml:TimeIntervalLengthType"/>
<complexType name="TimeIntervalLengthType" final="#all">
 <simpleContent>
  <extension base="decimal">
   <attribute name="unit" type="gml:TimeUnitType" use="required"/>
   <attribute name="radix" type="positiveInteger"/>
   <attribute name="factor" type="integer"/>
  </extension>
 </simpleContent>
</complexType>
ISO/IEC 11404 syntax specifies the use of a positive integer together with appropriate values for radix and factor. The resolution of the time interval is to one radix(-factor) of the specified time unit of measure.
For example: unit="second", radix="10", factor="3" specifies a resolution of milliseconds.
The value of the unit XML attribute is selected from the units of measure for time intervals as specified in ISO 31 Quantities and Units. The content model for gml:TimeUnitType as restricted for use in the TSPI Schema (see Section 8.4) is as follows:
<simpleType name="TimeUnitType">
 <restriction base="string">
  <enumeration value="year"/>
  <enumeration value="month"/>
  <enumeration value="day"/>
  <enumeration value="hour"/>
  <enumeration value="minute"/>
  <enumeration value="second"/>
 </restriction>
</simpleType>
8.7.4	Encoding
Depending on the intended semantic and most convenient expression either a duration or an interval may be used to encode a given time period. For example, to express a period length of 5 days, 14 hours and 30 minutes, either of the following XML instances are acceptable:
<duration>P5DT14H30M</duration>
<timeInterval unit="hour" radix="10" factor="0">134.5</timeInterval>
8.8	Temporal Uncertainty
Assessment of the quality of temporal data includes characterization of the precision of data values as well as quantitative and qualitative estimates of the accuracy and/or uncertainty of temporal characteristics. 
The National System for Geospatial Intelligence (NSG)  Metadata Foundation (NMF) is a profile of the conceptual schema for metadata defined by International Organization for Standardization (ISO) Technical Committee 211 (TC 211) Geographic Information / Geomantics.  Part 1 of the NMF profiles ISO 19115:2003/Cor 1:2006 to specify the minimum and recommended set of metadata elements required for the discovery and exchange of geospatial datasets in the NSG.
NGA.STND.0012-2_1.0 NSG Metadata Foundation (NMF) – Part 2: Quality Metadata extends that core to include descriptions of quality metadata associated with an NSG resource, where “quality” is defined in ISO 19101:2002 as “the totality of characteristics of a product that bear on its ability to satisfy stated and implied needs”. Data may be considered to be of high quality if it correctly represents the real-world construct to which it refers, e.g., temporal accuracy.
In coordination with the finalization of NGA.STND.0012-2_1.0, a Data Quality Measures information resource is being established in the DoD Data Services Environment (DSE) Metadata Registry (MDR); Annex A.5.5 describes those resources. Its initial content is based on ISO/DIS 19157-1, Geographic information – Data quality, a consolidation and revision of ISO 19113:2002,  ISO 19114:2006  and ISO/TS 19138:2006. 
Quality Measures relevant to temporal accuracy include:
•	Time accuracy at 68.3% significance level (Table D.56)
•	Time accuracy at 50% significance level (Table D.57)
•	Time accuracy at 90% significance level (Table D.58)
•	Time accuracy at 95% significance level (Table D.59)
•	Time accuracy at 99% significance level (Table D.60)
•	Time accuracy at 99.8% significance level (Table D.61)
The TSPI Schema shall only use those data quality measures that have been registered in this component of the GSIP Governance Namespace in the MDR.
[this section currently being revised in coordination with the ongoing review of the final-draft standard]


Annex A – Conventions
(Normative)
A.1	Introduction
This Annex establishes a set of conventions for XML component naming and design, schema referencing, and the structure and use of dynamic information resources that are applied throughout this specification.
A.2	Naming and Design Rules from GML
A.2.1	Introduction
The TSPI Schema is an ISO 19106-conformant Class 2 Profile of ISO 19136:2007 (GML). Although it does not constitute a GML-based application schema, it follows the applicable naming and design rules from GML such that users of the TSPI Schema may create GML-based application schemas when appropriate. Section 1.5 identified some of the benefits of this design approach.
A.2.2	Lexical Conventions
The GML schema follows several lexical conventions for the names of elements and complex types to assist in human comprehension of GML instance documents and schemas. These lexical conventions are as follows:
•	Objects are instantiated as XML elements with a conceptually meaningful name in UpperCamelCase. 
•	Properties are instantiated as XML elements whose name is in lowerCamelCase.
•	Abstract elements have a prefix “Abstract” (objects) or “abstract” (properties) prepended to their name.
•	Names of XML Schema complex types are in UpperCamelCase ending in the word “Type”.
•	Abstract XML Schema complex types have the word “Abstract” prepended.
These lexical conventions shall be followed in this TSPI specification.
While both ISO 19136:2007 (GML) and by ISO/TS 19103:2005 Geographic information – Conceptual schema language are ambiguous regarding the recommended approach to the naming of enumeration and code list literals, ISO/DIS 19103 (Draft International Standard, Second Edition) states that “Enumerated types are modeled as classifiers with attributes representing the allowed values; these attributes shall follow the naming conventions for regular attribute names and should be mnemonic.” Therefore this specification follows the lowerCamelCase convention for naming the literal values of enumerations and code lists.
A.2.3	XML Schema Conventions
The GML schema consists of W3C XML Schema components that define types and declare:
•	XML elements to encode GML objects with identity,
•	XML elements to encode GML properties of those objects, and
•	XML attributes qualifying those properties.
The GML schema, and profiles of the GML schema, is constrained as follows:
•	A GML object is an XML element of a type derived directly or indirectly from gml:AbstractGMLType. From this derivation, a GML object shall have a gml:id attribute.
•	A GML property shall not be derived from gml:AbstractGMLType, shall not have a gml:id attribute, or any other attribute of XML type ID.
•	An element is a GML property if and only if it is a child element of a GML object.
•	A GML object shall not appear as the immediate child of a GML object.
•	Consequently, no element may be both a GML object and a GML property.
•	All XML attributes declared in the GML schema are defined without namespace, the only exception is the gml:id XML attribute.
•	The use of additional XML attributes in a GML profile (and GML application schemas) is discouraged.
These XML Schema conventions shall be followed in this TSPI specification.
A.3	Referencing GML
A.3.1	GPAS Governance Namespace
ISO 19136:2007 (GML) is one of a family of public geospatial standards, specifications, schemas, and related documents that are available through the Internet. The Geospatial Publicly Available Specifications (GPAS) governance namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR) provides a configuration-controlled copy of these publicly available geospatial documents.
The GPAS namespace is governed as part of the DODENT (DoD Enterprise) governance namespace. Access to the content of the GPAS governance namespace through the MDR web-browser interface is through the path:
Governance Namespaces  DODENT  GPAS
Because the GPAS governance namespace is used as a repository of publicly available documents, the content of the GPAS governance namespace is organized by the publishing organization for a given document. The current GPAS hierarchy and the corresponding responsible standards organization is listed in Table 11. For each organization, the name of the sub-division within the GPAS governance namespace is listed. In addition, the right-most column lists the URL used for publication of the organization’s documents on the Internet. Additional sub-divisions of the GPAS governance namespace are added as additional requirements for documents, and their publishing organizations, are identified.
Table 11 – GPAS Document Organization
Publishing Organization	GPAS Division	Internet URL Reference
Open Geospatial Consortium, Inc. (OGC)	ogc	http://schemas.opengis.net
ISO TC211 Geographic information/Geomatics	iso	http://www.isotc211.org/schemas 
World Wide Web Consortium (W3C)	w3	http://www.w3.org
A.3.2	Referencing GPAS Schemas
XML schemas define the structure and syntax of XML instance documents. XML Schema Definition (XSD) files are used by many standards development organizations to define the content of XML instance documents that are conformant with their standards and specifications. In order to validate an XML instance document, access to the XSD is required. The GPAS governance namespace provides a mechanism for making XSD files available for DoD/IC users in environments where a copy of the MDR is available, but direct access to the Internet is not.
For each of the organization’s specifications maintained in the GPAS namespace, a Uniform Resource Locator (URL) is published to allow any corresponding schema document(s) to be directly accessible through the MDR. The general form of the URL for accessing a schema through the GPAS governance namespace on the MDR is:
http://metadata.ces.mil/mdr/ns/GPAS/schemas
For referencing XML schemas published in the GPAS governance namespace, the organization divisions identified in Table 11 are appended to the base schema location URL. The directory hierarchy used by the publishing organization for a given set of schemas is replicated for the schemas published in the GPAS governance namespace. Examples of the GPAS schema locations for each of the organizations identified Table 11 are listed in Table 12.
Table 12 – Example GPAS Schema Locations
Organization	Example Schema Location URLs
OGC	http://metadata.ces.mil/mdr/ns/GPAS/schemas/ogc/gml/3.2.1/gml.xsd
ISO TC211	http://metadata.ces.mil/mdr/ns/GPAS/schemas/iso/19139/TS_2007/gmx/catalogues.xsd
W3C	http://metadata.ces.mil/mdr/ns/GPAS/schemas/w3/1999/xlink/xlinks.xsd

XML schemas developed for general use within the DoD/IC or for a specific community of interest are able to include or import (as appropriate) these publicly available schemas directly from the MDR. Figure 46 illustrates how the schema location for the MDR-hosted ISO 19136:2007 (GML) schema is identified in an XSD.
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://www.w3.org/2001/XMLSchema"
    xmlns:gml="http://www.opengis.net/gml" version="">

  <import namespace="http://www.opengis.net/gml" schemaLocation="http://metadata.ces.mil/mdr/ns/GPAS/schemas/ogc/gml/3.2.1/gml.xsd"/>

   <!-- schema content omitted -->
</schema>
Figure 46 – Example Import of the GPAS-registered GML Schema
In an instance document based on a schema that has been registered (hosted) in the GPAS governance namespace, the schema location in the XML instance document can reference the MDR URL address corresponding to that schema. This is illustrated in Figure 47. 
<?xml version="1.0" encoding="UTF-8"?>
<gml:Dictionary xmlns:gml="http://www.opengis.net/gml"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.opengis.net/gml http://metadata.ces.mil/mdr/ns/GPAS/schemas/ogc/gml/3.2.1/gml.xsd">

   <!-- XML instance document content omitted -->
</gml:Dictionary>
Figure 47 – Example schemaLocation Usage of the GPAS-registered GML Schema 
A.3.3	Modifications to Publicly Available Schemas
XML schemas published through the GPAS namespace are not materially altered. The only modification that may be made is the alteration of the schema location of imported and included schemas required by the XML schema. There are two cases where the schema location will be altered:
1.	The published schema uses an absolute URL for an imported or included schema; or
2.	The published schema uses a local or duplicate copy of a schema that is also published in the GPAS governance namespace.
Registration of publicly available schemas through the GPAS governance namespace is intended to remove the dependency of any of the published schemas on access to non-DoD/IC assets. Where an XML schema references another XML schema through an absolute URL, the reference is changed to be relative to the XML schema within the GPAS governance namespace (this implies that the referenced schema has been registered in the GPAS governance namespace). This is intended to make GPAS-registered schemas “self-contained”, so that they can be reused without dependencies on non-DoD/IC assets. The fragment in Figure 48 illustrates this change. The import statement (in red) is deleted and replaced with the import statement (in green) that follows it. The example file is:
http://metadata.ces.mil/mdr/ns/GPAS/schemas/iso/19139/TS_2007/gss/geometry.xsd
The GML file to be imported is: 
http://metadata.ces.mil/mdr/ns/GPAS/schemas/ogc/gml/3.2.1/gml.xsd
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://www.w3.org/2001/XMLSchema"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     xmlns:gco="http://www.isotc211.org/2005/gco"
     xmlns:gml="http://www.opengis.net/gml"
     xmlns:gss="http://www.isotc211.org/2005/gss"
     targetNamespace="http://www.isotc211.org/2005/gss"
     elementFormDefault="qualified" version="0.1">

  <import namespace="http://www.opengis.net/gml/3.2" schemaLocation="http://schemas.opengis.net/gml/3.2.1/gml.xsd"/>

  <import namespace="http://www.opengis.net/gml/3.2" schemaLocation="../../../../ogc/gml/3.2.1/gml.xsd"/>

   <!-- schema content omitted -->
</schema>
Figure 48 – Example Change of Absolute to Relative URL for an Imported Schema
For convenience, some XML schemas may exist on multiple sites or as parts of different sets of XML schemas. An example of this is the XML Linking Language (XLink) schema based upon the corresponding W3C recommendation. During development of GML, for example, no XSD for XLink was published by W3C. As a result, the GML development team created a local-copy XSD for XLink.
The XLink XSD is registered (hosted) in the GPAS governance namespace through the w3 directory. References to it within the GPAS-registered GML schemas have been changed from the copy otherwise expected to be found in the ogc directory to the copy maintained in the w3 directory.
For example, both the family of TC211 schemas and the family of OGC schemas contain an XLink XSD file in their directory hierarchy. To eliminate this redundancy in the GPAS governance namespace, the xlinks.xsd file is registered in the w3 GPAS sub-division and is accessible using the URL:
http://metadata.ces.mil/mdr/ns/GPAS/schemas/w3/1999/xlink/xlinks.xsd
An example result of redundancy elimination is illustrated in Figure 49, from the file:
http://metadata.ces.mil/mdr/ns/GPAS/schemas/iso/19139/TS_2007/gco/gcoBase.xsd
The import statement (in red) is deleted and replaced with the import statement (in green) that follows it, which (correctly) references the GPAS-registered xlinks.xsd file.
<?xml version="1.0" encoding="UTF-8"?>
<schema targetNamespace="http://www.isotc211.org/2005/gco"
     elementFormDefault="qualified" attributeFormDefault="unqualified"
     xmlns:gco="http://www.isotc211.org/2005/gco"
     xmlns="http://www.w3.org/2001/XMLSchema"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     xmlns:gml="http://www.opengis.net/gml">

  <import namespace="http://www.w3.org/1999/xlink" schemaLocation="../xlink/xlinks.xsd"/>

  <import namespace="http://www.w3.org/1999/xlink" schemaLocation="../../../../w3/1999/xlink/xlinks.xsd"/>

  <!-- schema content omitted -->
</schema>
Figure 49 – Example Change of URL Reference to a Local Relative URL
It is a recommended practice that users of the TSPI Schema intending to use types from the XLink schema use, directly or indirectly, the copy that has been registered in the GPAS Governance Namespace of the MDR.
A.3.4	XML Schema Namespace Identifiers
The term Namespace can have two connotations when dealing with the MDR. The MDR supports Governance Namespaces which are used to register documents, schemas, etc. in logical groupings for discovery and reuse by the DoD/IC community. The GPAS is an example of an MDR Governance Namespace.
XML Namespaces are used to organize XML schema definitions for reuse. Names of XML objects (element, complex type, etc.) are required to be unique within an XML namespace for that type of object. The XML Namespace for ISO 19136:2007 (GML) is encoded as a URL and is:
http://www.opengis.net/gml/3.2
Within this XML namespace, there can be only one element definition for the element named Point. This ensures that, within the GML namespace, the element Point has one unique definition. It also allows other XML namespaces to define an element named Point with a (potentially different) meaning specific to that namespace that does not conflict with the same-named element in the GML namespace.
XML Namespaces are identified using a Uniform Resource Identifier (URI). The URI is used to identify the XML schema namespace for which the schema contains definitions. The URI can be implemented as either a Uniform Resource Name (URN) or as a URL, depending upon the preference of the schema author. For example, the Intelligence Community Information Security Markup (ICISM) schema uses a URN to identify the ICISM namespace which is:
urn:us:gov:ic:ism
When a URL is used, the URL may be crafted so that it can also be used as a web reference related to the XML namespace. This is the case of the GML namespace identifier listed above. This dual use of a URL as both an XML namespace and as a web resource address is a convenience and is not required for XML schema and instance document validation.
The XML Namespace identifier chosen by the organization publishing the schemas registered in the GPAS is part of the schema content and should not be changed. For this reason, XML schema namespace identifiers for publicly available schemas are unchanged for schemas registered in the GPAS governance namespace. 
A.4	Referencing TSPI
A.4.1	GSIP Governance Namespace
This TSPI specification is one of a family of DoD/IC geospatial standards, specifications, schemas, and related documents that either constitute the GEOINT Structure Implementation Profile (GSIP) or are closely associated with it. The GSIP governance namespace in the the DoD Data Services Environment (DSE) Metadata Registry (MDR) provides a configuration-controlled copy of these DoD geospatial documents.
The GSIP namespace is governed as part of the GEOINT (Geospatial Intelligence) namespace under the DODENT (DoD Enterprise) governance namespace. Access to the content of the GSIP governance namespace through the MDR web-browser interface is through the path:
Governance Namespaces  DODENT  GEOINT GSIP
A.4.2	TSPI XML Namespace
An XML namespace provides a simple method for qualifying element and attribute names used in XML documents by associating them with namespaces identified by URI references. They are the primary mechanism for preventing name collisions in and across schemas. The qualification mechanism is known as the namespace prefix. For the TSPI Schema the following assignments shall apply:
XML Namespace Prefix:	tspi
XML Namespace:	http://metadata.ces.mil/mdr/ns/GSIP/tspi
Name:	Time-Space-Position Information
XML Namespace Prefix:	tspi-core
XML Namespace:	http://metadata.ces.mil/mdr/ns/GSIP/tspi
Name:	Time-Space-Position Information Core Types
XML Namespace Prefix:	tspi-ext
XML Namespace:	http://metadata.ces.mil/mdr/ns/GSIP/tspi
Name:	Time-Space-Position Information Extensions

A.5	Information Resources
A.5.1	Introduction
The MDR may be used to ensure the persistence of a variety of information resources (e.g., XSD files). Each information resource may be bound to a unique URL that provides both identity for that resource and access to that resource. Through replication, the MDR provides a mechanism for making information resources available for DoD/IC users in environments where a copy of the MDR is available but direct access to the Internet is not (e.g., in DIL (Disconnected, Intermittent, or Low-bandwidth) situations, including secure enclaves).
In support of the National System for Geospatial Intelligence (NSG) the GEOINT Standards Working Group (GWG) maintains multiple information resources in the MDR. The management of MDR-provisioned information resources is accomplished through mechanisms established in governance namespaces by their managers. Both the GPAS and GSIP Governance Namespaces are governed at two levels of granularity: schemas (and related documents) and schema items (e.g., elements, datatypes, and datatype domain values).
Annex A.2 described one aspect of schema-level governance. This section describes some aspects of schema item-level governance.
A.5.2	Coordinate Reference System Resources
The GEOINT Standards Working Group (GWG) maintains a set of Coordinate Reference System (CRS) information resources in the MDR. They may be accessed at:
http://metadata.ces.mil/mdr/ns/GSIP/crs/
The TSPI Schema shall only use those CRS that have been registered in this component of the GSIP Governance Namespace in the MDR.
Registered CRS are identified by URIs composed from the ~/GSIP/crs/ base URL plus a short CRS-specific identifier. For example, in the case of the World Geodetic System 1984 - Geographic, 2-Dimensional CRS, this identification is by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
Each such URI has a corresponding CRS-specific accessible information resource – a GML-conformant instance document. Section 5.3.1.6 specifies the nature of this XML instance document resource in greater detail.
Specification of CRS “by reference” in the MDR-hosted CRS information resource(s) allows for dynamic support for CRS independent of evolution of the TSPI Schema itself. It also avoids the overhead of exchanging CRS specification(s) as part of individual TSPI instance documents by instead promulgating “well-known CRS identifiers”(and their specifications) in the DoD/IC. Both the DoD Discovery Metadata Specification (DDMS) and Universal Core (UCore) v2.0.0 employ this mechanism.
A.5.3	Code List Resources
A.5.3.1	Fixed Enumerations
The values of domains whose allowed values can be completely listed are termed enumerations and may be established both as sets and as (contained) individual domain value items. XML Schema Part 2: Datatypes Second Edition (W3C Recommendation 28 October 2004) Section 4.3.5 specifies the characteristics of this encoding as follows: 
[Definition:]   enumeration constrains the value space of a specified set of values.  enumeration does not impose an order relation on the value space it creates; the value of the ordered property of the derived datatype remains that of the datatype from which it is derived.  enumeration provides for: 
Constraining a value space to a specified set of values. 
The following example is a datatype definition for a user-derived datatype which limits the values of dates to the three US holidays enumerated. This datatype definition would appear in a schema authored by an "end-user" and shows how to define a datatype by enumerating the values in its value space. The enumerated values must be type-valid literals for the base type. 
<simpleType name='holidays'>
    <annotation>
        <documentation>some US holidays</documentation>
    </annotation>
    <restriction base='gMonthDay'>
      <enumeration value='--01-01'>
        <annotation>
            <documentation>New Year's day</documentation>
        </annotation>
      </enumeration>
      <enumeration value='--07-04'>
        <annotation>
            <documentation>4th of July</documentation>
        </annotation>
      </enumeration>
      <enumeration value='--12-25'>
        <annotation>
            <documentation>Christmas</documentation>
        </annotation>
      </enumeration>
    </restriction>
</simpleType>

There exist enumeration datatypes whose listed domain values are subject to change, evolving over time as new values are added and old values are either retired or superseded by new values; e.g., country names (renaming of “Burma” to the “Union of Myanmar”, or the retirement of the name “Union of Soviet Socialist Republics”). The rate of change may be relatively slow (e.g., the set of country names) or relatively fast (e.g., the set of Earth-imaging satellites).
Revising the domain of an enumeration datatype requires publishing a new version of the schema since it constitutes a revision to a schema-specified type.
A.5.3.2	Flexible Enumerations
For relatively quickly changing enumerations it can become onerous to have to publish a new version of a schema whenever the set of domain values has changed. In these cases it is valuable to replace an enumeration by a code list. A code list is a flexible enumeration that specifies an unambiguous identifier using a consistent representation for each member in a set of domain values (e.g., country codes or units of measure). A code list can be used to specify an open enumeration and should be used if only the likely or an initial set of allowed values are known at schema-creation time.
When a code list value is instantiated in an XML instance document, two identifiers are provided – codeList and codeListValue – where:
•	The codeList specifies a remote resource in which the code list domain is defined.
•	The codeListValue is the coded value from the specified (remote resource code list) domain that encodes the concept intended (denoted) in the XML instance document.
Figure 50 illustrates a use of such a code list value in a XML instance document, and Figure 51 the alternative (traditional) use of an enumeration value.
<?xml version="1.0" encoding="UTF-8"?>
<tspi-core:Container xmlns:nas="http://metadata.ces.mil/mdr/ns/GSIP/tspi">
  <!-- some elements omitted from this illustration -->

  <CountryCode codeList="http://metadata.ces.mil/mdr/ns/GPAS/codelist/iso3166-1/digraph" codeListValue="FR"/>

  <!-- some elements omitted from this illustration -->
</tspi-core:Container>
Figure 50 – Example Codelist Instance Document Fragment
<?xml version="1.0" encoding="UTF-8"?>
<tspi-core:Container xmlns:nas="http://metadata.ces.mil/mdr/ns/GSIP/tspi">
  <!-- some elements omitted from this illustration -->

  <CountryCode>FR</CountryCode>

  <!-- some elements omitted from this illustration -->
</tspi-core:Container>
Figure 51 – Example Enumeration Instance Document Fragment
These two styles may be combined by extending the traditional enumeration type with the codeList-pair of XML attributes, asserting a mutual-exclusion constraint so that valid instance documents employ only one of the two mechanisms in ease use, and then carefully managing the code list resource to ensure upwards-compatibility from any given schema release. Figure 52 illustrates a use of such a code list.
<?xml version="1.0" encoding="UTF-8"?>
<schema targetNamespace="http://metadata.ces.mil/mdr/ns/GSIP/tspi"
     elementFormDefault="qualified" attributeFormDefault="unqualified"
     xmlns:tspi="http://metadata.ces.mil/mdr/ns/GSIP/tspi"
     xmlns="http://www.w3.org/2001/XMLSchema"
     xmlns:sch="http://purl.oclc.org/dsdl/schematron" 
     xmlns:gml="http://www.opengis.net/gml/3.2">

  <annotation>
    <appinfo>
     <sch:title>TSPI Schematron validation</sch:title>
     <sch:ns prefix="tspi" uri="http://metadata.ces.mil/mdr/ns/GSIP/tspi"/>
    </appinfo>
  </annotation>

  <element name="Country" type="tspi-core:CountryCodeType">
    <annotation>
      <appinfo>
        <sch:pattern id="CountryFlexibleEnum">
          <sch:rule context="tspi-core:Country">
            <sch:assert test="count(@codeList)=count(@codeListValue) and count(@codeList)=1 implies .='' and count(@codeList)=0 implies .!=''">
            Either the code list and value must be specified or the country code itself must be specified, but not both.
            </sch:assert>
          </sch:rule>
        </sch:pattern>
      </appinfo>
    </annotation>
  </element>

  <simpleType name="CountryCodeEnumerationType">
    <restriction base="string">
      <enumeration value="DE"/>
      <enumeration value="US"/>
      <enumeration value="CA"/>
      <!-- some enumerants omitted from this illustration -->
    </restriction>
  </simpleType>

  <complexType name="CountryCodeType">
    <simpleContent>
      <extension base="tspi-core:CountryCodeEnumerationType">
        <attribute name="codeList" type="anyURI" use="optional"/>
        <attribute name="codeListValue" type="anyURI" use="optional"/>
      </extension>
    </simpleContent>
  </complexType>

  <!-- further schema content omitted -->
</schema>
Figure 52 – Example Flexible Enumeration Schema Fragment
This design pattern is employed in the TSPI Schema.
Note that code lists may be extended by a user of the schema by defining their own codeList resource and included codeListValues. Business practices may either encourage or preclude such uses.
A.5.3.3	Managed Code Lists
The TSPI Schema employs managed code lists. The GEOINT Standards Working Group (GWG) maintains a set of code list information resources in the MDR. They may be accessed at either:
http://metadata.ces.mil/mdr/ns/GPAS/codelist/
http://metadata.ces.mil/mdr/ns/GSIP/codelist/
The TSPI Schema shall only use those code lists that have been registered in these components of the GPAS and GSIP Governance Namespaces in the MDR.
Registered code lists are identified by URIs composed from the ~/codelist/ base URL plus a short code list-specific identifier. For example, in the case of the Horizontal Resolution Type, this identification is by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/codelist/horizResolutionType
Each such URI has a corresponding code list-specific accessible information resource – a GML-conformant instance document.
A.5.3.4	Code List Item References
The GEOINT Standards Working Group (GWG) maintains a set of code list item (enumerant) information resources in the MDR. They may be accessed at:
http://metadata.ces.mil/mdr/ns/GPAS/codelist/[...]/
http://metadata.ces.mil/mdr/ns/GSIP/codelist/[...]/
For example, the TSPI Schema defines a pair of categorical resolution enumerations for use in extending GML geometry specifications.  These enumerations are defined as part of tspi.xsd, but are employed as flexible enumerations (see Annex A.5.3.2) and may be extended. They are identified by the URIs:
http://metadata.ces.mil/mdr/ns/GSIP/codelist/horizResolutionType
http://metadata.ces.mil/mdr/ns/GSIP/codelist/vertResolutionType
Registered code list item values are identified by URIs composed from the appropriate ~/codelist/ base URL plus the code list-type identifier plus a short code list-specific item (enumerant) identifier. The code list-type identifier and enumerant-specific identifier correspond, respectively, to a codeList and a codeListValue as specified in Annex A.5.3.2. The codeListValue values for code list items (enumerants) are specified in accordance with the lowerCamelCase convention (see Annex A.2).
For example, in the case of the “decametre” code list items (enumerants) of the Horizontal Resolution Type and Vertical Resolution Type code lists, these identifications are by the URIs:
http://metadata.ces.mil/mdr/ns/GSIP/codelist/horizResolutionType/decametre
http://metadata.ces.mil/mdr/ns/GSIP/codelist/vertResolutionType/decametre
Each such URI has a corresponding code list-specific accessible information resource – a GML-conformant instance document. 
A.5.4	Physical Quantity and Unit of Measure Resources
A.5.4.1	Introduction
Measures are employed in both metadata and data resources to characterize the values of properties. A measure is the result of performing the act or process of ascertaining the extent, dimensions, or quantity of some entity. A measure has an accompanying “unit” that is a reference quantity chosen from a category of mutually comparable physical quantities, e.g., second (time category), metre (length category), or kilogram (mass category).
This TSPI specification supports the standardized units of measure specified by ISO 80000 Quantities and Units (also known as the International System of Units (SI)) in conjunction with the conceptual schema for measures specified by ISO/TS 19103:2005 Geographic information – Conceptual schema language. Non-standard “conventional” units of measure are also supported (e.g., English Units, Imperial units, and U.S. customary units), as required.
A.5.4.2	Radix Point Presentation
In specifying the presentation of numeric quantities having fractional parts this specification recognizes international variation in the presentation of the radix point. The radix point is the symbol used in numerical representations to separate the integral part of the number (to the left of the radix) from its fractional part (to the right of the radix).
The radix point mark is usually a small dot, either placed on the baseline or halfway between the baseline and the top of the numerals. In base-10, the radix point is more commonly called the decimal point; radix point, however, is the more general term used for other bases. In many non-English speaking countries, a comma ',' is used instead of a period '.' as the radix point mark.
This specification always uses the period '.' as the radix point mark, however the schema implementation allows for other choices.
A.5.4.3	SI Prefixes
The TSPI specification adopts the SI nomenclature for prefixing units of measure with standardized decimal multiples and submultiples. SI prefixes are used to reduce the number of zeros shown in numerical quantities. For example, one-thousandth of an arc degree (a planar angle) can be written as 0.001 arc degree. Using an SI prefix, this is equivalent to 1 arc millidegree.
This specification extends SI prefixes in order to define a consistent notation for the naming of XML elements and types; the applicable SI and extended-SI prefixes are listed in Table 13.
Table 13 – Unit of Measure Prefixes
Name	Multiple	Description	Note
mega 	106	1,000,000	
hectokilo	105	100,000	Extended from SI
decakilo	104	10,000	Extended from SI
kilo 	103	1,000	
hecto 	102	100	
deca 	101	10	
uni 	100	1	
deci 	10-1	0.1	
centi 	10-2	0.01	
milli 	10-3	0.001	
decimilli	10-4	0.0001	Extended from SI
centimilli	10-5	0.00001	Extended from SI
micro   	10-6 	0.000001	

In specifying members of categories of mutually comparable physical quantities (e.g., length) this specification includes not only base units (e.g., metre and foot) but also prefixed-units (e.g., kilometre, millimetre and kilofoot).
A.5.4.4	Measures and Units of Measure
ISO 19136:2007 (GML) specifies the gml:MeasureType to support recording an amount encoded as a value of XML Schema xsd:double, together with a unit of measure indicated by an XML attribute uom – short for “unit of measure”. The value of the uom attribute identifies a reference system for the amount, usually a ratio or interval scale.
The complex type gml:MeasureType is defined as follows:
<complexType name="MeasureType">
  <simpleContent>
    <extension base="double">
      <attribute name="uom" type="gml:UomIdentifier" use="required"/>
    </extension>
  </simpleContent>
</complexType>

For example, an XML schema may contain an element declaration using this type: 
<element name="height" type="gml:MeasureType"/>

Elements corresponding to this might appear in an XML instance document as follows:
<height uom="m">1.4224</height>
<height uom="http://www.equestrian.org/units/hands">14</height>

In each case the value of the uom attribute identifies either the unit of measure directly or a resource that defines the unit of measure. 
The simple type gml:UomIdentifer defines the syntax and value space of the unit of measure identifier. This is a union type defined as follows:
<simpleType name="UomIdentifier">
  <union memberTypes="gml:UomSymbol gml:UomURI"/>
</simpleType>

The first member of the union type, gml:UomSymbol, is defined as follows:
<simpleType name="UomSymbol">
   <restriction base="string">
    <pattern value="[^: \n\r\t]+"/>
  </restriction>
</simpleType>

This type specifies a character string of length at least one, and restricted such that it must not contain any of the following characters: “:” (colon), “ ” (space), (new line), (carriage return), (tab). This allows values corresponding to familiar abbreviations, such as “kg”, “m/s”, etc.
The second member of the union type, gml:UomURI, is defined as follows:
<simpleType name="UomURI">
  <restriction base="anyURI">
    <pattern value="([a-zA-Z][a-zA-Z0-9\-\+\.]*:|\.\./|\./|#).*"/>
  </restriction>
</simpleType>

This type specifies a URI, restricted such that it must start with one of the following sequences: “#”, “./”, “../”, or a string of characters followed by a “:”.  These patterns ensure that the most common URI forms are supported, including absolute and relative URIs and URIs that are simple fragment identifiers, but prohibit certain forms of relative URI that could be mistaken for unit of measure symbol, e.g., “m/s”. 
In an instance document, on elements of type gml:MeasureType the mandatory uom attribute shall carry a value corresponding to either:
•	a conventional unit of measure symbol; or
•	a link to a definition of a unit of measure that does not have a conventional symbol, or when it is desired to indicate a precise or variant definition.
For the latter purpose, units of measure dictionaries may be established based on appropriate GML components. 
A.5.4.5	Unit of Measure Dictionaries
In accordance with ISO 19136:2007 (GML) Clause 16.2 Units schema, units of measure may be unambiguously specified, their relationships and conversion factors documented (where appropriate), and dictionaries of units of measure established.
Figure 53 illustrates a use of the GML units schema to establish a hypothetical GML dictionary (see ISO 19136:2007 Clause 15.2 Dictionary schema) corresponding to the base and derived units defined by ISO 31 Quantities and Units, plus a selection of conventional units to illustrate the usage of these GML components.
<gml:Dictionary gml:id="unitsDictionary">
 <gml:description>A dictionary of units of measure</gml:description>
 <gml:identifier codeSpace="http://friendly.com/UOM">My Units</gml:identifier>

 <gml:dictionaryEntry>
  <gml:Dictionary gml:id="SIBaseUnits">
   <gml:description>The Base Units from the SI units system.</gml:description>
   <gml:identifier codeSpace="http://friendly.com">SI BaseUnits</gml:identifier>

   <gml:dictionaryEntry>
    <gml:BaseUnit gml:id="m">
     <gml:description>The metre is the length of the path travelled by light in vacuum during a time interval of 1/299 792 458 of a second.</gml:description>
     <gml:identifier codeSpace="http://www.bipm.fr/en/3_SI/base_units.html">metre</gml:identifier>
     <gml:name xml:lang="en/US">metre</gml:name>
     <gml:quantityType>length</gml:quantityType>
     <gml:catalogSymbol codeSpace="http://www.bipm.fr/en/3_SI/base_units.html">m</gml:catalogSymbol>
     <gml:unitsSystem xlink:href="http://www.bipm.fr/en/3_SI"/>
    </gml:BaseUnit>
   </gml:dictionaryEntry>
   <!-- further content omitted -->
  </gml:Dictionary>
 </gml:dictionaryEntry>

 <gml:dictionaryEntry>
  <gml:Dictionary gml:id="SIDerivedUnits">
   <gml:description>The Derived Units from the SI units system. These are all derived as a product of SI Base Units, except degrees Celsius in which the conversion formaula to the SI Base Unit (kelvin) involves an offset. </gml:description>
   <gml:identifier codeSpace="http://friendly.com">SI DerivedUnits</gml:identifier>

   <gml:dictionaryEntry>
    <gml:DerivedUnit gml:id="rad">
     <gml:identifier codeSpace="http://www.bipm.fr/en/3_SI">radian</gml:identifier>
     <gml:quantityType>plane angle</gml:quantityType>
     <gml:catalogSymbol codeSpace="http://www.bipm.fr/en/3_SI">rad</gml:catalogSymbol>
     <gml:derivationUnitTerm uom="#m" exponent="1"/>
     <gml:derivationUnitTerm uom="#m" exponent="-1"/>
    </gml:DerivedUnit>
   </gml:dictionaryEntry>
   <!-- further content omitted -->
  </gml:Dictionary>
 </gml:dictionaryEntry>

 <gml:dictionaryEntry>
  <gml:Dictionary gml:id="ConventionalUnitsDictionary">
   <gml:description>A collection of Conventional Units. These are units of measure which are either widely used or important within a specific community. For most of these there is
1. a known derivation from more primitive units, which may or may not be SI Base Units, or
2. a known conversion to a preferred unit, which may or may not be an SI Base or Derived unit, through rescaling and offset,
or both.</gml:description>
   <gml:identifier codeSpace="http://friendly.com">Conventional</gml:identifier>

   <gml:dictionaryEntry>
    <gml:DerivedUnit gml:id="m3">
     <gml:identifier codeSpace="http://friendly.com">cubic metre</gml:identifier>
     <gml:quantityType>Volume</gml:quantityType>
     <gml:derivationUnitTerm uom="#m" exponent="3"/>
    </gml:DerivedUnit>
   </gml:dictionaryEntry>

   <gml:dictionaryEntry>
    <gml:ConventionalUnit gml:id="l">
     <gml:identifier codeSpace="http://friendly.com">litre</gml:identifier>
     <gml:quantityType>Volume</gml:quantityType>
     <gml:conversionToPreferredUnit uom="#m3">
      <gml:factor>0.001</gml:factor>
     </gml:conversionToPreferredUnit>
    </gml:ConventionalUnit>
   </gml:dictionaryEntry>
   <!-- further content omitted -->
  </gml:Dictionary>
 </gml:dictionaryEntry>
</gml:Dictionary>
Figure 53 – Example GML Units of Measure Dictionary
A.5.4.6	Unit of Measure References
The GEOINT Standards Working Group (GWG) maintains a set of physical quantity and commensurate units of measure (UoM) information resources in the MDR. They may be accessed at:
http://metadata.ces.mil/mdr/ns/GSIP/uom/
The TSPI Schema shall only use those UoM that have been registered in this component of the GSIP Governance Namespace in the MDR.
In a TSPI instance document, on elements of type (or derived from type) gml:MeasureType the mandatory uom attribute shall carry a value (gml:UomURI) corresponding to a URI identifying a registered unit of measure.
That URI is an identifier of a reference quantity chosen from a category of mutually comparable physical quantities. Each such category is established as a separate MDR resource and associated GML units of measure dictionary, for example:
length/	length quantities (e.g., “metre”, “foot”, “fathom”, “nauticalMile”)
area/	area quantities (e.g., “squareMetre”, “squareFoot”)
volume/	volume quantities (e.g., “cubicMetre”, “liter”, “usGallon”)
planeAngle/	plane angle quantities (e.g., “radian”, “arcDegree”, “grad”)
speed/	speed quantities (e.g., “metrePerSecond”, “milePerHour”)
time/	time quantities (e.g., “second”, “minute”, “hour”, “day”)
pureNumber/	pure number quantities (e.g., “unitless”, “percent”, “deciMachNumber”)
In addition, there is a separate MDR resource (and associated GML units of measure dictionary) for those units of measure that are not a member of any category of mutually comparable physical quantities:
noncomparable/	non-comparable physical quantities (e.g., “flightLevel”)
Registered UoM are identified by URIs composed from the ~/GSIP/uom/ base URL plus the quantity-type identifier plus a short UoM-specific identifier. The quantity-type identifier and UoM-specific identifier correspond, respectively, to a codeList and a codeListValue as specified in Section 4.3.3. The codeListValue values for UoM are specified in accordance with the lowerCamelCase convention (see Annex A.2).
In the case of the “metre” unit of measure, this identification is by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/uom/length/metre
Each such URI has a corresponding UoM-specific accessible information resource – a GML-conformant instance document. 
Specification of UoM “by reference” in the MDR-hosted units of measure information resource allows for dynamic support for units of measure independent of evolution of the TSPI specification itself. It ensures that UoM in GML-based XML instance documents can be validated against type-specific sets of comparable physical quantities (e.g., the employment of only a registered “length” UoM, thus excluding the erroneous use of the “arcDegree” UoM). Schematron assertions (see Annex A.6) may be used to assert additional constraints on the allowed values of UoM for individual measures in a domain-specific schema.
Specification of UoM “by reference” also supports unambiguous documentation of the exact relationships among units of measure in the same category of comparable physical quantities and accordingly the exact conversion of quantity values specified in accordance with different units of measure. It does so without imposing unnecessary burden on XML instance documents.
A.5.5	Data Quality Measure Resources
Data quality measures specify technical methods that may be used to assess the quality of a data resource and its fitness for use (e.g., horizontal positional accuracy). The GEOINT Standards Working Group (GWG) maintains a set of data quality measure information resources in the MDR. They may be accessed at:
http://metadata.ces.mil/mdr/ns/GSIP/dq/
The TSPI Schema shall only use those data quality measures that have been registered in this component of the GSIP Governance Namespace in the MDR.
[this section currently being revised in coordination with the ongoing review of the NGA.STND.0012-2_1.0 NSG Metadata Foundation (NMF) – Part 2: Quality Metadata, Version 1.0 (draft), 20 February 2011 ]
A.5.6	Void Values
ISO 19136:2007 (GML) specifies a mechanism to support content models that require (or allow) recording of an explanation for a void value or other exception. The simple type gml:NilReasonType is defined as follows:
<simpleType name="NilReasonEnumeration">
 <union>
  <simpleType>
   <restriction base="string">
    <enumeration value="inapplicable"/>
    <enumeration value="missing"/>
    <enumeration value="template"/>
    <enumeration value="unknown"/>
    <enumeration value="withheld"/>
   </restriction>
  </simpleType>
  <simpleType>
   <restriction base="string">
    <pattern value="other:\w{2,}"/>
   </restriction>
  </simpleType>
 </union>
</simpleType>
 
<simpleType name="NilReasonType">
 <union memberTypes="gml:NilReasonEnumeration anyURI"/>
</simpleType>

The semantics of the enumerated values of gml:NilReasonType are as follows:
•	"inapplicable": there is no value;
•	"missing": the correct value is not readily available to the sender of this data. – furthermore, a correct value may not exist;
•	"template": the value will be available later;
•	"unknown": the correct value is not known to, and not computable by, the sender of this data – however, a correct value probably exists;
•	"withheld": the value is not divulged;
•	"other:"+text: other brief explanation, where text is a string of two or more characters with no included spaces; and
•	anyURI: should refer to a resource which describes the reason for the exception.
A particular community may choose to assign more detailed semantics to the standard values provided. Alternatively, the URI method enables a specific or more complete explanation for the absence of a value to be provided elsewhere and indicated “by reference” in an instance document.
gml:NilReasonType may be used as a member of a union in a simple content type where it is necessary to permit a value from the NilReasonType union as an alternative to the primary type.
The XML Schema attribute nillable may be included in any element declaration within a schema. By default the schema attribute nillable has a value of “false”. By declaring an element as nillable (nillable ="true"), an instance of that element may omit its content in cases where an empty value would normally not be schema valid by supplying an attribute nil from the XML Schema Instance namespace with the value “true”.
In some situations where it is required to declare an element in an application schema nillable, it may be convenient to also add an attribute of type gml:NilReasonType. For example:
<element name="amount" nillable="true">
 <complexType>
  <simpleContent>
   <extension base="double">
    <attribute name="nilReason" type="gml:NilReasonType"/>
   </extension>
  </simpleContent>
 </complexType>
</element>
would allow the instances to be augmented with an additional attribute explaining the absence of a value,  such as:
   <amount xsi:nil="true" nilReason="unknown"/> 
A.6	Data Validation
ISO/IEC 19757-3 defines the Schematron Document Schema Definition Language (DSDL) that may be used to specify one or more validation processes to be performed against XML instance documents. Schematron is a rule-based validation language for making assertions about the presence or absence of patterns in XML trees. It is a simple and powerful structural schema language expressed in XML using a small number of elements and XPath (a query language for selecting nodes from an XML document). It may be employed as an adjunct to the structural validation capabilities of XSD – testing for co-occurrence constraints, non-regular constraints, and inter-document constraints.
The W3C XML Schema recommendations allow applications to extend schema validation by adding application specific data in appinfo elements within the annotation of a particular schema element. One can embed sch:pattern elements within these extension blocks, which can then be applied as part of the schema validation process. Namespaces that are used by patterns are declared in an annotation at the top level of the schema using ns elements.
An example of an embedded Schematron validation pattern is illustrated in Figure 54, where a test has been added to ensure that only srsName XML attribute values that are registered in the MDR may occur in TSPI instance documents containing the tspi-core:PointType.
<?xml version="1.0" encoding="UTF-8"?>
<sch:schema
  xmlns:sch="http://purl.oclc.org/dsdl/schematron"
  xmlns:gml="http://www.opengis.net/gml/3.2"
  xmlns:gmlce="http://www.opengis.net/gml/3.3/ce"
  xmlns:xlink="http://www.w3.org/1999/xlink"
  xmlns:tspi="http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0"
  xmlns:tspi-core="http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0/core"
  xmlns:tspi-ext="http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0/ext"
  xml:lang="en">
    
  <sch:title>TSPI Schematron validation</sch:title>
  
  <sch:ns prefix="sch" uri="http://purl.oclc.org/dsdl/schematron"/>
  <sch:ns prefix="gml" uri="http://www.opengis.net/gml/3.2"/>
  <sch:ns prefix="gmlce" uri="http://www.opengis.net/gml/3.2/ce"/>
  <sch:ns prefix="xlink" uri="http://www.w3.org/1999/xlink"/>
  <sch:ns prefix="ism" uri="urn:us:gov:ic:ism"/>
  <sch:ns prefix="tspi" uri="http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0"/>
  <sch:ns prefix="tspi-core" uri="http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0/core"/>
  <sch:ns prefix="tspi-ext" uri="http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0/ext"/>
  
  <sch:let name="GSIP" value="'http://metadata.ces.mil/mdr/ns/GSIP'"/>

  <sch:pattern id="PointSrsName_Valid_in_Resource">
    <sch:rule context="tspi-core:PointType">
      <sch:assert test="starts-with(@srsName, concat($GSIP, '/crs'))">
        The CRS must be from the set registered
            in the MDR GSIP Governance Namespace.</sch:assert>
      <sch:assert test="document(@srsName)">
        The specified srsName must reference a net-accessible resource
            in the MDR GSIP Governance Namespace.</sch:assert>
      <!-- Verify that the content of the resource matches the instance document -->
      <sch:assert test="concat(substring-before(@srsName, '/crs'),'/crs') = 
                        document(@srsName)//gml:identifier/@codeSpace">
        The body of the srsName must match the codeSpace of the identifier
            in the resource.</sch:assert>
      <sch:assert test="substring-after(@srsName, 'crs/') = 
                        document(@srsName)//gml:identifier">
        The tail of the srsName
        ('<sch:value-of select="substring-after(@srsName, 'crs/')"/>')
        must match the value of the identifier in the resource.</sch:assert>
    </sch:rule>
  </sch:pattern>

</schema>
Figure 54 – Example Inclusion of a Schematron Pattern Element in an XSD
Similar assertions may be used to constrain the use of values from code list resources for individual domain-specific data types, e.g., the set of allowed values of UoM for a measure.
ISO 19136:2007 (GML) employs Schematron assertions for a variety of purposes.
The TSPI Schema employs Schematron assertions to declare XML element constraints and co-constraints that cannot be expressed using XML Schema.
It is a recommended practice that users of the TSPI Schema employ Schematron assertions in order to more fully document the complete syntactic rule set for their schemas. This level of increased rigor allows for enhanced automated instance document validation as well as providing more detailed guidance to data providers and consumers as to the allowed range of instance documents that they may be allowed to generate, or required to consume, respectively.
Annex B– Test Suite
(Normative)
B.1	Introduction
Conformance with the TSPI Schema shall be determined based on the tests specified in this Annex. These tests are accomplished through the use of a validating XML processor and a Schematron validator. In general, these tests are used to determine if an XML instance document is both well-formed (meets syntactic requirements) and valid (meets logical requirements) with respect to the requirements of the TSPI Schema, and in the case of an TSPI Schema-conformant application whether it correctly writes and/or reads TSPI Schema-conformant instance documents.
B.2	Validating XML Processor
XML Schema 1.0 (Second Edition) describes a class of data objects called “XML documents” and partially describes the behavior of computer programs which process them.
XML documents are made up of storage units called “entities”, which contain either parsed or unparsed data. Parsed data is made up of characters, some of which form character data, and some of which form markup. Markup encodes a description of the document's storage layout and logical structure. XML provides a mechanism to impose constraints on the storage layout and logical structure.
An XML schema is used to describe the structure of an XML document by specifying the valid elements that can occur in a document, the order in which they can occur, and expressing constraints on certain aspects of these elements. These constraints may be as simple as “The Name in an element's end-tag MUST match the element type in the start-tag.” and “An element type MUST NOT be declared more than once.”, however many are more complex.
An XML schema is intended as a machine-readable mechanism to describe what constitutes a valid XML document according to a particular XML vocabulary. A schema defines what constraints an XML document producer commits to meeting and what expectations an XML document consumer must meet in order to ensure that the transmission of that document from producer to consumer results in a complete and faithful data exchange. Typically, the consumer ensures that the XML document being received from the producer conforms to that producer commitment by validating the received document against its specified XML Schema document (XSD).
Usually a general-purpose XML processor is used to read XML documents, providing access to their content and structure; this is typically accomplished on behalf of a specialized application. XML Schema 1.0 (Second Edition) describes the required behavior of that XML processor in terms of how it must read XML data and the information that it must provide to that specialized application. Usually a “validating” XML processor is employed – which is required to examine every component of the XML document and report all well-formedness and validity violations.
B.3	Schematron Validator
ISO/IEC 19757-3:2006 defines the Schematron Document Schema Definition Language (DSDL) that may be used to specify one or more validation processes to be performed against XML instance documents. Schematron is a rule-based validation language for making assertions (see Annex A.6) about the presence or absence of patterns in XML trees. It is a simple and powerful structural schema language expressed in XML using a small number of elements and XPath (a query language for selecting nodes from an XML document). It may be employed as an adjunct to the structural validation capabilities of XSD – testing for co-occurrence constraints, non-regular constraints, and inter-document constraints.
Schematron is a language system for specifying and declaring assertions about arbitrary patterns in XML documents, based on the presence or absence, names and values of elements and attributes along paths. It uses the languages of XML Path Language (XPath) Version 1.0 and XSL Transformations (XSLT) Version 1.0.
Considered as a document type, a Schematron schema (.sch file) contains natural-language assertions concerning a set of XML documents, marked up with various elements and attributes for testing these natural-language assertions, and for simplifying and grouping assertions.
Considered theoretically, a Schematron schema reduces to a non-chaining rule system whose terms are Boolean functions invoking an external query language on the instance and other visible XML documents, with syntactic features to reduce specification size and to allow efficient implementation.
Considered analytically, Schematron has two characteristic high-level abstractions: the pattern and the phase. These allow the representation of non-regular, non-sequential constraints that ISO/IEC 19757-2:2003 (Document Schema Definition Languages (DSDL) – Part 2: Regular grammar-based validation – RELAX NG) cannot specify, and various dynamic or contingent constraints.
A general Schematron validator is a function returning an indication that an XML document is "valid", "invalid" or "error". The function notionally performs two steps: transforming the specified Schematron schema into a minimal syntax , and then testing the XML document against the minimal syntax. It is common to implement Schematron validators directly using XSLT.
ISO/IEC 19757-3:2006, Annex C Default Query Language Binding specifies that:
A Schematron schema with no language binding or a queryBinding attribute with the value xslt, in any mix of upper and lower case letters, shall use the following binding:
•	The query language used is the extended version of XPath specified in XSLT. Consequently, the data model used is the data model of those specifications.
•	The rule context is interpreted according to the Production 1 of XSLT. The rule context may be the root node, elements, attributes, comments and processing instructions.
•	The assertion test is interpreted according to Production 14 of XPath, as returning a Boolean value.
•	The name query is interpreted according to Production 14 of XPath, as returning a string value. Typically, the select attribute contains an expression returning an element node: the name query takes the local or prefixed name of the node, not its value.
•	The value-of query is interpreted according to Production 14 of XPath, as returning a string value.
•	The let value is interpreted according to Production 14 of XPath, as returning a string value.
•	The notation for signifying the use of parameter of an abstract pattern is to prefix the name token with the ‘$’ character. This is a character not found as a delimiter in URLs or XPaths. The ‘$’ character not followed by the name of an in-scope parameter shall not be treated as a parameter name delimiter. Such a character may subsequently be used as a delimiter for a variable name or as a literal character.
•	A Schematron let expression is treated as an XSLT variable. The XSLT ‘$’ delimiter signifies the use of a variable in a context expression, assertion test, name query, value-of query or let expression. The ‘$’ character not followed by the name of an in-scope variable shall be treated as a literal character.
The XSLT key element may be used, in the XSLT namespace, before the pattern elements.
The attributes id, name and prefix should follow the rules for non-colonized names for the version of XML used by the document.
While the ISO/IEC 19757-3:2006 Default Query Language Binding uses XSLT 1.0, other Query Language Bindings may be employed.
Schematron validators used in testing TSPI Schema conformance shall use the default Query Language Binding of XSLT 1.0.
In the future it may be the case that XSL Transformations (XSLT) Version 2.0 (http://www.w3.org/TR/xslt20/) may be allowed for use in testing TSPI Schema conformance, based on the publication of ISO/IEC 19757-3 Second Edition. 
B.4	Conformance
B.4.1	Introduction
This TSPI standard specifies the following  XML namespaces:
•	‘tspi-core’: Specifies core XML type components that shall always be used as specified without further restriction unless documented by, and accomplished using, Schematron assertions.
•	‘tspi-ext’: TSPI-conformant registered extensions that specify additional representations for spatial position, geographic location, and/or physical address. It is populated with initial high-value extensions, but is dynamically maintained on the MDR. Its use is conditional on the requirements of a given system/application and its accompanying business requirements.
•	 ‘tspi’: XML elements and non-core types with less strict reuse rules than ‘tspi-core’; it imports the schemas of the ‘tspi-core’and ‘tspi-ext’ namespaces.
When any of these three XML namespaces are referenced from other schemas then the single valid schemaLocation for the <import> is that established in the MDR.  For the current TSPI release these are, respectively:
•	‘tspi-core’: http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0.0/tspi-core.xsd
•	‘tspi-ext’: http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0.0/tspi-ext.xsd
•	‘tspi’: http://metadata.ces.mil/mdr/ns/GSIP/tspi/2.0.0/tspi.xsd 
Schema component files (XSD, SCH, XML) may be copied to other locations for development and/or efficiency purposes, however any alteration or substitution violates TSPI conformance requirements (see Annex B).
These namespaces are  implemented in terms of a set of data-file components that are of one of the following three types:
•	XML Schema documents (XSD): These specify authoritative XML Schema components that are either:
o	imported from other XML namespaces, or 
o	define the TSPI XML namespaces (‘tspi-core’, ‘tspi-ext’, and ‘tspi’).
•	ISO/IEC 19757:2006 Schematron (SCH) documents: These specify authoritative constraints applied to XML Schema components that are either:
o	imported from other XML namespaces, or
o	define the TSPI XML namespaces (‘tspi-core’, ‘tspi-ext’, and ‘tspi’).
•	XML instance documents: These either specify:
o	authoritative GML-based CodeList Dictionaries that are used by various XML Schema components and associated Schematron assertions, or
o	informative examples of the use of TSPI Schema components in XML-based information exchange.
Schema component files (XSD, SCH, XML) may be copied from the MDR to other locations for development and/or efficiency purposes, however any alteration or substitution violates TSPI conformance requirements.
In order to support such “expedient alternatives” the TSPI Schema is distributed with an accompanying XML Catalog (OASIS XML Catalogs, Committee Specification 06 Aug 2001) that is configured to redirect references to MDR-associated resources to local folders. In a typical environment, those redirects would appear as follows:
<rewriteSystem
   systemIdStartString="http://metadata.ces.mil/mdr/ns/GPAS/schemas/fgdc/" 
   rewritePrefix="./fgdc/"/>
<rewriteSystem
   systemIdStartString="http://metadata.ces.mil/mdr/ns/GPAS/schemas/iso/" 
   rewritePrefix="./iso/"/>
<rewriteSystem
   systemIdStartString="http://metadata.ces.mil/mdr/ns/GPAS/schemas/ogc/" 
   rewritePrefix="./ogc/"/>
<rewriteSystem
   systemIdStartString="http://metadata.ces.mil/mdr/ns/GPAS/schemas/w3c/" 
   rewritePrefix="./w3c/"/>
<rewriteSystem
   systemIdStartString="http://metadata.ces.mil/mdr/ns/GSIP/tspi/"
   rewritePrefix="./tspi/"/>
B.4.2	Schema Subsetting
While schema component files (XSD, SCH, XML; see Annex B.4.1) may be copied from the DoD Data Services Environment (DSE) Metadata Registry (MDR) to other locations for temporary development and/or efficiency purposes, any alteration or substitution (e.g., by the preparation of “subset schemas”) violates TSPI conformance requirements. These requirements are necessitated by the potential consequences to the distributed enterprise of differing local policies regarding how schema definitions are located on the Web.
XML Schema Part 1: Structures, Second Edition, Sections 4.3.1 (Standards for representation of schemas and retrieval of schema documents on the Web ) and 4.3.2 (How schema definitions are located on the Web) include the following language (see: http://www.w3.org/TR/xmlschema-1/#schema-loc):
For interoperability, serialized •schema documents•, like all other Web resources, may be identified by URI and retrieved using the standard mechanisms of the Web (e.g. http, https, etc.) Such documents on the Web must be part of XML documents (see clause 1.1), and are represented in the standard XML schema definition form described by layer 2 (that is as <schema> element information items).
…
As described in Layer 1: Summary of the Schema-validity Assessment Core (§4.1), processors are responsible for providing the schema components (definitions and declarations) needed for •assessment•. This section introduces a set of normative conventions to facilitate interoperability for instance and schema documents retrieved and processed from the Web.
…
Schema Representation Constraint: Schema Document Location Strategy
Given a namespace name (or none) and (optionally) a URI reference from xsi:schemaLocation or xsi:noNamespaceSchemaLocation, schema-aware processors may implement any combination of the following strategies, in any order: 
    1 Do nothing, for instance because a schema containing components for the given namespace name is already known to be available, or because it is known in advance that no efforts to locate schema documents will be successful (for example in embedded systems); 
    2 Based on the location URI, identify an existing schema document, either as a resource which is an XML document or a <schema> element information item, in some local schema repository; 
    3 Based on the namespace name, identify an existing schema document, either as a resource which is an XML document or a <schema> element information item, in some local schema repository; 
    4 Attempt to resolve the location URI, to locate a resource on the web which is or contains or references a <schema> element; 
    5 Attempt to resolve the namespace name to locate such a resource. 
Whenever possible configuration and/or invocation options for selecting and/or ordering the implemented strategies should be provided. 

In accordance with the W3C recommendation, conformance with the TSPI Schema includes the requirement to follow Strategy #4 to locate and employ the MDR-hosted information resources defined by the xsi:schemaLocation attribute in all files comprising the TSPI Schema.
This requirement is necessitated to ensure that all enterprise participants/applications are employing a correct, complete component file-set for the TSPI and not inadvertently depending on caches (whether filesystem-based, memory-resident, or software-embedded) that may be stale and thus incorrect/incomplete.
B.4.3	Instance Document
TSPI Schema conformance of an XML instance document requires that the following set of conditions be met; in general these tests will be applied in the sequence specified.
1.	The XML instance document, when evaluated against tspi.xsd and the specified MDR-based imported schema resources using a validating XML processor, shall be determined to be well-formed in accordance with the XML Schema 1.0 (Second Edition) standard.
2.	The XML instance document, when evaluated against tspi.xsd and the specified MDR-based imported schema resources using a validating XML processor, shall be determined to be valid in accordance with the XML Schema 1.0 (Second Edition) standard.
B.4.4	Document Generation
All XML instance documents generated by the system under test that are intended to be TSPI Schema-conformant shall satisfy the set of conditions specified in Annex B.4.3.
B.4.5	Document Consumption
The system under test shall demonstrate that it successfully and “meaningfully” extracts all component values of any XML instance document that has been demonstrated to be TSPI Schema-conformant, as determined by the set of conditions specified in Annex B.4.3.
Annex C – Geodetic Datums
(Informative)
C.1	Coordinate Reference System Ambiguity
Spatial positions are effectively meaningless without an unambiguous specification of their Coordinate Reference System (CRS). As stated in Section 5.3.1.2, CRS are defined by the combination of one coordinate system with one datum.
In many DoD/IC systems and exchange format (e.g.,  USMTF) the coordinate system is implied by the naming of fields or other context-sensitive information external to the system or exchange format (e.g., in development documentation).
Given a lack of explicit specification of the (geodetic) datum when spatial position information is exchanged , in most cases (and perhaps all cases of recent-vintage systems)  it is assumed that the WGS 84 geodetic datum should be “understood” as being intended. This is not a “fail safe” unambiguous solution and this practice is not followed in this TSPI specification. In particular, there exist many printed maps/charts whose projection and/or printed grid may be based on a legacy datum. Inadvertant transcription of spatial positions to or from such maps/charts will result in errors.
In the TSPI Schema all representations of spatial position shall include an unambiguous specification of their CRS, usually by reference.
C.2	CRS Referencing
WGS 84 is a global reference system for identifying locations on the Earth and is defined in NIMA TR8350.2 Department of Defense World Geodetic System 1984 - Its Definition and Relationships with Local Geodetic Systems, 3rd Edition, Amendment 2. In addition to WGS 84, there are also many localized “Earth reference systems” that specify a different, usually geographically localized, geodetic datum.
It is a recommended practice (see Section  5.3.2.2) that when a Geodetic 2D CRS is used that it be in accordance with World Geodetic System 1984 - Geographic, 2-Dimensional, as specified in NIMA TR8350.2 (3rd Edition, Amendment 2) and identified by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
Instance documents conforming to the TSPI Schema may specify an alternative Geodetic 2D CRS if that CRS has been registered in the GSIP Governance Namespace in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
C.3	Registered CRS
Each registered CRS (see Section 5.3.1.6) is identified by a URI composed from a base URL:
http://metadata.ces.mil/mdr/ns/GSIP/crs/
To this is concatenated a short CRS-specific identifier. In the case of the World Geodetic System 1984 - Geographic, 2-Dimensional CRS, the resulting identification is by the URI:
http://metadata.ces.mil/mdr/ns/GSIP/crs/WGS84E_2D
Each such URI has a corresponding CRS-specific accessible information resource in the MDR that is realized as an XML instance document using XML elements and types specified in ISO 19136:2007 (GML) Clause 12.3 Coordinate reference systems.
C.4	Alternate and Legacy Datums
USMTF defines the domain values for the GEODETIC DATUM field as specified in Table 14. In this specification, for clarity the allowed domain values have been sorted into two groups:
•	domain values (consisting of 3- to 5- character codes) denoting geodetic datums, and then
•	domain values (consisting of 2-character codes) denoting ellipsoids. 
The geodetic datums (first group of domain values) may be divided into those whose relationship to WGS 84 has been specified, and those that are “unrelated” (identified in red-font). NIMA TR8350.2 (3rd Edition, Amendment 2) indicates that the latter set of codes are intended only for the purpose of grouping related geodetic datums (those sharing a common ellipsoid and related geographic extents) and not for the purpose of establishing a unique geodetic datum. Their inclusion in the USMTF GEODETIC DATUM field is not appropriate.
The ellipsoids (second group of domain values) are included inappropriately because they merely indicate an ellipsoid – which may be used to specify a component of a geodetic datum specification, but is not itself a geodetic datum.
It is the continuing existence of these types of anomalies (“datum” codes that do not designate valid datums) in DoD/IC systems and data exchange formats that the conformant employment of the TSPI Schema will eliminate.
The remaining domain values may be used to establish a Geodetic 2D CRS that is “tied” to WGS 84 and thus spatial positions specified in terms of those CRS may be transformed into corresponding spatial positions in terms of a WGS 84 Geodetic 2D CRS. 
Table 14 – USMTF GEODETIC DATUM Domain Values
CODE	EXPLANATION	CRS IDENTIFIER
ADI	ADINDAN	
ADI-A	ADINDAN - ETHIOPIA	ADIA_2D
ADI-B	ADINDAN - SUDAN	ADIB_2D
ADI-C	ADINDAN - MALI	ADIC_2D
ADI-D	ADINDAN - SENEGAL	ADID_2D
ADI-E	ADINDAN - BURKINA FASO	ADIE_2D
ADI-F	ADINDAN - CAMEROON	ADIF_2D
ADI-M	ADINDAN - MEAN SOLUTION (ETHIOPIA AND SUDAN)	ADIM_2D
AFG	AFGOOYE - SOMALIA	AFG_2D
AIA	ANTIGUA ISLAND ASTRO 1943 - ANTIGUA AND LEEWARD ISLANDS	AIA_2D
AIN	AIN EL ABD 1970	
AIN-A	AIN EL ABD 1970 - BAHRAIN ISLAND	AINA_2D
AIN-B	AIN EL ABD 1970 - SAUDI ARABIA	AINB_2D
AMA	AMERICAN SAMOA 1962 - AMERICAN SAMOA ISLANDS	AMA_2D
ANO	ANNA 1 ASTRO 1965 - COCOS ISLANDS	ANO_2D
ARF	ARC 1950	
ARF-A	ARC 1950 - BOTSWANA	ARFA_2D
ARF-B	ARC 1950 - LESOTHO	ARFB_2D
ARF-C	ARC 1950 - MALAWI	ARFC_2D
ARF-D	ARC 1950 - SWAZILAND	ARFD_2D
ARF-E	ARC 1950 - ZAIRE	ARFE_2D
ARF-F	ARC 1950 - ZAMBIA	ARFF_2D
ARF-G	ARC 1950 - ZIMBABWE	ARFG_2D
ARF-H	ARC 1950 - BURUNDI	ARFH_2D
ARF-M	ARC 1950 – MEAN SOLUTION (BOTSWANA, LESOTHO, MALAWI, SWAZILAND, ZAIRE, ZAMBIA, ZIMBABWE)	ARFM_2D
ARS	ARC 1960	
ARS-A	ARC 1960 - KENYA	ARSA_2D
ARS-B	ARC 1960 - TANZANIA	ARSB_2D
ARS-M	ARC 1960 – MEAN SOLUTION (KENYA AND TANZANIA)	ARSM_2D
ASC	ASCENSION ISLAND 1958 - ASCENSION ISLAND	ASC_2D
ASM	MONTSERRAT ISLAND ASTRO 1958 – LEEWARD AND MONTSERRAT ISLANDS	ASM_2D
ASQ	ASTRONOMICAL STATION 1952 - MARCUS ISLAND	ASQ_2D
ATF	ASTRO BEACON E 1945 - IWO JIMA	ATF_2D
AUA	AUSTRALIAN GEODETIC 1966 - AUSTRALIA AND TASMANIA	AUA_2D
AUG	AUSTRALIAN GEODETIC 1984 - AUSTRALIA AND TASMANIA	AUG_2D
BAT	DJAKARTA (BATAVIA) SUMATRA (INDONESIA)	BAT_2D
BER	BERMUDA 1957 – BERMUDA ISLANDS	BER_2D
BID	BISSAU - GUINEA-BISSAU	BID_2D
BOO	BOGOTA OBSERVATORY - COLOMBIA	BOO_2D
BUR	BUKIT RIMPAH - BANGKA AND BELITUNG ISLANDS (INDONESIA)	BUR_2D
CAC	CAPE CANAVERAL – MEAN SOLUTION (FLORIDA AND BAHAMAS)	CAC_2D
CAI	CAMPO INCHAUSPE 1969 - ARGENTINA	CAI_2D
CAO	CANTON ASTRO 1966 - PHOENIX ISLANDS	CAO_2D
CAP	CAPE - SOUTH AFRICA	CAP_2D
CAZ	CAMP AREA ASTRO - CAMP MCMURDO AREA, ANTARCTICA	CAZ_2D
CCD	S-JTSK – CZECHOSLOVAKIA (PRIOR 1 JAN 1993)	CCD_2D
CGE	CARTHAGE - TUNISIA	CGE_2D
CHI	CHATHAM ISLAND ASTRO 1971 - CHATHAM ISLAND (NEW ZEALAND)	CHI_2D
CHU	CHUA ASTRO - PARAGUAY	CHU_2D
COA	CORREGO ALEGRE - BRAZIL	COA_2D
DAL	DABOLA - GUINEA	DAL_2D
DID	DECEPTION ISLAND - DECEPTION ISLAND AND ANTARCTICA	DID_2D
DOB	GUX I ASTRO - GUADALCANAL ISLAND	DOB_2D
EAS	EASTER ISLAND 1967 - EASTER ISLAND	EAS_2D
ENW	WAKE-ENIWETOK 1960 - MARSHALL ISLANDS	ENW_2D
EST	CO-ORDINATE SYSTEM 1937 OF ESTONIA - ESTONIA	EST_2D
EUR	EUROPEAN 1950	
EUR-A	EUROPEAN 1950 - (WESTERN EUROPE (LIMITED TO AUSTRIA, DENMARK, FRANCE, FEDERAL REPUBLIC OF GERMANY (FRG) (PRIOR 1 JAN 1993), NETHERLANDS, AND SWITZERLAND)	EURA_2D
EUR-B	EUROPEAN 1950 - GREECE	EURB_2D
EUR-C	EUROPEAN 1950 - NORWAY AND FINLAND	EURC_2D
EUR-D	EUROPEAN 1950 - PORTUGAL AND SPAIN	EURD_2D
EUR-E	EUROPEAN 1950 - CYPRUS	EURE_2D
EUR-F	EUROPEAN 1950 - EGYPT	EURF_2D
EUR-G	EUROPEAN 1950 - ENGLAND, CHANNEL ISLANDS, SCOTLAND, AND SHETLAND ISLANDS	EURG_2D
EUR-H	EUROPEAN 1950 - IRAN	EURH_2D
EUR-I	EUROPEAN 1950 - ITALY (SARDINIA)	EURI_2D
EUR-J	EUROPEAN 1950 - ITALY (SICILY)	EURJ_2D
EUR-K	EUROPEAN 1950 - ENGLAND, IRELAND, SCOTLAND, AND SHETLAND ISLANDS	EURK_2D
EUR-L	EUROPEAN 1950 - MALTA	EURL_2D
EUR-M	EUROPEAN 1950 – MEAN SOLUTION (AUSTRIA, BELGIUM, DENMARK, FINLAND, FRANCE, FEDERAL REPUBLIC OF GERMANY (PRIOR 1 JAN 1993), GIBRALTAR, GREECE, ITALY, LUXEMBOURG, NETHERLANDS, NORWAY, PORTUGAL, SPAIN, SWEDEN, AND SWITZERLAND)	EURM_2D
EUR-S	EUROPEAN 1950 - IRAQ, ISRAEL, JORDAN, KUWAIT, LEBANON, SAUDI ARABIA, AND SYRIA	EURS_2D
EUR-T	EUROPEAN 1950 - TUNISIA	EURT_2D
EUS	EUROPEAN 1979 – MEAN SOLUTION (AUSTRIA, FINLAND, NETHERLANDS, NORWAY, SPAIN, SWEDEN, AND SWITZERLAND)	EUS_2D
FAH	OMAN - OMAN	FAH_2D
FLO	OBSERVATORIO METEOROLOGICO 1939 - CORVO AND FLORES ISLAND (AZORES)	FLO_2D
FOT	FORT THOMAS 1955 – LEEWARD ISLANDS (NEVIS AND ST. KITTS)	FOT_2D
GAA	GAN 1970 - REPUBLIC OF MALDIVES	GAA_2D
GEO	GEODETIC DATUM 1949 - NEW ZEALAND	GEO_2D
GIZ	DOS 1968 - GIZO ISLAND (NEW GEORGIA ISLANDS)	GIZ_2D
GRA	GRACIOSA BASE SW 1948 - FAIAL, GRACIOSA, PICO, SAO JORGE AND TERCEIRA ISLANDS (AZORES)	GRA_2D
GSE	GUNUNG SEGARA - KALIMANTAN (INDONESIA)	GSE_2D
GUA	GUAM 1963 - GUAM	GUA_2D
HEN	HERAT NORTH - AFGHANISTAN	HEN_2D
HER	HERMANNSKOGEL – YUGOSLAVIA (PRIOR 1 JAN 1990), SLOVENIA, CROATIA, BOSNIA AND HERZEGOVINA, SERBIA	HER_2D
HIT	PROVISIONAL SOUTH CHILEAN 1963 (A.K.A. HITO XVIII 1963) - SOUTHERN CHILE (NEAR 53 DEGREES SOUTH)	HIT_2D
HJO	HJORSEY 1955 - ICELAND	HJO_2D
HKD	HONG KONG 1963 – HONG KONG	HKD_2D
HTN	HU-TZU-SHAN - TAIWAN	HTN_2D
IBE	BELLEVUE (IGN) - EFATE AND ERROMANGO ISLANDS	IBE_2D
IDN	INDONESIAN 1974 - INDONESIA	IDN_2D
IND	INDIAN	
IND-B	INDIAN - BANGLADESH	INDB_2D
IND-I	INDIAN - INDIA AND NEPAL	INDI_2D
IND-P	INDIAN - PAKISTAN	INDP_2D
INF	INDIAN 1954	
INF-A	INDIAN 1954 - THAILAND	INFA_2D
ING	INDIAN 1960	
ING-A	INDIAN 1960 - VIETNAM (NEAR 16 DEGREES NORTH)	INGA_2D
ING-B	INDIAN 1960 - CON SON ISLAND (VIETNAM)	INGB_2D
INH	INDIAN 1975	
INH-A	INDIAN 1975 - THAILAND	INHA_2D
INH-A1	INDIAN 1975 - THAILAND (ALTERNATE)	INHA1_2D
IRL	IRELAND 1965 - IRELAND	IRL_2D
ISG	ISTS 061 ASTRO 1968 - SOUTH GEORGIA ISLAND	ISG_2D
IST	ISTS 073 ASTRO 1969 - DIEGO GARCIA	IST_2D
JOH	JOHNSTON ISLAND 1961 – JOHNSTON ISLAND	JOH_2D
KAN	KANDAWALA - SRI LANKA	KAN_2D
KEA	KERTAU 1948 - WEST MALAYSIA AND SINGAPORE	KEA_2D
KEG	KERGUELEN ISLAND 1949 - KERGUELEN ISLAND	KEG_2D
KGS	KOREAN GEODETIC SYSTEM 1995 - SOUTH KOREA	KGS_2D
KUS	KUSAIE ASTRO 1951 - CAROLINE ISLANDS, FED. STATES OF MICRONESIA	KUS_2D
LCF	L.C. 5 ASTRO 1961 - CAYMAN BRAC ISLAND	LCF_2D
LEH	LEIGON - GHANA	LEH_2D
LIB	LIBERIA 1964 - LIBERIA	LIB_2D
LUZ	LUZON	
LUZ-A	LUZON - PHILIPPINES (EXCLUDING MINDANAO ISLAND)	LUZA_2D
LUZ-B	LUZON - MINDANAO ISLAND	LUZB_2D
MAS	MASSAWA - ERITREA (ETHIOPIA)	MAS_2D
MER	MERCHICH - MOROCCO	MER_2D
MID	MIDWAY ASTRO 1961 - MIDWAY ISLAND	MID_2D
MIK	MAHE 1971 – MAHE ISLAND	MIK_2D
MIN	MINNA	
MIN-A	MINNA - CAMEROON	MINA_2D
MIN-B	MINNA - NIGERIA	MINB_2D
MOD	ROME 1940 – SARDINIA, ITALY	MOD_2D
MPO	M'PORALOKO - GABON	MPO_2D
MVS	VITI LEVU 1916 - VITA LEVU ISLAND (FIJI ISLANDS)	MVS_2D
NAH	NAHRWAN	
NAH-A	NAHRWAN - MASIRAH ISLAND (OMAN)	NAHA_2D
NAH-B	NAHWRAN - UNITED ARAB EMIRATES	NAHB_2D
NAH-C	NAHRWAN - SAUDI ARABIA	NAHC_2D
NAP	NAPARIMA, BWI - TRINIDAD AND TOBAGO	NAP_2D
NAR	NORTH AMERICAN 1983	
NAR-A	NORTH AMERICAN 1983 - ALASKA (EXCLUDING ALEUTIAN ISLANDS)	NARA_2D
NAR-B	NORTH AMERICAN 1983 - CANADA	NARB_2D
NAR-C	NORTH AMERICAN 1983 - CONUS	NARC_2D
NAR-D	NORTH AMERICAN 1983 - MEXICO AND CENTRAL AMERICA	NARD_2D
NAR-E	NORTH AMERICAN 1983 - ALEUTIAN ISLANDS	NARE_2D
NAR-H	NORTH AMERICAN 1983 - HAWAII	NARH_2D
NAS	NORTH AMERICAN 1927	
NAS-A	NORTH AMERICAN 1927 - EASTERN UNITED STATES (ALABAMA, CONNECTICUT, DELAWARE, DISTRICT OF COLUMBIA, FLORIDA, GEORGIA, ILLINOIS, INDIANA, KENTUCKY, LOUISIANA, MAINE, MARYLAND, MASSACHUSETTS, MICHIGAN, MINNESOTA, MISSISSIPPI, MISSOURI, NEW HAMPSHIRE, NEW JERSEY, NEW YORK, NORTH CAROLINA, OHIO, PENNSYLVANIA, RHODE ISLAND, SOUTH CAROLINA, TENNESSEE, VERMONT, VIRGINIA, WEST VIRGINIA AND WISCONSIN)	NASA_2D
NAS-B	NORTH AMERICAN 1927 - WESTERN UNITED STATES (ARIZONA, ARKANSAS, CALIFORNIA, COLORADO, IDAHO, IOWA, KANSAS, MONTANA, NEBRASKA, NEVADA, NEW MEXICO, NORTH DAKOTA, OKLAHOMA, OREGON, SOUTH DAKOTA, TEXAS, UTAH, WASHINGTON AND WYOMING)	NASB_2D
NAS-C	NORTH AMERICAN 1927 - MEAN SOLUTION (CONUS)	NASC_2D
NAS-D	NORTH AMERICAN 1927 - ALASKA (EXCLUDING ALEUTIAN ISLANDS)	NASD_2D
NAS-E	NORTH AMERICAN 1927 - CANADA MEAN SOLUTION (INCLUDING NEWFOUNDLAND)	NASE_2D
NAS-F	NORTH AMERICAN 1927 - ALBERTA AND BRITISH COLUMBIA	NASF_2D
NAS-G	NORTH AMERICAN 1927 - EASTERN CANADA (NEWFOUNDLAND, NEW BRUNSWICK, NOVA SCOTIA, AND QUEBEC)	NASG_2D
NAS-H	NORTH AMERICAN 1927 - MANITOBA AND ONTARIO	NASH_2D
NAS-I	NORTH AMERICAN 1927 - NORTHWEST TERRITORIES AND SASKATCHEWAN	NASI_2D
NAS-J	NORTH AMERICAN 1927 - YUKON	NASJ_2D
NAS-L	NORTH AMERICAN 1927 - MEXICO	NASL_2D
NAS-N	NORTH AMERICAN 1927 - CENTRAL AMERICA (BELIZE, COSTA RICA, EL SALVADOR, GUATEMALA, HONDURAS, AND NICARAGUA)	NASN_2D
NAS-O	NORTH AMERICAN 1927 - CANAL ZONE	NASO_2D
NAS-P	NORTH AMERICAN 1927 - CARIBBEAN (ANTIGUA ISLAND, BARBADOS, BARBUDA, CAICOS ISLAND, CUBA, DOMINICAN REPUBLIC, GRAND CAYMAN, JAMAICA, AND TURKS ISLANDS)	NASP_2D
NAS-Q	NORTH AMERICAN 1927 - BAHAMAS (EXCLUDING SAN SALVADOR ISLAND)	NASQ_2D
NAS-R	NORTH AMERICAN 1927 - SAN SALVADOR ISLAND	NASR_2D
NAS-T	NORTH AMERICAN 1927 - CUBA	NAST_2D
NAS-U	NORTH AMERICAN 1927 - GREENLAND (HAYES PENINSULA)	NASU_2D
NAS-V	NORTH AMERICAN 1927 - ALEUTIAN ISLANDS (EAST OF 180W)	NASV_2D
NAS-W	NORTH AMERICAN 1927 - ALEUTIAN ISLANDS (WEST OF 180W)	NASW_2D
NSD	NORTH SAHARA 1959 - ALGERIA	NSD_2D
OEG	OLD EGYPTIAN 1907 - EGYPT	OEG_2D
OGB	ORDNANCE SURVEY OF GREAT BRITAIN 1936	
OGB-A	ORDNANCE SURVEY OF GREAT BRITAIN 1936 - ENGLAND	OGBA_2D
OGB-B	ORDNANCE SURVEY OF GREAT BRITAIN 1936 - ENGLAND, ISLE OF MAN, AND WALES	OGBB_2D
OGB-C	ORDNANCE SURVEY OF GREAT BRITAIN 1936 - SCOTLAND AND SHETLAND ISLANDS	OGBC_2D
OGB-D	ORDNANCE SURVEY OF GREAT BRITAIN 1936 - WALES	OGBD_2D
OGB-M	ORDNANCE SURVEY OF GREAT BRITAIN 1936 – MEAN SOLUTION (ENGLAND, ISLE OF MAN, SCOTLAND, SHETLAND ISLANDS, AND WALES)	OGBM_2D
OHA	OLD HAWAIIAN	
OHA-A	OLD HAWAIIAN - HAWAII	OHAA_2D
OHA-B	OLD HAWAIIAN - KAUAI	OHAB_2D
OHA-C	OLD HAWAIIAN - MAUI	OHAC_2D
OHA-D	OLD HAWAIIAN - OAHU	OHAD_2D
OHA-M	OLD HAWAIIAN - MEAN SOLUTION	OHAM_2D
OHI-A	OLD HAWAII - HAWAII	OHIA_2D
OHI-B	OLD HAWAII - KAUAI	OHIB_2D
OHI-C	OLD HAWAII - MAUI	OHIC_2D
OHI-D	OLD HAWAII - OAHU	OHID_2D
OHI-M	OLD HAWAII - MEAN SOLUTION	OHIM_2D
PHA	AYABELLE LIGHTHOUSE - DJIBOUTI	PHA_2D
PIT	PITCAIRN ASTRO 1967 - PITCAIRN ISLAND	PIT_2D
PLN	PICO DE LAS NIEVES - CANARY ISLANDS	PLN_2D
POS	PORTO SANTO 1936 - PORTO SANTO AND MADEIRA ISLANDS	POS_2D
PRP	PROVISIONAL SOUTH AMERICAN 1956	
PRP-A	PROVISIONAL SOUTH AMERICAN 1956 - BOLIVIA	PRPA_2D
PRP-B	PROVISIONAL SOUTH AMERICAN 1956 - CHILE (NORTHERN CHILE (NEAR 19 DEGREES SOUTH))	PRPB_2D
PRP-C	PROVISIONAL SOUTH AMERICAN 1956 - (SOUTHERN CHILE (NEAR 43 DEGREES SOUTH))	PRPC_2D
PRP-D	PROVISIONAL SOUTH AMERICAN 1956 - COLUMBIA	PRPD_2D
PRP-E	PROVISIONAL SOUTH AMERICAN 1956 - ECUADOR	PRPE_2D
PRP-F	PROVISIONAL SOUTH AMERICAN 1956 - GUYANA	PRPF_2D
PRP-G	PROVISIONAL SOUTH AMERICAN 1956 - PERU	PRPG_2D
PRP-H	PROVISIONAL SOUTH AMERICAN 1956 - VENEZUELA	PRPH_2D
PRP-M	PROVISIONAL SOUTH AMERICAN 1956 – MEAN SOLUTION (BOLIVIA, CHILE, COLOMBIA, ECUADOR, GUYANA, PERU, AND VENEZUELA)	PRPM_2D
PTB	POINT 58 – MEAN SOLUTION (BURKINA FASO AND NIGER)	PTB_2D
PTN	POINTE NOIRE 1948 - CONGO	PTN_2D
PUK	PULKOVO 1942 (S42) - RUSSIA	PUK_2D
PUR	PUERTO RICO - PUERTO RICO AND VIRGIN ISLANDS	PUR_2D
QAT	QATAR NATIONAL - QATAR	QAT_2D
QUO	QORNOQ - SOUTH GREENLAND	QUO_2D
REU	REUNION - MASCARENE ISLANDS	REU_2D
SAE	SANTO (DOS) 1965 - ESPIRITO SANTO ISLAND	SAE_2D
SAN	SOUTH AMERICAN 1969	
SAN-A	SOUTH AMERICAN 1969 ARGENTINA	SANA_2D
SAN-B	SOUTH AMERICAN 1969 - BOLIVIA	SANB_2D
SAN-C	SOUTH AMERICAN 1969 - BRAZIL	SANC_2D
SAN-D	SOUTH AMERICAN 1969 - CHILE	SAND_2D
SAN-E	SOUTH AMERICAN 1969 - COLOMBIA	SANE_2D
SAN-F	SOUTH AMERICAN 1969 - ECUADOR (EXCLUDING GALAPAGOS ISLANDS)	SANF_2D
SAN-G	SOUTH AMERICAN 1969 - GUYANA	SANG_2D
SAN-H	SOUTH AMERICAN 1969 - PARAGUAY	SANH_2D
SAN-I	SOUTH AMERICAN 1969 - PERU	SANI_2D
SAN-J	SOUTH AMERICAN 1969 - BALTRA, GALAPAGOS ISLANDS	SANJ_2D
SAN-K	SOUTH AMERICAN 1969 - TRINIDAD AND TOBAGO	SANK_2D
SAN-L	SOUTH AMERICAN 1969 - VENEZUELA	SANL_2D
SAN-M	SOUTH AMERICAN 1969 – MEAN SOLUTION (ARGENTINA, BOLIVIA, BRAZIL, CHILE, COLOMBIA, ECUADOR, GUYANA, PARAGUAY, PERU, TRINIDAD, TOBAGO, AND VENEZUELA)	SANM_2D
SAO	SAO BRAZ - SAO MIGUEL, SANTA MARIA ISLANDS (AZORES)	SAO_2D
SAP	SAPPER HILL 1943 - EAST FALKLAND ISLAND	SAP_2D
SCK	SCHWARZECK - NAMIBIA	SCK_2D
SGM	SELVAGEM GRANDE 1938 -SALVAGE ISLANDS	SGM_2D
SHB	ASTRO DOS 71/4 - ST HELENA ISLAND	SHB_2D
SIR	SOUTH AMERICAN GEOCENTRIC REFERENCE SYSTEM (SIRGAS) - SOUTH AMERICA	SIR_2D
SOA	SOUTH ASIA - SINGAPORE	SOA_2D
SPK	S-42 - PULKOVO 1942	
SPK-A	S-42 (PULKOVO 1942) – HUNGARY	SPKA_2D
SPK-B	S-42 (PULKOVO 1942) – POLAND	SPKB_2D
SPK-C	S-42 (PULKOVO 1942) - CZECHOSLOVAKIA (PRIOR TO 1 JAN 1993)	SPKC_2D
SPK-D	S-42 (PULKOVO 1942) – LATVIA	SPKD_2D
SPK-E	S-42 (PULKOVO 1942) – KAZAKHSTAN	SPKE_2D
SPK-F	S-42 (PULKOVO 1942) – ALBANIA	SPKF_2D
SPK-G	S-42 (PULKOVO 1942) - ROMANIA	SPKG_2D
SRL	SIERRA LEONE 1960 – SIERRA LEONE	SRL_2D
TAN	TANANARIVE OBSERVATORY 1925 - MADAGASCAR	TAN_2D
TDC	TRISTAN ASTRO 1968 - TRISTAN DA CUNHA	TDC_2D
TIL	TIMBALAI 1948 - BRUNEI AND E. MALAYSIA (SARAWAK AND SABAH)	TIL_2D
TOY	TOKYO	
TOY-A	TOKYO - JAPAN	TOYA_2D
TOY-B	TOKYO - SOUTH KOREA	TOYB_2D
TOY-B1	TOKYO - SOUTH KOREA (ALTERNATE)	TOYB1_2D
TOY-C	TOKYO - OKINAWA	TOYC_2D
TOY-M	TOKYO – MEAN SOLUTION (JAPAN, OKINAWA AND SOUTH KOREA)	TOYM_2D
TRN	ASTRO TERN ISLAND (FRIG) 1961 - TERN ISLAND	TRN_2D
VOI	VOIROL 1874 - TUNISIA/ALGERIA	VOI_2D
VOR	VOIROL 1960 - ALGERIA	VOR_2D
WAK	WAKE ISLAND ASTRO 1952 - WAKE ATOLL	WAK_2D
WGA	WORLD GEODETIC SYSTEM 1960 (WORLDWIDE)	WGA_2D
WGB	WORLD GEODETIC SYSTEM 1966 (WORLDWIDE)	WGB_2D
WGC	WORLD GEODETIC SYSTEM 1972 (WORLDWIDE)	WGC_2D
WGE	WORLD GEODETIC SYSTEM 1984 (WORLDWIDE)	WGS84E_2D
YAC	YACARE - URUGUAY	YAC_2D
ZAN	ZANDERIJ - SURINAME	ZAN_2D
 	 
AA	AIRY 1830	
AM	MODIFIED AIRY	
AN	AUSTRALIAN NATIONAL	
BN	BESSEL 1841 - NAMIBIA	
BR	BESSEL 1841 - ETHIOPIA, INDONESIA, JAPAN, AND KOREA	
CC	CLARKE 1866	
CD	CLARKE 1880	
EA	EVEREST - INDIA 1830	
EB	EVEREST - BRUNEI AND E. MALAYSIA (SABAH AND SARAWAK)	
EC	EVEREST - INDIA 1956	
ED	EVEREST - W. MALAYSIA 1969	
EE	EVEREST - W. MALAYSIA AND SINGAPORE 1948	
EF	EVEREST - PAKISTAN	
FA	MODIFIED FISHER 1960	
HE	HELMERT 1906	
HO	HOUGH 1960	
ID	INDONESIAN 1974	
IN	INTERNATIONAL 1924	
KA	KRASSOVSKY 1940	
RF	GEODETIC REFERENCE SYSTEM 1980	
SA	SOUTH AMERICAN 1969 ELLIPSOID	
WC	WORLD GEODETIC SYSTEM 1966	
WD	WORLD GEODETIC SYSTEM 1972	
WE	WORLD GEODETIC SYSTEM 1984	
WS	WORLD GEODETIC SYSTEM 1960	

In Table 14 the rightmost column “CRS Identifier” specifies the short Geodetic 2D CRS-specific identifier that may be concatenated with the MDR CRS resource base URL (http://metadata.ces.mil/mdr/ns/GSIP/crs/) to determine the corresponding registered URI to be used with the TSPI Schema.
For example, when the USMTF GEODETIC DATUM code-value is “ADI-A” then the corresponding URI is formed by concatenating the strings “http://metadata.ces.mil/mdr/ns/GSIP/crs/” and “ADIA_2D".
The resulting registered Geodetic 2D CRS URI for use in conformant XML instance documents is then:
http://metadata.ces.mil/mdr/ns/GSIP/crs/ADIA_2D
This TSPI specification does not support any Geodetic 3D CRS other than the single one that is based on the WGS 84 ellipsoid.
Annex D – GML Profiles and Application Schemas
(Informative)
D.1	Geography Markup Language
ISO 19136:2007 Geographic information – Geography Markup Language (GML) enables an interoperable transfer of spatiotemporal data among distributed systems. It specifies an open, vendor-neutral framework for the definition of application schemas that describe the spatial, temporal and other characteristics of real world objects in a standard manner. GML can be used for both the storage and transport of spatiotemporal data. Additionally, a number of OGC web-services use GML for data exchange, especially for encoding requests and responses of Web Feature Services (WFS). GML may be used to support an Internet-based infrastructure of interconnected geographic information sources and processing services.
OGC® Geography Markup Language (GML) - Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1) extends ISO 19136:2007 to specify additional geometric representations, compact geometry encodings, and enhancements in basic types and XML encoding rules.
D.2	GML Data Instances
The GML standard specifies a set of rules and constructs for encoding both spatiotemporal and non-spatiotemporal data, which are expected to be adapted to the specific requirements of a user domain. These domain-specific requirements are used to define a tailored GML application schema which defines a community information exchange format as a set of XML Schema Definition (XSD) documents.
These XSD documents define the elements and object types that may be used in a GML instance file and determine how the data in a GML instance file shall be structured (e.g.: which elements, tags or hierarchy could be expected). It is then possible to validate GML instance files against the specified application schema and verify if they are well formed (syntactically) and valid. Figure 55 illustrates the relationships between the GML standard, GML-based application schemas and GML data instances.
 
Figure 55 – Relating the GML Standard to a GML-based Application Schema and a Data Instance
D.3	GML Profiles
The GML standard enables the specification and encoding of a number of spatiotemporal representations. Because it is unlikely that there is a community information exchange requirement that would employ all of the constructs specified by the GML standard, it is desirable to be able to reduce the number of supported elements and types to only those that are required to meet the specific information exchange requirement. GML specifies a mechanism for restricting the use of its schema-components by generating profiles.
Profiles of GML are generated by selecting and restricting the constructs offered by the GML standard to just those that are necessary to accomplish specific information exchanges. A single GML profile could be the common basis for the different schemas of multiple information exchange communities. All GML-based application schemas that conform to a specific GML profile necessarily employ exactly the same restricted capabilities. Therefore, a GML profile can simplify software development, increase system performance and improve interoperability.
To define a specific GML profile, it is necessary to determine the community information exchange requirement in terms of the GML elements and types.
Figure 56 illustrates the relationships between the GML standard, a GML profile and a GML-based application schema. The construction of a GML-based application schema is a two-part process. The GML profile restricts the allowed types and elements in a manner consistent with the GML standard itself. The GML-based application schema then uses these types to define a domain specific model by extension or inclusion. In this respect extension can be understood as defining the representation of real world objects (e.g., roads and rivers) in terms of the provided GML constructs.
 
Figure 56 – Relating the GML Standard to a GML Profile and a GML-based Application Schema
The TSPI Schema is an ISO 19106-conformant Class 2 Profile  of ISO 19136:2007 (GML) and OGC® Geography Markup Language (GML) – Extended schemas and encoding rules, Version 3.3 (OGC 10-129r1). In carefully selected cases it asserts restrictions on the use of GML schema components (for example, see Section 8.4).
Because these restrictions revise the obligation of some elements (some optional elements in the GML standard are, e.g., disallowed), XML instance documents that are valid against the full set of GML schema files will not necessarily be conformant with the TSPI Schema or Information Exchange Schemas (IES) based on the TSPI Schema.
Reuse of the GML schema definitions permits existing GML-aware software applications to be easily adapted for processing XML instance documents conformant with this TSPI specification. The following assumptions have been made about software applications which are GML-aware:
•	In the case of element extension, such applications will likely ignore additional properties until they have been enhanced to understand the additional content.
•	In the case of datatype specialization, such applications will need to be enhanced before they wil be able to understand the additional content.
In order to achieve this objective for TSPI instance documents, the specified XML encoding schema is careful to first observe all requirements of GML, and then extends that encoding schema in a maximally-consistent manner to address the specific requirements of this specification.

Annex E – Extension Procedure
(Informative)
E.1	Introduction
In order to promote flexibility while maintaining interoperability, the TSPI Schema is designed to decouple – to the maximum extent possible – changes to its content from changes to its structure. The latter are manifested by new versions of the TSPI Schema. The former are manifested by the creation and dissemination of new “content models” and/or new content through a process of registration and publication in the DoD Data Services Environment (DSE) Metadata Registry (MDR).
While all releases of the TSPI Schema are published as net-accessible persistent resources in the MDR, it is possible to leverage the MDR as a means for publishing enhancements to the TSPI Schema – particularly content-enhancements – as well.
The TSPI specifies two types of extensibility-points: XML substitution groups, and code lists.
XML substitution groups allow additional group-members to be added as-needed without disturbing other members of the substitution group or existing users of the substitution group. Group additions shall meet specific semantic and syntactic requirement in order that they “fit well” with existing members of the substitution group and the intended uses of the substitution group. Annex E.2 specifies how new members may be added to substitution groups specified by the TSPI Schema.
Code lists, when coupled with a well-designed XML Schema, are based on the specification (in XML instance documents) of two identifiers – codeList and codeListValue – where:
•	The codeList specifies a remote resource in which the code list domain is defined.
•	The codeListValue is the coded value from the specified (remote resource code list) domain that encodes the concept intended (denoted) in the XML instance document.
Schematron-based (ISO/IEC 19757:2006) assertions may then be used to verify that only authoritative code lists/values are employed in information exchanges. Annex E.3 specifies how new code list values may be added to existing TSPI-related code lists, and new TSPI-related code lists be added.
E.2	Substitution Group Extension
The TSPI Schema specifies the following XML substitution groups:
•	gml:AbstractGeometry –  the head of a substitution group of which all TSPI-specified elements that represent positions are members. The technical requirements for adding new members are specified in Section 5.8 as well as a specific extension.
•	tspi:AbstractGeographicLocation –  the head of a substitution group of which all TSPI-specified elements that represent geographically-identified locations are members. The technical requirements for adding new members are specified in Section 6.4.
•	tspi:AbstractPhysicalAddress –  the head of a substitution group of which all TSPI-specified elements that represent (physical) addresses are members. The technical requirements for adding new members are specified in Section 7.4.
New XML elements, and corresponding XML types, may be added to these substitution groups and registered as part of the ‘tspi-ext’ XML namespace through governance processes associated with the GSIP Governance Namespace (see: http://metadata.ces.mil/mdr/ns/GSIP). These processes are managed by the GEOINT Standards Working Group (GWG; see: http://www.gwg.nga.mil/) through the activities of the Application Schemas for Feature Encoding Focus Group (ASFE FG; see: http://nsgreg.nga.mil/asfe). 
Extension proposals should be directed to asfechair@nga.mil.
E.3	Code List Extension
The TSPI Schema specifies the following types of information resources (see Annex A.5):
•	Coordinate Reference System (CRS) Resources  -- define the coordinate space such that the coordinate values of a position are unambiguous (see Section 5.3.1). The technical requirements for adding new CRS resources are specified in Annex A.5.2.
•	Code List Resources – define domains whose allowed values are listed. The technical requirements for adding new code list resources are specified in Annex A.5.3.
•	Physical Quantity and Unit of Measure (UoM) Resources – define physical quantities, comparable units of measure for those physical quantities, and their relationships and conversion factors documented (where appropriate). The technical requirements for adding new physical quantity and UoM resources are specified in Annex A.5.4.
•	Data Quality Measure Resources – define technical measures used to assess the quality of a data resource and its fitness for use. The technical requirements for adding new resources are specified in Annex A.5.5.
New lists (with code-members) and new codes (for existing lists) may be added to these registered resources through governance processes associated with the GSIP Governance Namespace (see: http://metadata.ces.mil/mdr/ns/GSIP). These processes are managed by the GEOINT Standards Working Group (GWG; see: http://www.gwg.nga.mil/) through the activities of the Metadata Focus Group (MFG; see: http://nsgreg.nga.mil/mfg) in coordination with the Application Schemas for Feature Encoding Focus Group (ASFE FG; see: http://nsgreg.nga.mil/asfe).
Extension proposals should be directed to mfgchair@nga.mil.

</pre>
