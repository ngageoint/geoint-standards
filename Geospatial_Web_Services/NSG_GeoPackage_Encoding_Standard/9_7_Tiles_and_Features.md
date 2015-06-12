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
<br><br><br><br>
<p align="middle"><b>Table 5 Allowed Coordinate Reference Systems</b></p>
 <table>
  <tr>
    <th>CRS Name</th>
    <th>CRS AUTH ID</th>
    <th>Expl or Templ</th>
    <th>Templ XX Values</th>
    <th>CRS Type</th>
    <th>CRS Dim</th>
    <th>CRS Use</th>
    <th>CRS Def</th>
  </tr>
  <tr>
    <td>WGS 84 Geographic 3D lat/lon/hae</td>
    <td>EPSG 4979</td>
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
  </table> 

