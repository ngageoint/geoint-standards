<h2> 6.	GeoPackages </h2><br>
<ol start="6.1"><ol><li>  File Names
Extension Title
	File Names
Introduction
	This extension specifies file name and extension name requirements for GeoPackages that contain NSG data.
Extension Author
	U.S. Army Geospatial Center (AGC) and U.S. National Geospatial-Intelligence Agency (NGA), on behalf of the National Systems for Geospatial-Intelligence (NSG), author_name “nsg”
Extension Name or Template
	Extension Name “nga_file_names”
Extension Type
	Extension of existing requirement in Clause 1.1.1.1.2.
Applicability
	This extension is mandatory.  It applies to any GeoPackage that contains NSG data.
Scope
	The scope of this extension is write-only.
Requirements
GeoPackage
	NSG Req 1: This NSG extension does not require and SHALL NOT be registered in the gpkg_extensions table in a GeoPackage.
File Name
	GeoPackage file names SHOULDALL indicate the NSG data product specification contents and/or intelligence agency or DoD service mission specific contents.  GeoPackage file names MAY be constructed using official data product and mission acronyms.  Examples include:
•	Example 1 
•	Example 2
•	Example 3
 File Extension Name
	NSG Req 12: GeoPackages that contains NSG data SHALL use the “gpkg” file extension.  They SHALL NOT use the “gpkx” file extension to indicate that they are Extended GeoPackages.
      GeoPackage SQLite Configuration
	None
      GeoPackage SQLite Extension
	None
</ol></ol><br>
6.2.	Extensions
Extension Title
	Extensions
Introduction
	Every GeoPackage must contain either tiles or features per Req17.  GeoPackages that contain tiles SHALL contain a nsg_tile_matrix_extent table per profile Clause 8.5.  Extended GeoPackages with SQL tables not defined in the OGC GeoPackage Encoding Standard SHALL register such tables in the gpkg_extensions table per GeoPackage Req79.    In GeoPackages that contain only features, the absence of row records in the gpkg_extensions table indicates the absence of extensions.  For structural consistency, this extension requires definition of the optional gpkg_extensions table in all GeoPackages that contain NSG data
Extension Author
	U.S. Army Geospatial Center (AGC) and U.S. National Geospatial-Intelligence Agency (NGA), on behalf of the National Systems for Geospatial-Intelligence (NSG), author_name “nsg”.
Extension Name or Template
	Extension Name “nga_extensions”
Extension Type
	Extension of existing requirements in Clause 2.5.
Applicability
	This extension is mandatory.  It applies to any GeoPackage that contains NSG data.
Scope
	The scope of this extension is write-only.
Requirements
GeoPackage
	NSG Req 3: This NSG extension does not require and SHALL NOT be registered in the gpkg_extensions table in a GeoPackage.
	NSG Req 24: The gpkg_extensions SQL table SHALL be defined and contain data in accordance with the GeoPackage Encoding Standard Clause 2.5 and the requirements defined therein in any GeoPackage that contains NSG data.
