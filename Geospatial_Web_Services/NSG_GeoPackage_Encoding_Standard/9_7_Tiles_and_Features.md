<h2> 7.	Tiles and Features </h2>
<ol start="7"><li>1.	Spatial Reference Systems<br><br>
	This  clause specifies allowable spatial reference systems (SRS)<sup>1</sup>  that are coordinate reference systems (CRS) and their Well Known Text (WKT) definitions that SHALL be included in the gpkg_spatial_ref_sys table and referenced by the gpkg_contents, gpkg_tile_matrix_set and gpkg_geometry_columns tables srs_id column values that specify the SRS used by tile pyramid and vector feature user data tables.  The allowable CRSs are listed in Table 5 below.  CRS parameter values SHALL be those stated in Table 6 through Table 25 below.  Parameter values for CRS defined by EPSG are those specified by the EPSG Geodetic Parameter Registry when this document was published.  Parameter values for CRS specified by the U.S. National Geospatial-Intelligence Agency (NGA) are those defined in Table 9, Table 11, Table 13, Table 16 and Table 17 below.<br><br> 
Applications that can read standard GeoPackages can read the specified SRS definitions in the gpkg_spatial_ref_sys table.  
<br><br>
	
<b><i>NSG Req 3: The Allowed CRSs listed explicitly or specified as templates with parameter value substitutions in Table 5 SHALL be the only CRSs used by tile pyramid and vector feature user data tables containing NSG data in a GeoPackage.</i></b>
<p>Note:  The integer codes assigned to NGA CRSs in this document meet two conditions to avoid confusion with CRS codes used for data imported from external sources and converted to a CRS defined by NGA.  First, they are unique among all srs_id values referenced by the base GeoPackage specification and those defined in this document.  Second, they do not duplicate the codes for any CRSs registered in http://www.epsg-registry.org, although some of them do duplicate codes for coordinate operations and other items in that registry, where codes are only unique within a type.  It is recommended that these conditions continue to be met if these codes are changed by the appropriate NGA authority.</p>
</ol>
-----
<sup>1</sup>The term spatial reference system (SRS) used by the GeoPackage standard has the following lineage.  ISO 19101 specifies that Spatial Reference Systems include those for coordinates as specified by ISO 19111 and those for geographic identifiers as specified by ISO 19112.  The GeoPackage standard reused the spatial definition schema from ISO/IEC 13249-3 to define the gpkg_spatial_ref_sys SQL table and provided SQL views of it for compatibility with ISO/IEC 13249-3 and with the variant specified by OGC 06-104r4.  SRS definitions in gpkg_spatial_ref_sys only include those for coordinate reference systems (CRS).
<p align="middle"><b>Table 5 Allowed Coordinate Reference Systems</b><table>
  <tr>
    <th>CRS Name</th>
    <th>CRS<br>AUTH<br>ID</th>
    <th>Expl<br> or<br> Templ</th>
    <th>Templ XX<br> Values</th>
    <th>CRS<br> Type</th>
    <th>CRS<br> Dim</th>
    <th>CRS<br> Use</th>
    <th>CRS<br> Def</th>
  </tr>
  <tr>
    <td>WGS 84 Geographic 3D lat/lon/hae</td>
    <td>EPSG       4979</td>
    <td>Expl</td>
    <td></td>
    <td>GEOD</td>
    <td>3</td>
    <td>Feat</td>
    <td>Table 6</td>
  </tr>
   <tr>
    <td>WGS 84 Geographic 2D lat/lon</td>
    <td>EPSG 4326</td>
    <td>Expl</td>
    <td></td>
    <td>GEOD</td>
    <td>2</td>
    <td>Feat</td>
    <td>Table 7</td>
  </tr>
   <tr>
    <td>WGS 84 / World Mercator</td>
    <td>EPSG 3395</td>
    <td>Expl</td>
    <td></td>
    <td>PROJ</td>
    <td>3</td>
    <td>Feat</td>
    <td>Table 8</td>
  </tr>
   <tr>
    <td>WGS 84 / Tiled Mercator</td>
    <td>NGA 7395</td>
    <td>Expl</td>
    <td></td>
    <td>PROJ</td>
    <td>2</td>
    <td>Tiles</td>
    <td>Table 9</td>
  </tr>
  <tr>
    <td>WGS 84 / UPS North (E,N)</td>
    <td>EPSG 5041</td>	
    <td>Expl</td> 
    <td> </td>		
    <td>PROJ</td>	
    <td>2</td>	
    <td>Feat</td>	
    <td>Table 10</td>
  </tr>
  <tr>
    <td>WGS 84 / Tiled Polar Stereographic North (E,N)</td> 
    <td>NGA 7041</td>	
    <td>Expl</td> 
    <td></td>		
    <td>PROJ</td>	
    <td>2</td>	
    <td>Tiles</td>	
    <td>Table 11</td>
  </tr>
  <tr>
    <td>WGS 84 / UPS South (E,N)</td>	
    <td>EPSG 5042</td>	
    <td>Expl</td> 
    <td></td>		
    <td>PROJ</td>	
    <td>2</td>	
    <td>Feat</td>	
    <td>Table 12</td>
  </tr>
  <tr>
    <td>WGS 84 / Tiled Polar Stereographic South (E,N)</td>	
    <td>NGA 7042</td>	
    <td>Expl</td> 
    <td></td>		
    <td>PROJ</td>	
    <td>2</td>	
    <td>Tiles</td>	
    <td>Table 13</td>
  </tr>
  <tr>
    <td>WGS 84 / UTM zone XX north</td>	
    <td>EPSG 326XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>PROJ</td>	
    <td>2</td>	
    <td>Feat</td>	
    <td>Table 14 Table 15</td>
  </tr>
  <tr>
    <td>WGS 84 / UTM zone XX south</td>	
    <td>EPSG 327XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>PROJ</td>	
    <td>2</td>	
    <td>Feat</td>	
    <td>Table 14 Table 15</td>
  </tr>
  <tr>
    <td>WGS 84 / Tiled Transverse Mercator zone XX north</td>	
    <td>NGA 76XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>PROJ</td>	
    <td>2</td>	
    <td>Tiles</td>	
    <td>Table 16 Table 17</td>
  </tr>
  <tr>
    <td>EGM2008 geoid height</td>	
    <td>EPSG  3855</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>Expl</td>	
    <td>1</td>	
    <td>Comp Elev</td>	
    <td>Table 18</td>
  </tr>
  <tr>
    <td>EGM2008 geoid depth</td>	
    <td>NGA 8056</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>VERT</td>	
    <td>1</td>	
    <td>Comp Elev</td>	
    <td>Table 14 Table 15</td>
  </tr>
  <tr>
    <td>EGM96 geoid height</td>	
    <td>EPSG 5773</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>VERT</td>	
    <td>1</td>	
    <td>Comp Elev</td>	
    <td>Table 20</td>
  </tr>
  <tr>
    <td>EGM96 geoid depth</td>	
    <td>EPSG 8074</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>VERT</td>	
    <td>1</td>	
    <td>Comp Elev</td>	
    <td>Table 21</td>
  </tr>
  <tr>
    <td>MSL height</td>	
    <td>EPSG 5714</td>	<td>Templ</td>	
    <td> </td>	
    <td>Expl</td>	
    <td>1</td>	
    <td>Comp Elev</td>	
    <td>Table 22</td>
  </tr>
  <tr>
    <td>MSL depth</td>	
    <td>EPSG 5715</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>VERT</td>	
    <td>1</td>	
    <td>Comp Elev</td>	
    <td>Table 23</td>
  </tr>
  <tr>
    <td>WGS84 Geographic 2D Height (EGM08)</td>	
    <td>NGA 8101</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24<br> Table 25</td>
  </tr>
  <tr>
    <td>WGS84 Geographic 2D Depth (EGM08)</td>	
    <td>NGA 8102</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS84 Geographic 2D Height (EGM96)</td>	
    <td>NGA 8103</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS84 Geographic 2D Depth (EGM96)</td>	
    <td>NGA 8104</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS84 Geographic 2D Height (MSL)</td>	
    <td>NGA 8105</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS 84 / UTM zone XX south</td>	
    <td>EPSG 327XX</td>	<td>Templ</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>2</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS84 Geographic 2D Depth (MSL)</td>	
    <td>NGA 8106</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS84 / World Mercator Height (EGM08)</td>	
    <td>NGA 8111</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
   <tr>
    <td>WGS84 / World Mercator Depth (ETM08)</td>	
    <td>NGA 8112</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS84 / World Mercator Height (EGM96)</td>	
    <td>NGA 8113</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS84 / World Mercator Depth (EGM96)</td>	
    <td>NGA 8114</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS84 / World Mercator Height (MSL)</td>	
    <td>NGA 8115</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>WGS84 / World Mercator Depth (MSL)</td>	
    <td>NGA 8116</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS North Pole (WGS84) Height (EGM08)</td>	
    <td>NGA 8121</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS North Pole (WGS84) Depth (EGM08)</td>	
    <td>NGA 8122</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS North Pole (WGS84) Height (EGM96)</td>	
    <td>NGA 8123</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS North Pole (WGS84) Depth (EGM96)</td>	
    <td>NGA 8124</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS North Pole (WGS84) Height (MSL) </td>	
    <td>NGA 8125</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS North Pole (WGS84) Depth (MSL) </td>	
    <td>NGA 8126</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS South Pole (WGS84) Height (EGM08)</td>	
    <td>NGA 8131</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS South Pole (WGS84) Depth (EGM96)</td>	
    <td>NGA 8134</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS South Pole (WGS84) Height (MSL)</td>	
    <td>NGA 8135</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UPS South Pole (WGS84) Depth (MSL)</td>	
    <td>NGA 8136</td>	
    <td>Expl</td>	
    <td> </td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX north (WGS84) Depth (EGM08)</td>	
    <td>NGA 82XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX north (WGS84) Depth (EGM08)</td>	
    <td>NGA 83XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX north (WGS84) Height (EGM96)</td>	
    <td>NGA 84XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX north (WGS84) Depth (EGM08)</td>	
    <td>NGA 85XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX north (WGS84) Height (EGM08)</td>	
    <td>NGA 86XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX north (WGS84) Depth (MSL) </td>	
    <td>NGA 87XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX south (WGS84) Height (EGM08) </td>	
    <td>NGA 92XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX south (WGS84) Depth  (EGM08) </td>	
    <td>NGA 93XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX south (WGS84) Height (EGM96) </td>	
    <td>NGA 94XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX south (WGS84) Depth (EGM96) </td>	
    <td>NGA 95XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX south (WGS84) Height (MSL) </td>	
    <td>NGA 96XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  <tr>
    <td>UTM Zone XX south (WGS84) Depth (MSL) </td>	
    <td>NGA 97XX</td>	
    <td>Templ</td>	
    <td>01 – 60</td>	
    <td>COMP</td>	
    <td>3</td>	
    <td>Feat</td>	
    <td>Table 24 Table 25</td>
  </tr>
  </table></p> 
<b><i>NSG Req 4: The CRSs listed and defined by template parameter value substitution in Table 5 above SHALL BE defined by inserting column values into the gpkg_spatial_ref_sys_table in a GeoPackage containing NSG data and SHALL BE referenced by gpkg_contents, gpkg_tile_matrix_set and gpkg_geometry_columns tables srs_id column values.</i></b><br>  
	<p>
	These column values are specified in Table 6 through Table 25 below listed in the Table 5 “CRS Def” column above and produced by following the template instantiation instructions in the paragraphs below to create CRS WKT definitions encoded per OpenGIS® 01-009.</p>  	 
	<p><b><i>NSG Req 5: The CRS definitions in Table 6 through Table 25 below SHALL be used to specify the CRS used by tile pyramid and vector feature user data tables containing NSG data in a GeoPackage.</i></b><br></p>  
	<p>The srs_name column values do not contain the name in the definition column value in cases where the name is ambiguous or conflicts with other CRS naming conventions, i.e. the Military Grid Reference System  (MGRS), as footnoted below<sup>1</sup>.</p>  
	<p><b><i>NSG Req 6: Other SRS definitions SHALL NOT be specified for GeoPackage SQL tables containing NSG data.</i></b><br></p> 
	<p>Note:  Annex A provides a crosswalk between the Coordinate Reference Systems (CRS) defined in this clause and the corresponding identifiers in the DoD/IC Coordinate Reference Systems Dictionary in the DoD Data Services Environment (DSE) Metadata Registry (MDR), where such exist.  It proposes DSE MDR identifiers for the CRSs defined in this clause that are not registered in the DSE MDR.</p>
	<p>OpenGIS® 01-009 does not specify a WKT encoding for a 3D geodetic CRS, or a way to correctly specify the axis directions for polar stereographic projections, which are required for this profile.   OGC 12-063 / ISO 19162, which upon approval will supersede OGC 01-009, provides for WKT definition of 3D geodetic CRS and correct specification of axis directions.  An OGC Change Request Proposal (CRP) OGC 14-078 has been submitted to replace OGC 01-099 with OGC 12-063 / ISO 19162 in the next version of the GeoPackage Encoding Standard.   For forward compatibility, Annex B provides the CRS WKT definitions encoded per OGC 12-063 / ISO 19162 that will replace those in this clause when this Standardization Document is updated accordingly.</p>

-----
 <sup>1</sup>There is no requirement in 12-128r10 that the srs_name match the name in the definition column, so this profile will attempt to resolve ambiguities and conflicts with MGRS conventions.

 <p><b><i>Geographic (3D) CRS Definition</i><b/></p>
 <p align="middle"><b>Table 6 WGS 84 Geographic 3D CRS Definition</b></p>
 <table>
 <tr>
 <th>gpkg_spatial_ref_sys<br> Column Name</th>
 <th>gpkg_spatial_ref_sys <br> Column Data Value</th>
 </tr>
 <tr>
 <td> <b>srs_name</b> </td>
 <td> WGS 84 Geographic 3D lat/lon/hae<sup>1</sup>  </td>
 </tr>
 <tr>
 <td> <b>srs_id</b> </td>
 <td> 4979 </td>
 </tr>
 <tr>
 <td><b>organization</b>  </td>
 <td> EPSG </td>
 </tr>
 <tr>
 <td> <b>organization_coordsys_id</b> </td>
 <td> 4979 </td>
 </tr>
 <tr>
 <td> <b>definition<sup>2</sup> </b> </td>
 <td> GEOCCS["WGS 84",<br>
     DATUM["World Geodetic System 1984",<br>
         SPHEROID["WGS 84", 6378137, 298.257223563,<br>
	AUTHORITY["EPSG","7030"]],<br>
         AUTHORITY["EPSG","6326"]],<br>
      PRIMEM["Greenwich", 0 , <br>
         AUTHORITY["EPSG","8901"]],<br>
      UNIT["degree", 0.017453292519943278, <br>
         AUTHORITY["EPSG","9102"]],<br>
      AXIS["Geodetic latitude",NORTH],<br>
      AXIS["Geodetic longitude",EAST],<br>
      AXIS[“Ellipsoidal height",UP],<br>
      AUTHORITY[“EPSG”,”4979”]]<br>
 </td>
 </tr>
 <tr>
 <td> <b>description</b> </td>
 <td> Used by the GPS satellite navigation system and for NATO military geodetic surveying. </td>
 </tr>
</table>

-----
<p><sup>1</sup> “WGS 84” is the srs_name specified by EPSG, which is ambiguous because it is also used for 4326.  The NSG DSE MDR name for it is “World Geodetic System 1984 - Geographic 2D + HAE”, but according to Roger Lott of OGP that nomenclature does not use the correct progression. He says that WGS 84 is fundamentally a geocentric Cartesian (X,Y,Z) system (EPSG::4978). From that, geographic 3D coordinates (including HAE) may be derived (EPSG::4979).  If you drop the HAE you end up with geographic 2D (EPSG::4326).</p>
<p><sup>2</sup> EPSG defines this as a geographic 3D CRS.  Unfortunately OGC 01-099 WKT EBNF does not include an entity for definition of a 3D geographic CRS.  So the WKT definition used here is one for a geocentric CRS with the same datum, ellipsoid, and axes. Note: the unspecified unit of measure for ellipsoidal height is meters.   This definition will be replaced by the new definition in Annex B  that is encoded per OGC 12-063 / ISO 19162 once that standard is approved and cited by a future revision of OGC 12-128r10 GeoPackage Encoding Standard.</p>  

<p><b><i>NSG Req 7: The WGS 84 Geographic 3D (Lat / Lon / HAE) CRS SHALL be used only for vector features with Z geometry values.  Tiles SHALL be provided in one of the “Tiled” projected 2D SRSs defined by NGA below.</i></b></p>

	<p><i>Geographic (2D) CRS Definition</i></p>

<p align="middle"><b>Table 7 WGS 84 Geographic 2D CRS Definition</b></P>
<table>
 <tr>
 <th>gpkg_spatial_ref_sys<br> Column Name</th>
 <th>gpkg_spatial_ref_sys <br> Column Data Value</th>
 </tr>
 <tr>
 <td> <b>srs_name</b> </td>
 <td> WGS 84 Geographic 2D lat/lon<sup>1</sup>  </td>
 </tr>
 <tr>
 <td> <b>srs_id</b> </td>
 <td> 4326 </td>
 </tr>
 <tr>
 <td><b>organization</b>  </td>
 <td> EPSG </td>
 </tr>
 <tr>
 <td> <b>organization_coordsys_id</b> </td>
 <td> 4326 </td>
 </tr>
 <tr>
 <td> <b>definition</b></td>
 <td> GEOGCS["WGS 84",<br>
	DATUM["World Geodetic System 1984",<br>
		SPHEROID["WGS 84", 6378137, 298.257223563,<br>
			AUTHORITY["EPSG","7030"]],<br>
		AUTHORITY["EPSG","6326"]],<br>
	PRIMEM["Greenwich", 0 ,<br> 
		AUTHORITY["EPSG","8901"]],<br>
	UNIT["degree", 0.017453292519943278, <br>
		AUTHORITY["EPSG","9102"]],<br>
             AXIS["Geodetic latitude",NORTH],<br>
             AXIS["Geodetic longitude",EAST],<br>
	AUTHORITY["EPSG","4326"]<br>
 </td>
 </tr>
 <tr>
 <td> <b>description</b> </td>
 <td> Horizontal component of 3D system. Used by the GPS satellite navigation system and for NATO military geodetic surveying. </td>
 </tr>
</table>
<p><b><i>NSG Req 8: The WGS 84 Geographic 2D (Lat / Lon) CRS with srs_id 4326 SHALL be used only for vector features without Z geometry values.  Tiles SHALL be provided in one of the “Tiled” projected 2D CRSs defined by NGA below.</i></b></p>

----
<p><sup>1</sup>“WGS 84” is the srs_name specified by EPSG, which is ambiguous because it is also used for 4979.  This CRS is also known as Plate Carree, Cylindrical Equirectangular, Simple Cylindrical, WGS 84 Geodetic, or WGS 84 Lat/Lon.  The NSG DSE MGR name for it is “World Geodetic System 1984 - Geographic 2D”.</p>

Horizontal (2D) Projected CRS Definitions
	NGA.SIG.0011_1.0.0_WEBMERC Clause 6.2 states that “NGA does not endorse nor does NGA support the spherical based Web Mercator map projection (and variant names such as WGS 84 Web Mercator) for the acquisition, visualization, exploitation, and exchange of any GEOINT data for the NSG.”  Note: WGS 84 / Pseudo Mercator is another variant name for this map projection.
	This Clause defines 2D Mercator, Transverse Mercator and Polar Stereographic (North and South) map projections that SHALL be used instead of the spherical based Web Mercator map projection.  There are two forms of these definitions, conventional CRSs (citing EPSG definitions) and NGA Tile Pyramid CRSs defined  by the NGA Office of Geomatics in NGA.SIG.0014 and referenced herein with innovative scale factors determined in accordance with the tile pyramid design principles of Clause 8.3.  In all cases, the datum for the CRS is WGS 84.  
	 NGA Req 9: NGA Tile Pyramid CRSs SHALL be used for tiles.  
	NGA Tile Pyramid CRSs SHOULD also be used for vector features that may be rendered for tile layer display overlay.  Doing so avoids potential unnecessary coordinate conversion when vector features are stored in the corresponding conventional CRS which in effect differs only by scale factor.  Conventional CRSs MAY be used for legacy vector feature data.  Infrastructure or applications written for tile layer display overlay using such data SHOULD be written to avoid unnecessary coordinate conversion, when only affine transformation from CRS coordinates to user interface display space is required.  Table 33 in Clause 8.3 below provides a crosswalk between these two forms.   
	WGS 84 / Tiled Mercator (NGA::7395) defined in Table 9 below is the default general-purpose NGA Tile Pyramid CRS that SHOULD be used unless one of the special-purpose Tiled Transverse Mercator or Tiled Polar Stereographic CRSs is required to meet mission needs.
	NGA Req 10: Vector feature geometries with srs_id values specifying the tiled or conventional Mercator, UPS, and UTM horizontal (2D) projected  CRSs defined in this Clause SHALL NOT contain Z values.


