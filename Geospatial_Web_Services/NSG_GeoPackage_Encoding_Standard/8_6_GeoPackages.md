<html>
<head>
<style type="text/css">
<!--
.tab { margin-left: 40px; }
-->
</style>
</head>
<body>

<h2> 6.	GeoPackages </h2><br>
<ol start="6"><li>1.  File Names
GeoPackage file names SHOULD indicate the NSG data product specification contents and/or intelligence agency or DoD service mission specific contents.  GeoPackage file names MAY be constructed using official data product and mission acronyms.  Examples include:
	<ul>
<li> Example 1 
<li> Example 2
<li> Example 3
</ul>
<br>
<font color="blue">File Extension Name</font><br>
 
<br><b><i>NSG Req 1: GeoPackages that contains NSG data SHALL use the “gpkg” file extension.  They SHALL NOT use the “gpkx” file extension to indicate that they are Extended GeoPackages.</i></b><br><br>
     
</ol><br>
<ol start="6"><li>2.	Extensions

<br>
<p class="tab">Every GeoPackage must contain either tiles or features per Req17.  GeoPackages that contain tiles SHALL contain a nsg_tile_matrix_extent table per profile Clause 8.5.  Extended GeoPackages with SQL tables not defined in the OGC GeoPackage Encoding Standard SHALL register such tables in the gpkg_extensions table per GeoPackage Req79.    In GeoPackages that contain only features, the absence of row records in the gpkg_extensions table indicates the absence of extensions.  For structural consistency, this extension requires definition of the optional gpkg_extensions table in all GeoPackages that contain NSG data</p>
<br><b><i>NSG Req 2: The gpkg_extensions SQL table SHALL be defined and contain data in accordance with the GeoPackage Encoding Standard Clause 2.5 and the requirements defined therein in any GeoPackage that contains NSG data.</i></b><br><br>
</ol>
</body>
</html>
