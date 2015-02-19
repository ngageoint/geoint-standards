

	                                                                                     NGA.STND.0046_1.0
	                                                                                            2015-XX-XX








                                          #NGA STANDARDIZATION DOCUMENT



                                       The Generic Point-cloud Model (GPM):
                                         Implementation and Exploitation
                                                 (2015-XX-XX)





                                                 Version 1.0













NATIONAL CENTER FOR GEOSPATIAL INTELLIGENCE STANDARDS
 

TABLE OF CONTENTS
1	Overview	1
1.1	Need for Error Modeling	1
1.2	Potential Strategies	1
1.3	Recommended Strategy: GPM	4
2	Purpose of Document	10
2.1	Proposed Users	10
2.2	Document Structure	11
3	Definitions	14
3.1	Terms Used in the Document	14
3.2	Error Contributors and Parameters	20
3.3	Coordinate Systems	25
4	CSM and GPM Overview	30
4.1	Overview of the Community Sensor Model (CSM)	30
4.2	Implementing GPM within CSM	33
4.3	Overview of Using GPM CSM For Lidar	35
5	Use of CSM / GPM Function Calls during Exploitation	37
5.1	Absolute Error at a Point	37
5.2	Relative error between points	37
5.3	Multi-Image Geopositioning (MIG)	40
5.4	General Data Adjustment	43
6	GPM for Sensor Model Plug-In Builders	47
6.1	SENSOR-SPACE GPM	47
6.2	GROUND-SPACE GPM	68
7	Populating / Generating GPM for Sensor Builders and Data Providers	80
8	References	94
9	GPM Storage Roadmap	96
9.1	GPM Implementation Storage Options	96
9.2	Sensor-Space GPM Storage	97
9.3	Ground-Space GPM Storage	99
Appendix A : Additional Sources of Mensuration Error	100
Appendix B Interpolation of Adjustable Parameters	102
Appendix C : Square Root of a Matrix	104
Appendix D : Sensor-Space GPM Storage Format	106
Appendix E : Ground-Space GPM Storage Format	143
Appendix F : Unmodeled Error Storage Format	161
Appendix G: GPM Master VLR	168
Appendix H: Storage and Retrieval of 3D Per-Point Error  	177
Appendix I: Use of EXTRA_BYTES VLR for PPE Pointer Per Point Record	181
Appendix J: Use of ULEM Files within the GPM Construct.	185

 
1	OVERVIEW

1.1	NEED FOR ERROR MODELING

The National Geospatial-Intelligence Agency (NGA) requires that rigorous error propagation be used for precise geopositioning scenarios.  Rigorous error propagation results in reliable accuracy predictions corresponding to the coordinates for a point of interest.  Rigorous error propagation, whether for imagery or for lidar, is generally based on a sensor model.  Casual users of high-resolution three-dimensional data may be content to work with the point cloud alone.  However, a sensor model is needed to support rigorous error propagation and adjustability in, for example, the following three point cloud scenarios:  1) standalone exploitation if the objects of interest can be identified in the point cloud; 2) use as a reference source to which other datasets can be registered; or 3) registration to another reference source of same or different modality.  
Lidar vendors today generally use proprietary physical sensor models to create point clouds, and do not make their models available to the public.  In a similar fashion, electro-optically (EO) derived point clouds are often generated using proprietary algorithms and leverage a variety of sensor models, some of them proprietary or sensitive.  Point clouds derived from other modalities would have a similar proprietary and sensitive nature.  However, the Community Sensor Model Working Group (CSMWG) maintains a strict set of rules that define an application programming interface (API) to which many sensor model builders, e.g., optical and SAR, design their sensor models.  Likewise, Sensor Exploitation Tool (SET) builders benefit from the API since they can write their photogrammetric processing code in a sensor-agnostic manner.  For the past few years, NGA has supported the CSMWG’s effort to bring lidar into the mix of sensor models associated with traditional imagery.  That is, the CSMWG has been working to add lidar sensor models to the list of sensor models that are consistent with its API, i.e., the “CSM API”, by expanding the CSM 3.0 API to handle lidar datasets.  Much of this work is encapsulated in CSMWG Information Guidance Document NGA.IP.0008_1.0, 2013-01-22 Universal Lidar Error Model (ULEM) Implementation and Exploitation Document, Version 1.0. However, in recent years, interest in point cloud datasets generated from other sources in addition to lidar has expanded.  So, the CSMWG is currently building on the previous ULEM efforts and expanding the CSM 3.0 API to handle point clouds from any source.  These efforts are encapsulated in this Generic Point-cloud Model (GPM) documentation.

1.2	POTENTIAL STRATEGIES

For the three scenarios described above, the user / application will need to do one or more of the following: (1) compute the predicted absolute geopositioning covariance at a point, (2) compute the predicted relative covariance between points, or (3) compute the full 3n   3n ground covariance to describe the predicted accuracy and relationships of a network of points.  A variety of approaches could be performed to support these calculations.  One possibility is to pre-compute the predicted absolute accuracy of every point in the point cloud and store a   ground error covariance matrix per point, as in Equation 1 - 1.
 
Equation 1 - 1 Error Covariance Matrix at a Point.
It may be possible to meet the first objective and compute the predicted absolute accuracies of all of the points and store them with the data.  However, it would become difficult or impossible to meet requirements (2) and (3) above.  As shown in Figure 1 - 1 below, once relative accuracies are required it becomes unwieldy to carry the off-diagonal cross-covariance data, shown in Equation 1-2, necessary to compute the relative accuracies between any two points in the dataset.

 
Equation 1 - 2 Error Cross-Covariance Matrix for Two Points.

 
Figure 1 - 1 Developing the Full Covariance Matrix Between Multiple Points.
An alternative is to store a very detailed physical model that is specific to the sensor(s) used to capture the dataset.  This has the advantage that it uses the sensor model that generated the three-dimensional point cloud to begin with, and thus would provide a rigorous result.  Additionally, it uses the metadata in the form that it was captured by the sensor(s) and exploited by the processing software.  However, this method has the disadvantage that every sensor and its associated metadata are unique.  Thus, a unique model must be generated for every sensor and be deployed to every SET that will use the data.  Additionally, the metadata required for each sensor will be unique and could not be standardized for implementation in a database storage schema.  So, even though this may provide the most rigorous approach, it may not be the approach that supports widespread implementation.   
An additional alternative is to assemble a model that approaches the rigor and utility of the detailed physical model while allowing for standardization of metadata and ease of storage.  This was the alternative originally recommended in the Universal Lidar Error Model (ULEM) and the approach is still encapsulated below in Sensor-Space GPM.  However, this approach becomes difficult if point clouds are created from multiple datasets, advanced algorithms, or sensors other than lidar.  In these cases, a more generic approach is required that disassociates the final point-cloud dataset from the original collection(s).  This type of approach is also described below as Ground-Space GPM.   
Since this is an early iteration of the document, it is expected that as the concepts mature, modifications will be needed. Areas with anticipated modifications or additions are labeled either To Be Revised (TBR) or To Be Determined (TBD), respectively. 

1.3	RECOMMENDED STRATEGY: GPM 

The concept of GPM has been developed to provide three main advantages.  First, it stores the metadata required to calculate the error covariances associated with a point cloud efficiently, thereby needing less metadata to generate any point’s ground covariance matrix.  Second, it provides a means to calculate full ground error covariance matrices, including cross-covariances among points, to support relative uncertainties and to support data fusion applications, such as image-to-lidar registration.  Third, it provides a means for parameter adjustability so that the point-cloud data itself can be adjusted.  GPM has less impact on data providers than alternative strategies while still providing needed error propagation for point-cloud exploitation. 
The GPM strategy employs two implementations, Sensor-Space and Ground-Space.  The Sensor-Space GPM (formerly Sensor-Space ULEM) implementation offers a generic physical sensor model, consolidating the parameters from the full physical model into a few standardized GPM parameters.  The Sensor-Space GPM model is a lidar model.  However, as will be detailed later in this document, there may be cases where this storage of sensor parameters becomes impractical and unwieldy.  Additionally, there are point clouds and elevation datasets being generated from sensors other than lidar. For these cases, GPM offers the Ground-Space model in which an efficient strategy is implemented for the storage and exploitation of pre-computed error covariances within a point cloud, yet maintains the ability to efficiently generate full covariance matrices among multiple points and therefore supports rigorous data adjustment.  To transition from raw lidar sensor data to the Ground-Space model, the Sensor-Space model will often be an intermediate step.  The key concept is that GPM standardizes the storage required from sensor-specific data to one of two possible implementations. Additionally, as will be shown later in this document, using a common CSM interface ensures that during exploitation the differences in the two models are hidden from the users and a single GPM model is used during exploitation. 

1.3.1	SENSOR-SPACE GPM OVERVIEW

The Sensor-Space GPM concept is analogous to a generic imaging physical sensor model in its approach to lidar error propagation.  Namely, it permits sensor-space parameter uncertainties (pointing, ranging, etc.) to be propagated to ground space without needing detailed knowledge of the sensor operation itself.  This is possible by defining a set of general, or universal, lidar adjustable parameters in sensor space, and storing the uncertainties of these parameters for future exploitation.  The Sensor-Space GPM concept is illustrated in Figure 1-2.
 
Figure 1 - 2 The Sensor-Space GPM Concept.

The terrain point cloud is the point-cloud dataset consisting of X, Y and Z coordinates (and possibly other attributes such as intensity) provided by the lidar.  This data is computed from the lidar timing measurements and the application of a detailed model of the lidar sensor, including the GPS/INS solutions.  Once the point-cloud coordinates are computed, the supporting information involving the sensor positions and ranges are usually not supplied with the point-cloud dataset.  The Sensor-Space GPM concept involves requesting sufficient metadata to approximately re-compute these values.  In fact, GPM only requires the sensor position to recreate the collection geometry needed for exploitation.  To obtain the sensor position, metadata is needed that samples the path of the sensor during the lidar measurements and stores the timestamp of each sample.  In addition, metadata needs to be supplied for each point in the cloud that provides the time of the point measurement and a unique identifier for the sensor path corresponding to the point.  The time for a point-cloud point could be stored as an additional attribute with the point record or it could be interpolated based on its spatial position within a Time Reference Grid that is stored with the point cloud as additional metadata. Using this timing and sensor path identifier metadata, the approximate position of the sensor can be computed.  Given the sensor position and terrain point coordinates, the estimated lidar line-of-sight (LOS) can be calculated.  This LOS vector is one key component needed to estimate the measurement precision of the terrain point.  In addition, using the sensor path epochs recorded near the time of interest, a Path Coordinate System can be established based on the vector between the platform positions associated with the epochs.  Establishment of this system is necessary for future adjustment since GPM does not carry detailed pointing and orientation information.
Other key components needed to estimate the measurement uncertainty of the terrain points are the uncertainties associated with the lidar measurement parameters.  In the actual lidar sensor these uncertainties involve the various system components, such as the GPS receiver, inertial measurement unit, offsets and rotations between components, optical component positions and angles, timing, etc.  The uncertainties will also be influenced by the processing techniques used on the datasets.  The Sensor-Space GPM concept involves working with only the resulting top-level combination of all of these individual error contributors, namely, uncertainty in the sensor position, uncertainty in the LOS angles, and uncertainty in the range measurement.  The remaining error contributors not captured in the modeling are accounted for using unmodeled error covariance (see Section 3.2.2). This GPM uncertainty metadata must be supplied as a parameter covariance matrix, perhaps as a natural output from the rigorous physical lidar model used to compute the terrain coordinates in the point cloud.  It must be provided a sufficient number of times during a dataset collection to capture variations in the parameter uncertainties over time.  
When this GPM covariance metadata is captured at the natural rate of the sensor / processing system it is generally referred to as a Data Stream format.  Alternatively, the original GPM Data Stream covariance information and the associated adjustable parameters may be converted to parameters that apply to all of the points in an individual collection unit (e.g. swath).  A collection unit may be further subsampled into a representative set of covariance estimates spanning a specified collection time and spaced at a specified interval.   These samples are referred to as posts.  GPM allows for the use of collection unit parameters, or a combination of both collection units and posts in its implementation.  Details on these concepts are supplied in Section 6 of this document.
An additional uncertainty is related to the physical features of the terrain.  For linear mode lidar, each pulse of the lidar sensor illuminates the terrain with a finite size beam which intercepts features with potentially different reflectance properties and different heights.  This leads to variations in the return pulse shape and magnitude, adding error to the range calculation.  In a similar fashion, target reflectance can also impact the number of photons returned per voxel in Geiger-mode data and the terrain shape and features can impact surface finding algorithms.  Capturing an estimate of the aggregate range uncertainty for each point in the point cloud is a valuable piece of metadata to have available for GPM if possible.  If available and pre-calculated, this error could be captured as a per-point uncertainty.  If instead it is computed by the exploitation system at time of mensuration, it can be captured as a processing-error contribution to mensuration error.   
Additional metadata needed for use with Sensor-Space GPM are the estimated decorrelation parameters for the GPM parameter uncertainties.  The addition of this information permits calculation of relative accuracies between terrain points and becomes very important in data fusion and data adjustment algorithms.
It is proposed that the point-cloud data provider (hardware vendor) supply all of this necessary metadata.  Little additional burden would be imposed, since it is already available or easily derived from the sensor model used to compute the X, Y, Z point cloud coordinates.  However, it must be passed through the processing architecture.
With the Sensor-Space GPM adjustable parameter uncertainty metadata and the computed LOS for a given terrain point, a 3D error covariance matrix can be computed using standard error propagation techniques.  This resulting matrix is useful for a number of purposes that includes providing the horizontal- and vertical-component predicted accuracies (error covariance) for the point, which is necessary when exploiting the point cloud for precision geopositioning.  The Sensor-Space GPM concept enables the calculation of these necessary terrain-point uncertainties while defining a standard set of modest metadata requirements for lidar data providers.  In addition, the GPM metadata enables rigorous data adjustments to be performed relative to the re-established LOS and the Path Coordinate System by applying updates to the GPM adjustable parameters.  In supplying this metadata, the lidar data providers need to reveal few details of the sensor design and operation, only the resulting sensor parameter uncertainties.  In addition, the relatively modest amount of metadata needed for Sensor-Space GPM more easily permits precision geopositioning exploitation applications than the alternative strategies.  Finally, the standardization makes the development of standard file formats and storage systems possible.  Detailed descriptions of the different components of Sensor-Space GPM can be found throughout this document.

1.3.2	GROUND-SPACE GPM OVERVIEW

While the Sensor-Space GPM implementation has many advantages, there will be situations where it may not be feasible.  The Ground-Space GPM implementation can be applied in cases where the complexity of the point-cloud collection and processing concept of operations precludes a straightforward definition of a sensor-space projective model within the final point cloud.  In certain cases for lidar, the Sensor-Space GPM implementation may be a preliminary step, with the final point-cloud product using pre-computed error covariance information as defined by the Ground-Space GPM implementation.  

Storing pre-computed error covariance for every point in a point cloud could be unwieldy and impractical.  Additionally, all of the error covariance in a local region of the point cloud may be very similar, creating the storage of highly redundant data.  Rather than storing the pre-computed error covariance on a per-point basis, Ground–Space GPM employs a combination of two adjustment models.  The first is based on the storage of covariance data at anchor points that reflect the local phenomena in the data.  These anchor points are at specified locations within the point cloud, each with a stored associated error covariance.  Additionally, the correlation among the errors associated with the anchor points is captured.  During exploitation, these anchor point covariance sets are used to compute the uncertainty associated with any point within a data file.  Figure 1 - 3 illustrates the basic concept of the Ground-Space GPM.  Anchor points are not necessarily co-located with specific point-cloud points, although they may be if generated by propagating covariances of point coordinates from a Sensor-Space GPM adjustment.  Furthermore, anchor points are not necessarily laid out in a two-dimensional grid pattern.
The storage of the cross-covariance information between anchor points is achieved using one of two options.  One option is to store the full error covariance of the anchor points, to include the cross-covariance terms, within the point-cloud metadata.  This method is known as the direct method.  While the direct method is the most rigorous option, the number of anchor points may limit the ability to store this entire matrix.  In situations where this full covariance matrix is not available or cannot be stored, the indirect method is used.  In the indirect method, a full  covariance matrix is stored for each of the anchor points.  However, in this case the cross-covariance terms are not directly stored, but can be computed by a set of spatial correlation function parameters which are stored in the metadata.  Both of these methods are discussed in more detail later in this document (as well as an analogous covariance storage scheme for Sensor-Space GPM).  
Some point-cloud generation systems (e.g. datasets with small extents, terrestrial lidar) employ a three-dimensional conformal transformation to align overlapping datasets.  To accommodate these systems, the second adjustment model in Ground-Space GPM consists of the three-dimensional conformal (3DC) transformation parameters and their associated variances and covariances.  One set of these parameters are stored per dataset, with each set consisting of up to seven parameters associated with a typical 3DC transformation (3 rotations, 3 translations, 1 scale).  The Ground-Space GPM can consist of only the anchor point representation, only the 3DC representation, or a combination of both the anchor point and the 3DC representations.  If indirect covariance storage is used, the resulting covariance matrix does not allow for any correlation between anchor points and the 3DC transformation parameters.  Only through direct covariance storage are correlations modeled between 3DC parameter and anchor point errors.

 
Figure 1 - 3 Ground-Space GPM for Covariance Generation.

1.3.3	RELATIONSHIP OF GPM AND ULEM

As mentioned above, NGA and the CSMWG previously developed the Information Guidance Document NGA.IP.0008_1.0, 2013-01-22 Universal Lidar Error Model (ULEM) Implementation and Exploitation Document, Version 1.0.  This document was the first attempt to integrate lidar and therefore point clouds into the CSM construct.  Over time, updates were proposed and revisions to the ULEM model were developed.  During the same time period, interest in point-cloud datasets generated from sources other than lidar expanded.  Additionally, Ground-Space ULEM provided an appropriate error model to use for these new point clouds from other sources as well as lidar. Therefore, when it came time to integrate the proposed changes to ULEM, a decision was made by the CSMWG to change the name to reflect the fact that the format is agnostic to the point-cloud source.  The original ULEM 1.0 still exists as a standard and can be referenced and used.  However, updates to ULEM 1.0 are implemented in this new Generic Point-cloud Model (GPM). The GPM model includes many updates to the Ground-Space model, but also includes updates that impact the Sensor-Space model. Therefore, if a data provider or tool developer is leveraging the metadata structures from ULEM version 1.0, they should reference ULEM.  However, if instead they plan to leverage the proposed changes encapsulated in GPM, then they must reference GPM and the associated DISR number. 
It should be noted that the Sensor-Space model applies almost solely to lidar datasets.  However, to promote continuity and limit documentation, it was decided to carry the Sensor-Space model into the GPM document even though it may not be considered “generic”. Bringing Sensor-Space into GPM allows the model to leverage the updates being included in GPM without creating yet another version of the “ULEM” document. 









2	PURPOSE OF DOCUMENT

This document is meant to serve as a reference on GPM for a variety of users with varying needs.  This section provides an overview of the targeted users, followed by a description of the document organization and its relationship to the GPM lifecycle. 
2.1	PROPOSED USERS

There are four primary groups that will use GPM, and the required amount of knowledge related to GPM across the groups will vary.  These groups include the generators of GPM metadata, the builders of the CSM-compliant GPM plug-in, the exploitation tool developers, and finally the exploiters of point clouds with GPM metadata that use the exploitation tools.  Each group is described briefly below.
The generators of GPM include those people who collect the point-cloud data and the associated people who process the data to usable products within the processing architectures.  These groups are responsible for collecting and storing the required sensor metadata upstream so that GPM metadata can be generated during processing.  Similarly, they are responsible for maintaining and tracking rigorous adjustment methods during processing to ensure that the developed GPM metadata estimates are reliable.  
The next group of interest is the builders of CSM-compliant GPM plug-ins.  As the name implies, this group builds the sensor model plug-in that the exploitation tool will access via the API.  The plug-in provides access to the GPM metadata stored within the data file.  This group needs to be familiar with the GPM metadata contents, but must also be familiar with the rigorous exploitation methods and the CSM API.
The third group is the developers of the Sensor Exploitation Tool (SET) or in the case of lidar the LIDAR Exploitation Tool (LET).  This group does not build the input data or the GPM sensor model plug-in.  However, they build tools that utilize the GPM sensor model (via the CSM API), read the GPM enabled data, and exploit the data via the API.  While they may not need to know the specifics of the GPM model, they do need to know how to use the CSM API to make the appropriate function calls in order to rigorously exploit the data.  
The final group is the data exploiters.  These exploiters of GPM data include the analyst and those people who will be reading point-cloud data into a SET/LET on a routine basis for exploitation and product generation.  These people will have little knowledge of GPM or of CSM models.  They will perform queries and analyses on the data and expect the exploitation tool and the sensor model to provide the results in standardized formats (such as CE90 and LE90).  While they may have little insight into the overall process, these are the people who will be interpreting the final results and making decisions based on those results.

2.2	DOCUMENT STRUCTURE

As shown in Figure 2 - 1, GPM (and formerly ULEM) as a concept spans multiple processes from the collection of the raw data and the associated metadata, to the generation of the GPM metadata from the sensor specific raw metadata, to the exploitation of the data / GPM metadata using a CSM sensor model.  As discussed above, there are four primary groups that will perform these processes that include the generators of GPM, the builders of the CSM-compliant GPM plug-in, the SET/LET developers, and the exploiters of the GPM data.  This section describes how the remainder of this document is organized with respect to the GPM flow shown in Figure 2 - 1, and how the various sections of the document relate to the four GPM user groups.
 
Figure 2 - 1 The GPM Lifecycle and the Associated References in this document.
This document provides concise but thorough direction to generators of GPM data (boxes 1 and 2), exploiters of GPM data and SET developers (box 6), and to the builders of the GPM CSM plug-in (box 4), which is the cornerstone that connects the data providers and point-cloud data exploiters to one another via standardized interfaces.  The first key interface is the “GPM Standardized Metadata” interface (box 3) which defines the metadata format into which data providers shall convert their sensor-specific point-cloud metadata.  The second key interface is the “CSM API” (box 5) which defines the methods to which the exploitation tool can make calls in order to execute an exploitation workflow, such as relative mensuration, absolute geolocation or multi-modal block adjustment.  
Table 2-1 lists the titles of the discussed sections for quick reference. 
Table 2 - 1:  Titles of Referenced Sections.
Section Number	Title

4	
CSM and GPM Overview

5	Use of CSM/GPM Function Calls During Exploitation

6	GPM for Sensor Model Plug-In Builders

7	Populating/Generating GPM for Sensor Builders and Data Providers

App. D-I	GPM Storage Formats

Section 4 provides insight into the CSM API, CSM functions, and function calls that will be implemented within a CSM-compatible sensor model plug-in.  It defines the expected inputs and outputs of the various functions.  Section 6 then provides the details of both the Ground-Space GPM and the Sensor-Space GPM that are necessary to develop a CSM-compliant plug-in compatible with each implementation.  This section describes how the plug-in will use the point-cloud metadata that is stored in the standardized GPM format documented in Appendices D-J.  Both sections 4 and 6 are useful references for the CSM GPM plug-in developer.
Section 5 provides exploitation algorithms for mensuration, geolocation, and adjustment as functions of the CSM API function calls documented in Section 4.  A major advantage to this modular approach is that the SET/LET does not need to know details about sensor modeling and upstream processing since this concern is handled by the GPM CSM plug-in.  As far as the SET is concerned, it is simply exploiting point-cloud data that could have been derived from any source, e.g. lidar, stereo EO, stereo SAR, etc.  Similarly, this modular approach offers the major advantage that the CSM plug-in only needs to concern itself with a single GPM standardized metadata construct from which it instantiates the appropriate point-cloud sensor model.  The details of how to implement the CSM plug-in’s methods are documented in Section 5.  
Working our way upstream (box 1 and 2 of Figure 2 - 1), the responsibility of the data providers is to implement their sensor-specific GPM generators in order to provide support data that can be used to instantiate a CSM-compliant GPM sensor model.  Data providers may need to perform various levels of pre-processing that could be as simple as translating metadata elements from sensor-specific to Sensor-Space GPM, or as complex as performing widespread block adjustments for improved accuracy and then transforming the associated metric descriptors into the GPM uncertainty parameters (adjustable parameters and corresponding error covariance) associated with the collective dataset.  The mathematics and algorithms, associated with this pre-processing, are documented in Section 7.  This document does not address the details of each possible instance of sensor-specific lidar metadata nor of the metadata associated with the various alternatives for point-cloud generation from other modalities, since there can be an abundant number of different upstream architectures. Hence, the data processor’s responsibility is to obtain whatever level of detail it needs in order to process the data and report its complete error covariance information in the GPM standardized metadata format. 

 

3	DEFINITIONS

3.1	TERMS USED IN THE DOCUMENT
3.1.1	ABSOLUTE HORIZONTAL ACCURACY
Statistical representation of all random and systematic errors encountered in determining the horizontal position of a single data point with respect to a specified geodetic horizontal reference datum, expressed as a circular error at the 90 percent probability level (CE90). There are two types of absolute horizontal accuracy: predicted absolute horizontal accuracy is based on error propagation; and measured absolute horizontal accuracy is an empirically derived metric [adapted from [1]].
3.1.2	ABSOLUTE VERTICAL ACCURACY
Statistical representation of all random and systematic errors encountered in determining the elevation of a single point with respect to a vertical reference datum, expressed as a linear error at the 90 percent probability level (LE90). There are two types of absolute vertical accuracy: predicted absolute vertical accuracy is based on error propagation; and measured absolute vertical accuracy is an empirically derived metric [adapted from [1]].
3.1.3	ACCURACY
Closeness of agreement between a test result and the accepted reference value.  [2] This defines measured accuracy or empirically derived accuracy.  There is also predicted accuracy based on error propagation that provides estimated accuracies at points or across datasets. 
3.1.4	ADJUSTABLE MODEL PARAMETERS
Model parameters that can be refined using available additional information such as measured coordinates of ground control or tie points. Whether refined or not, adjustable parameters also provide a basis for the representation of estimated model accuracy.
3.1.5	ANCHOR POINTS
Specified locations within a dataset characterizing predicted uncertainties for local error phenomena. 
3.1.6	APPLICATION PROGRAMMING INTERFACE (API)
The interface (calling conventions) by which an application program accesses privileged utilities, providing a level of abstraction between the program and the utilities.  For CSM, its API provides a level of abstraction between a SET and the instantiated sensor model plug-in.
3.1.7	ATTITUDE
The angular orientation of a body, described by the angles between the axes of that body’s coordinate system and the axes of an external coordinate system [3].

3.1.8	COORDINATE
One of a sequence of   numbers designating the position of a point in  -dimensional space [4]  NOTE:  In a coordinate reference system, the numbers must be qualified by units.
3.1.9	COORDINATE CONVERSION
A general term used to describe changing the reference system associated with a set of coordinates.  As opposed to coordinate transformations, coordinate conversions are exact mathematical processes.  That is, there are no errors in the parameters describing a coordinate conversion.  This could include modifications such as unit conversions and map projections.  
3.1.10	COORDINATE REFERENCE SYSTEM
The coordinate system that is related to the real world by a datum [4].  
3.1.11	COORDINATE SYSTEM
The set of mathematical rules for specifying how coordinates are to be assigned to points [4].
3.1.12	COORDINATE TRANSFORMATION
A method to relate the coordinates in one coordinate reference system to a second coordinate reference system by means of a system of linear algebraic equations [5].  As opposed to coordinate conversions, coordinate transformations are defined by measurements.  Therefore, the parameters that describe a coordinate transformation contain errors.
3.1.13	CORRELATION
The degree of linear dependence between two random variables.  [6]
3.1.14	COVARIANCE 
The expected value of the product of the deviations of two random variables from their respective means. In the case of error covariance matrices, the means are zero. [6]
3.1.15	CROSS-COVARIANCE
The expected value of the product of the deviations from the respective means of two random variables at different epochs.  In the case of error covariance, the means are zero.
3.1.16	ERROR PROPAGATION
The occurrence of errors in quantities computed from measurements.  Or, the determination of the uncertainty of the computed quantities based on the uncertainty of the measurements.
3.1.17	EXPLOITATION TOOL
Software tool that is used to view and manipulate a dataset, metadata, and an associated sensor model in order to generate geospatial information or output products to be used by downstream consumers.
3.1.18	FULL COVARIANCE
A fully populated variance-covariance matrix that includes both the variance of individual variables and the covariance, including cross-covariance, between all pairs of variables.
3.1.19	GEIGER MODE
Type of lidar system for which the detector is biased and becomes sensitive to individual photons (photon counting).  These detectors exist in the form of arrays and are bonded with electronic circuitry.  The electronic circuitry produces a measurement corresponding to the time at which the current was generated, resulting in a direct time-of-flight measurement.  A lidar system that employs this detector technology typically illuminates a large scene area with a single pulse.  The direct time-of-flight measurements are then combined with platform location / attitude data along with pointing information to produce a three-dimensional product of the illuminated scene of interest.  Additional processing is applied which removes existing noise present in the data to produce a visually exploitable data set. [adapted from[8]].
3.1.20	GENERIC SENSOR MODEL
A mathematical description of a sensing system (sensor model) that is not designed and built around the intricate design parameters and specific variables associated with a particular make or model of sensor, but is instead based on general variables and parameters that can be used to describe a certain type / class of sensor.  An example is a generic frame sensor model to describe the imaging with an electro-optical camera where the sensor model is based on common parameters (e.g. focal length, array size).
3.1.21	GEODETIC COORDINATE SYSTEM
Coordinate system in which position is specified by geodetic latitude, geodetic longitude and (in the three-dimensional case) ellipsoidal height [4].
3.1.22	GEODETIC DATUM
Datum describing the relationship of a coordinate system to the Earth [4].
NOTE 1: In most cases, the geodetic datum includes an ellipsoid description
NOTE 2: The term may be applicable to some other celestial bodies.
3.1.23	GEOPOSITIONING
Determining the ground coordinates of an object from sensor measurements (also referred to as geolocating).
3.1.24	GROUND CONTROL POINT
A point on the ground, or on an object located on the Earth surface, that has an accurately known geographic location.
3.1.25	GROUND COORDINATES
Model coordinates to which the current values of the adjustable parameters (note that these are typically zero-valued pre-adjustment) have been applied. In addition to having been transformed per the adjustable-parameter values, the points have also been converted from the model-space coordinate system to ECEF as required by CSM.
3.1.26	GROUND-SPACE GPM / ULEM
Implementation of GPM / ULEM in which adjustable parameter values and associated error covariance matrices are carried in point-coordinate space as opposed to sensor-parameter space.  The Ground-Space model provides an efficient strategy for the storage and exploitation of pre-computed error covariances within a point cloud while maintaining the ability to efficiently generate full covariance matrices among multiple points and perform data adjustments.  
3.1.27	INTENSITY
The power per unit solid angle from a point source into a particular direction.  Typically for LIDAR, sufficient calibration has not been done to calculate absolute intensity, so relative intensity is usually reported.  In linear mode systems, this value is typically provided as an integer, resulting from a mapping of the return’s signal power to an integer value via a lookup table.
3.1.28	LIDAR
Acronym for Light Detection and Ranging.  A system consisting of 1) a photon source (frequently, but not necessarily a laser), 2) a return-signal detection system, 3) a timing circuit, and 4) optics for both the source and the receiver that uses emitted light to measure ranges to and/or properties of solid objects, gases, or particulates in the atmosphere.  Time-of-flight (TOF) lidar systems use short laser pulses and precisely record the time each laser pulse was emitted and the time each reflected return is received in order to calculate the distance(s) to the scatterer(s) encountered by the emitted pulse.  For topographic LIDAR, these time-of-flight measurements are then combined with precise geospatial platform location/attitude data along with pointing data to produce a three-dimensional geospatial product of the illuminated scene of interest.
3.1.29	LINE OF SIGHT
A line from an observer's eye to a distant point [Merriam-Webster on-line dictionary].  In the context of LIDAR, ULEM, and GPM the observer is the LIDAR instrument and the line of sight refers to the ray from the LIDAR sensor to the observed point.
3.1.30	LINEAR MODE
LIDAR systems operated in a mode where the output photocurrent is proportional to the input optical incident intensity.  A LIDAR system which employs this technology typically uses processing techniques to develop the time-of-flight measurements from the full waveform that is reflected from the objects in the illuminated scene of interest.  These time-of-flight measurements are then combined with precise geospatial platform location / attitude data along with pointing data to produce a three-dimensional geospatial product of the illuminated scene of interest. [adapted from [9]]
3.1.31	METADATA
Data about data [10].  In GPM, the data is the point cloud (X,Y,Z,I of each point), while the metadata includes supporting information (e.g. time tags, trajectory, error covariance matrices, temporal correlation parameters)  that allows for rigorous error propagation and data adjustments.
3.1.32	MODEL COORDINATES 
For GPM and ULEM, model coordinates refer to coordinates of the dataset points in the coordinate system in which they are stored.  During an adjustment procedure, model coordinates are treated like measurements with associated a priori measurement covariance representative of a human’s or algorithm’s ability to identify and select the point.  Model coordinates can be provided in a variety of coordinate systems and/or projections (e.g. ECEF, LSR, UTM) while CSM requires the Ground Coordinates to be in Earth Centered Earth Fixed (ECEF) coordinates. 
3.1.33	NADIR
The point of the celestial sphere that is directly opposite the zenith and vertically downward (in this document defined as normal to the ellipsoid) from the observer. [11] 
3.1.34	PHYSICAL SENSOR MODEL
A sensor model that describes the physics and the physical aspects associated with data capture using a sensor.  The physical sensor model is often specific to a given sensor (although there may be common terms between sensors), and designed around characteristics (e.g. optics, pointing subsystem) that are often unique to a given sensor.  The Sensor-space model is a generic physical sensor model for lidar. 
3.1.35	PLATFORM COORDINATE REFERENCE SYSTEM
The coordinate reference system fixed to the collection platform within which positions on the collection platform are defined.
3.1.36	PLUG-IN
A small piece of software that supplements a larger program [11].  The term plug-in refers to an independent software program with defined interfaces which will operate with other applications but will not interfere with the operation of other co-resident applications.  For this document, plug-in describes the CSM sensor models used to exploit data.
3.1.37	POINT CLOUD
A collection of data points in 3D space.  The distance between points is generally non-uniform and hence all three coordinates (Cartesian or spherical) for each point must be specifically encoded.
3.1.38	PREDICTED ACCURACY
Probabilistic metric quantifying the expected error characteristics for a measurement, often assumed (but not required) to be normally distributed in nature and often provided as a variance (1-D case) or covariance matrix (otherwise).
3.1.39	PROCESSING (UPSTREAM PROCESSING AND DOWNSTREAM PROCESSING)
For this document, processing refers to any procedure that is combining multiple input data types to generate a new data type, or processes used to modify and adjust a given data type (i.e. registration).  Upstream processing refers to processing that occurs closer to the actual data collection (e.g. generation of the initial point cloud).
3.1.40	RANDOM ERROR
Random errors are non-deterministic errors with an assumed mean value of zero and are uncorrelated between any arbitrary pair.
3.1.41	RELATIVE ACCURACY
Closeness of agreement between the measured relative vector between a pair of points and the relative vector extracted from an accepted reference. 
3.1.42	RELATIVE HORIZONTAL ACCURACY
Closeness of agreement between the measured relative horizontal vector between a pair of points and the relative horizontal vector extracted from an accepted reference.  There are two types of relative horizontal accuracy: predicted relative horizontal accuracy is based on error propagation; and measured relative horizontal accuracy is an empirically derived metric.
3.1.43	RELATIVE VERTICAL ACCURACY
Closeness of agreement between the measured relative vertical vector between a pair of points and the relative vertical vector extracted from an accepted reference.  There are two types of relative vertical accuracy: predicted relative vertical accuracy is based on error propagation; and measured relative vertical accuracy is an empirically derived metric.
3.1.44	SENSOR EXPLOITATION TOOL 
Within the CSM construct, software written to execute photogrammetric algorithms (e.g. resection) using the functions available from the CSM API.
3.1.45	SENSOR MODEL
Mathematical description of the relationship between a sensing system (including its measurements and uncertainties) and the three-dimensional object space of interest.  A sensor model also provides a means to perform rigorous error propagation and sensor parameter adjustment.
3.1.46	SENSOR-SPACE GPM / ULEM
The Sensor-Space GPM / ULEM implementation offers a generic physical sensor model, consolidating the parameters from the full physical model into a few standardized GPM / ULEM parameters.
3.1.47	THREE-DIMENSIONAL CONFORMAL (3DC) TRANSFORMATION
Also known as a Seven-Parameter or Helmert Transformation.  A 3-dimensional transformation consisting of seven parameters:  a uniform scale, three rotations and three translations.  It takes the general form  , where   is the 3D vector pre-transformation,   is the 3D vector post-transformation,   are the translation parameters,   is the rotation matrix constructed from the three rotation parameters, and   is the scale parameter.
3.1.48	UNCERTAINTY
General measure that addresses any statistical expression of predicted accuracy (e.g. CE90, LE90, covariance matrix).
3.1.49	UNMODELED ERROR
Combined effect of high-frequency systematic and random errors that cannot be removed by adjustable parameters.  The possible presence of systematic errors implies that two points within a short distance often have unmodeled errors that are correlated (not purely random)
3.1.50	VOXEL
A volume element, the 3D equivalent to a pixel in 2D.

3.2	ERROR CONTRIBUTORS AND PARAMETERS
3.2.1	CORRELATION MODEL

For GPM, the four-parameter correlation decay model as defined by the CSM is employed [13, 14].  For two points in a dataset separated in a given dimension (time or distance), this model defines the correlation coefficient (ρ) specifying the correlation between the points.  The general form for the correlation decay model is shown in Equation 3 - 1, where:
•	 
•	 
•	 
•	 
•	 
•	 
 
Equation 3 - 1  CSM four-parameter correlation model.
In this formulation,    (unit-less) controls the maximum correlation that can be obtained when   is greater than zero,   (unit-less) determines the minimum correlation value that can be obtained,   (unit-less) primarily controls the shape of the correlation curve, and   is a time constant that primarily controls the rate of the decay and is in the same units as . More detail on these four parameters is available in the CSM documentation.  
 
Figure 3 - 1  Graphical depiction of correlation parameters.
Above,   represents the difference between points in the dimension of interest.  In some models this dimension may be a temporal difference (thus the ).  However, in others it may be a spatial relationship that relates to ,  , or some other dimension.  In the case of spatial correlation, the correlation may have a distinct behavior with respect to each component of another primary coordinate system ( ) instead of with respect to each component of the cardinal (i.e. Model-space)  - -  directions.  For GPM, this system is derived using the theta angles ( ) that describe the sequential rotations (counter-clockwise positive) about the Model   axes, resulting in the   axes.  To formalize the required transformation, define two points in xyz-space and compute the distance between them: 
Given:  and  , Compute:  
Then the transformation to take these differences from xyz-space to uvw-space is:
 
Once in the ( ) coordinate system, the amount of correlation between the unmodeled errors (Section 3.2.2) and between anchor point errors (Section 6.2) is assumed to vary based on the spatial separation in the  ,   and   dimensions between points and is computed by Equations 3-3 and 3-4 (independent applications of Equation 3-1 for  ).

3.2.2	UNMODELED ERROR

One key contributor to the overall error propagation, particularly for predicted relative accuracy, is unmodeled error.  Per the CSM API TRD, unmodeled errors consist of errors that cannot be practically characterized by the physical sensor model’s support-data adjustable parameters.  Hence, contrary to adjustable parameters, unmodeled errors cannot be corrected or removed through a registration or triangulation process.  Other key characteristics of unmodeled error include that they collectively consist of high-frequency systematic and random components.  However, two points within a short distance often have unmodeled errors that are correlated (not purely random).  Therefore, the unmodeled error method employed must include a correlation model in addition to the covariance.  
For both Sensor-Space and Ground-Space GPM, the unmodeled error is represented by a series of    covariance matrices as shown in Equation 3-2.  A set of these unmodeled error covariances are established across the dataset at specified ( ) locations, or posts (the matrix in Equation 3-2 is for some post  ).  Note that the posts used here in describing unmodeled error are not the same as those in the posts concept used in Sensor-Space GPM, nor are they necessarily located at ground-space anchor point locations.
 
Equation 3 - 2  Unmodeled Error Covariance Matrix  .
The unmodeled error for an arbitrary location within the dataset will be determined using nearest-neighbor interpolation to the nearest unmodeled error post.  It is important to note, that the spacing and the number of unmodeled error posts required is dataset dependent.  In many cases, the unmodeled errors may be sufficiently described using a single unmodeled error post, for which an interpolation would not be required (equivalently, one would use a nearest-neighbor interpolation to that single data point).  
As mentioned above, points selected in close proximity may have highly correlated unmodeled errors.  However, due to the purely random contributors to the unmodeled error, coincident points may not be perfectly correlated (correlation equal to one).  For GPM, the four-parameter correlation model as defined by the CSM and described in Section 3.2.1 is being employed.  The correlation is defined to decay along the primary axes of the ( ) system that is defined by sequentially rotating about the x , y and z axes by the theta angles ( ) .  Once in the   coordinate system, the amount of correlation between the unmodeled errors is assumed to vary based on the spatial separation between points in the  ,  , and   directions ( ).  
Therefore, there are separate decay models for the  ,    and   directions as shown in Equation 3 - 3.  This leads to a final computation for the unmodeled error correlation between points, which is shown in Equation 3 - 4.
 ,   ,
 
Equation 3 - 3 Correlation functions in the  ,   and   dimensions.

 
Equation 3 - 4  Final correlation estimates between two points in the point cloud.

If two points are expected to be perfectly correlated at zero distance ( , then the   parameters would be equal to one.  However, because of the purely random contributors mentioned above, the   parameters will often be reduced to limit the maximum correlation between points (  to some smaller value such as 0.8 (TBR), so that even points very close together exhibit some relative uncertainty between them.  
The unmodeled error cross-covariance between two points can be determined by Equation 3 - 5, where   and   are the unmodeled error covariances for points r and s, respectively.  The calculation of the square root of a matrix required for Equation 3 - 5 is given in Appendix C.  
 
Equation 3 - 5  Unmodeled error cross-covariance matrix between two points (r and s).
The full ( ) unmodeled error covariance ( ) between two points (  and  ) can then be formed using Equation 3 - 6.  These principles can be extended to generate full ( ) unmodeled error covariance matrices for   points.
 
Equation 3 - 6  Full unmodeled error covariance matrix between two points (r and s).
Information on the storage of the unmodeled error data for ULEM is provided in Appendix F.

3.2.3	MENSURATION ERROR

Much of this document focuses on Sensor-Space GPM and the ability to take sensor covariance information ( ) and propagate it into a ground-space covariance ( ) representing positional uncertainty of the point of interest.  Similarly, other parts of this paper focus on recovering a covariance at the point of interest from the Ground-space model error propagation.  However, it is important to note that even in the simple case of propagating the absolute error at a single point, this propagated covariance ( ) is only part of the overall uncertainty at the mensurated point.  In addition to the contribution from unmodeled error ( ), as described previously, the mensuration error ( ) must also be taken into account.  The traditional mensuration error is based on the random error associated with the analyst’s ability to pick a point of interest, and has no correlation from one point to the next.  In the case of mensurating in a 3D point cloud, this mensuration error is modeled by a series of   covariances for each mensurated point that are then combined into a block diagonal matrix as shown below in Equation 3 - 7. 
 
Equation 3 - 7  Covariance matrix for analyst’s contribution to mensuration error.
In Equation 3 - 7,  
 
represents the uncertainty from analyst mensuration error at a specific point,  .   Note that the covariances in the matrix of mensuration error will often be negligible.
Additional contributors to mensuration error are discussed in Appendix A.

3.3	COORDINATE SYSTEMS

A sensor model is used to determine ground coordinates of sensed objects using measurements from various system components, and to propagate the system error estimates to a sensed point.    The reference frame of each component and their interrelationships must be understood to effectively utilize the model.    The GPM geometric model, as also used in ULEM, is generalized and does not directly utilize coordinate systems associated with specific sensor components, but rather leverages three generalized and consolidated coordinate systems.  The three primary systems used by GPM include the Path Coordinate System (PCS), the Ray Coordinate System (RCS), and the Model-space Coordinate System (MCS).  Additionally, there are several other common coordinate systems that may be used in the GPM generation and exploitation process which include geographic coordinates, Earth Centered Earth Fixed (ECEF) coordinates, and projected coordinates (e.g. UTM).  
In addition to these primary systems, other coordinate systems such as a platform system may be used in the generation of GPM metadata.  However, once GPM metadata is generated, these additional systems are no longer needed.  
The following sections will define the primary coordinate systems needed for GPM and their interrelationships.

3.3.1	MODEL-SPACE COORDINATE SYSTEM

The Model-space Coordinate System (MCS) is the chosen coordinate system in which all GPM parameters and covariances will be stored for a given file.  The coordinate systems that may be used as the MCS are:
•	Earth Centered Earth Fixed (ECEF).
•	Local Space Rectangular (LSR) – requires origin and rotations (Figure 3-2 shows an ENU LSR coordinate system).
•	UTM – requires hemisphere and zone.
The information describing the MCS chosen for a given dataset is stored in an MCS Variable Length Record (see Appendix G for storage description).  Note that the point-cloud points may be in a different coordinate system than the metadata that is referenced to the MCS.  Coordinates derived from the points must be converted to the MCS prior to performing exploitation calculations.
  
Figure 3 - 2  An East – North – Up LSR coordinate system.

3.3.2	PATH COORDINATE SYSTEM

The Path Coordinate System (PCS) is uniquely defined for each specific epoch of interest.   The origin for this system is the instantaneous sensor location as estimated from the trajectory information interpolated at the epoch of interest.  Its +XP axis is along the velocity vector of the aircraft.  The +YP axis is the cross-product of the PCS +XP axis and the ellipsoid normal defined at the current platform position.  The +ZP axis is then the cross-product of the PCS +XP and +YP axes, completing a right-handed Cartesian coordinate system.  Figure 3 - 3 illustrates the PCS.
 
Figure 3 - 3  Path Coordinate System (PCS)  NOTE: Path coordinate system may not be aligned with the heading of the aircraft as shown here.

3.3.3	RAY COORDINATE SYSTEM

The final primary coordinate system used in GPM is the Ray  Coordinate System (RCS) (Figure 3 - 4).   The origin for this system is the instantaneous sensor location as estimated from the trajectory information interpolated at the epoch of interest (and coincides with the origin of the PCS).  This is a local coordinate system which is relative to the specific ray connecting the sensor location at a specific epoch to the lidar point of interest.  It is an orthogonal system with the +ZR axis defined along the ray from the sensor to the ground point.  The +YR axis is the cross product of the +ZR axis and the PCS +XP axis.  The +XR axis is then the cross product of the +YR axis and the +ZR axis, completing a right-handed system.  Figure 3 - 4 illustrates the RCS.
 
Figure 3 - 4  Ray Coordinate System.
The relationships among the GPM coordinate systems are illustrated in Figure 3 - 5.  Here, the origin of the PCS is indicated as [ ,  ,  ] in the MCS and is assumed to be a function of time,  .  The axes XL, YL and ZL represent an LSR system, used for the MCS.
 
Figure 3 - 5  Relationships Among GPM Coordinate Systems.

 

4	CSM AND GPM OVERVIEW

Many applications, such as precise geopositioning, need metadata and sensor models to allow the predicted error covariances from the sensor and processing to be rigorously propagated to the ground in order to estimate ground-space covariances in the final products.  Additionally, there is a need for rigorous methods to adjust and fuse datasets.  These methods require both absolute and relative accuracy estimates between a series of points within single, and across multiple, datasets.  As described earlier, GPM is a method to meet these needs for point clouds (derived from lidar, EO, etc).  Challenges include developing models, methods, and tools that can be easily integrated into a variety of exploitation tools.  However, the Community Sensor Model Working Group (CSMWG) has been developing and maintaining a variety of sensor models to address these challenges.  A major goal of GPM is to integrate point-cloud functionality into the CSM API and promote interoperability in point-cloud exploitation.  This section provides a brief overview of CSM and then describes how lidar, point-cloud, and GPM functionality will be incorporated into CSM. 

4.1	OVERVIEW OF THE COMMUNITY SENSOR MODEL (CSM)

The US Air Force Aeronautical Systems Center and the National Geospatial-Intelligence Agency (NGA) initiated a program called the CSMWG which maintains an application program interface (API) to standardize sensor exploitation tools’ access to physical sensor model methods without insight into the detailed, and often proprietary, mathematics describing the sensing systems.  This API makes it possible for multiple tools to interface with multiple sensor models in standardized ways to perform error propagation, data adjustment, and fusion with single or multi-modal datasets.  
Users of geospatial data will often apply multiple datasets to a problem, whether the datasets are from the same or similar sensors, or from sensors using completely different modalities.  This fusion of geospatial datasets generates the need for geospatial fidelity among the datasets, which is best obtained by rigorous data adjustment using physical sensor models.  Likewise, accurate prediction and propagation of error covariance matrices are needed, which also demands use of sensor modeling.  However, implementing multiple sensor models within an application such as a Sensor Exploitation Tool (SET) can become difficult due to the complexity and sometimes proprietary nature of the models.
Standardized functions (or Key Methods) defined by the CSM API relate a sensed object to its representation in the geospatial product (e.g. image or point cloud) as a function of the sensor parameters, assign a measure of accuracy to the transformation, and provide a means to adjust the parameters for data registration or fusion.  This allows a user to develop a SET using CSM function calls without knowing the mathematical details of each sensor.  Tools can be written using CSM calls such that the same tool can utilize different sensor models.  The sensor models are often provided by the sensor vendor as shared libraries, and must be written to accept CSM function calls.  Recently, there has been a movement to develop more generic sensor models that can be used by the community on a variety of sensors with similar modality.   The CSM concept is further illustrated in Figure 4 - 1.
CSM has a variety of standardized functions and the user is asked to reference the CSM Technical Requirements Document (TRD) version 3.0.2 [15] for all of the details. Although there are many methods in the CSM API, the critical methods required to support photogrammetric data adjustment are listed below:
•	imageToGround – given the line and sample of an image pixel, calculate the associated ground XYZ coordinates.  Optionally, the image-coordinate covariance could be provided as additional input, and then ground covariance would be included in the output.
•	groundToImage – given the ground   coordinates, calculate the associated image line and sample.  Optionally, the ground covariance could be provided as additional input, and then image-coordinate covariance would be included in the output.
•	computeSensorPartials – given ground   coordinates, calculate the partial derivatives of the associated line and sample with respect to a designated sensor parameter.  For situations when the associated line and sample are needed to prevent redundant calculation (e.g. numerical partial derivatives), optional line and sample values may be passed, or a call to groundToImage would be needed within computeSensorPartials.
•	computeGroundPartials – given ground   coordinates, calculate the partial derivatives of the associated line and sample with respect to the  ,   and   values.
•	getParameterValue – given the index to a sensor parameter, return the current value of the adjustable parameter identified by the index.
•	getParameterCovariance - given two parameters (each specified by their index), return the covariance value of the specified parameter pair.  If index 1 equals index 2 for the parameter pair, then the variance of the parameter is returned.
•	getCrossCovarianceMatrix - returns a matrix containing all elements of the error cross-covariance matrix between the instantiated sensor model and a specified second sensor model.  
•	getUnmodeledError – for a given data point, provide the unmodeled error covariance specific to that point.  In the case of an image, a line and sample is passed in and a 2 by 2 covariance matrix describing the line and sample unmodeled error is returned.
•	getUnmodeledCrossCovariance – for two specified data points, return the unmodeled cross-covariance between the points.  In the case of an image, the two points are specified by line and sample values and the cross-covariance (in line and sample) between the two image points is returned.
•	setParameterValue – given the index to a sensor adjustable parameter and a desired value for that parameter, update the sensor model with the parameter value.  
•	setParameterCovariance – given index values to identify a parameter pair and a covariance value, update the sensor model covariance value for the pair of parameters. If index 1 is equal to index 2, then the variance for the parameter associated with index 1 will be updated.
These methods are designed primarily to operate on data which can be represented in image space, i.e. the data are arranged in a raster of lines and samples.  They are not currently set up to handle the irregularly-spaced 3D point clouds. The section below describes how point-cloud structures will be implemented within CSM.
  
Figure 4 - 1  The Community Sensor Model API and its interaction with photogrammetry tools and sensor models.



4.2	IMPLEMENTING GPM WITHIN CSM

The typical point-cloud product consists of irregularly-spaced three-dimensional points referenced to a ground-based coordinate system.  As discussed earlier, the fundamental methods of CSM are primarily designed to operate on data which can be represented in image space where the data are arranged in a raster of lines and samples. This section describes changes required to the CSM construct to accommodate the peculiarities of the point-cloud formats. 
Point clouds are often stored with respect to a local coordinate system such as UTM.  However, the CSM API requires that the ,  ,   coordinates of ground points be in the Earth Centered Earth Fixed (ECEF) Coordinate System.  Hence, for the remainder of this document the symbols ,  , and   refer to the “model” coordinates of points in the coordinate system of choice, e.g. UTM.  The coordinate values of these model points do not change; instead, corrections to adjustable parameters associated with them can take on non-zero values due to an adjustment.  Therefore, when the values of all adjustable parameters are uncorrected (zeros), the relationship between model space (x, y, z) and ground space (X, Y, Z) is simply a coordinate conversion from the associated local ground-based system to ECEF.  However, if the corrections to adjustable parameters have non-zero values, then the relationship between model-space and ground-space involves both a transformation of points based on the corrected adjustable parameters, and a subsequent coordinate conversion to ECEF.  More details on the GPM adjustable parameters are provided in Section 6.
To expand CSM to include point clouds, the addition of new methods and modifications to existing methods are required in the CSM API:  
•	computeSensorPartials – given a ground   point, calculate the partial derivatives of the  ,   and   model coordinates with respect to a designated sensor parameter.
•	modelToGround – given a set of model-point coordinates, apply adjusted sensor parameters resulting from a block adjustment or from calibration values to transform the  ,  ,   coordinates, and convert the results to  ,  ,   ground coordinates.  Optional error covariance for the model coordinates can be included as input, which will provide ground covariance information as additional output.  (Sensor parameter error covariance values are available to the model internally, so their effect will also be applied to the optional ground covariance calculation.).  Time can also to be passed into the function as an optional parameter in addition to the coordinates, alleviating the burden on the sensor model to determine the time based on the point coordinates.
•	groundToModel - given a set of ground-point coordinates as input, determine the associated model coordinates of the point.  If an optional ground covariance matrix is provided as input, then the sensor model will employ full covariance propagation of it and the associated sensor parameter covariance matrix to output a full error covariance matrix of the returned 3D coordinates of the model point.
•	computeGroundPartials – given  ,  ,   ground coordinates, returns partial derivatives of model coordinates with respect to geocentric ground coordinates, resulting in a total of nine partial derivatives.
•	getCrossCovarianceMatrix - given an instantiated collection unit (CU; see Section 6.1.1) containing u1 adjustable parameters and a specified second CU containing u2 adjustable parameters, return the u1 by u2 error cross-covariance matrix between the two CUs.
•	getModelCoordinateProperties – given an instantiated collection unit (CU), return a description of the model-space coordinate system (MCS) used by the sensor model.
•	getValidModelRange – given an instantiated collection unit, return the three dimensional model-space bounds representing the region over which the model is valid.
It is important to note that the functions above apply to both the Sensor-Space the Ground-Space implementations.  In both cases, there are model coordinates and ground coordinates. Also, adjustable parameters may be applied when transforming from model points to ground points and vice versa.  However, the adjustable parameters and how they are applied within the GPM vary between the implementations as described later in this document.

4.3	OVERVIEW OF USING GPM CSM FOR LIDAR

Point-cloud datasets can be categorized based on the source data, the processing method used to derive it, and the processing that has been applied to it.  Figure 4 - 2 shows one taxonomy for this type of categorization of lidar datasets.  Although Figure 4 - 2 focuses on lidar, the concepts could be applied to point clouds in general.  The components in Figure 4 - 2 are described as follows:
•	The blue boxes represent the processing levels of the point-cloud data.
o	L0 is the raw, off-the-platform data.
o	L1 is the initially-generated point cloud.
o	L2 is the noise-filtered L1 data.
o	L3 is the resulting point-cloud data after applying some type of data adjustment (an example of which is given in Section 5).
o	L4 is a derived product from the point-cloud data.
•	The yellow ovals indicate the processing that could take place between the levels.
CSM and GPM are utilized on the levels past the initial L0 to L1 processing that have a CSM class object (i.e. instantiation of the sensor model plug-in) associated with them.  It is important to note that a single CSM object can be used at multiple processing levels, as shown in Figure 4 - 2 as the green diamond.  For example, a point-cloud CSM object can be used in both the data adjustment (block adjustment) and in product generation (geopositioning scenario).
 
Figure 4 - 2  Lidar Processing Levels and Relationship to CSM.
 

5	USE OF CSM / GPM FUNCTION CALLS DURING EXPLOITATION

This section is provided for developers and users of exploitation tools (e.g. a sensor exploitation tool (SET) and lidar exploitation tool (LET)), and provides the algorithms for mensuration, geolocation, and adjustment as a function of CSM API function calls documented in Section 4.  The SET does not need to know details about point-cloud sensor modeling and upstream processing since this concern is handled by the GPM CSM plug-in.  Therefore, this section provides the details of how to implement the CSM plug-in’s methods for the purpose of exploiting point-cloud datasets.  For additional syntax on calling CSM functions, refer to the CSM TRD 3.0.2.  This section references mensuration error and unmodeled error, both of which are detailed in Sections 3 and 4.  For the rest of this section, it is assumed that a GPM Sensor-Space or Ground-Space model has already been instantiated by the SET/LET, via the GPM CSM plug-in.  When a GPM sensor model is instantiated, it is performed per Collection Unit (CU, see section 6.1.1).  Therefore, a single Sensor-Space GPM file may require multiple sensor models be instantiated if it contains multiple CUs.  For Ground-Space GPM, there will always be only one CU and thus one sensor model per file. 
5.1	ABSOLUTE ERROR AT A POINT
In order to obtain the estimated absolute accuracy at a point, all that is needed is a call to modelToGround(), passing in the   coordinates of the point of interest, as well as the mensuration error covariance values of the point.  The function returns the predicted absolute ground covariance of the point, and its updated   coordinates resulting from any transformation based on data adjustment and subsequent conversion to ECEF.  The predicted absolute ground covariance is used to calculate the CE90 associated with the predicted Absolute Horizontal Accuracy, the LE90 associated with the predicted Absolute Vertical Accuracy, or other related error metrics using well-defined equations (e.g. from MIL-STD-600001 [16]) for these metrics.

5.2	RELATIVE ERROR BETWEEN POINTS
Calculating relative accuracy between points requires knowledge of the absolute accuracy at each point of interest, as well as the error correlation between the points, in order to generate a full ground covariance matrix among all the points of interest.  Since modelToGround() solves for one point at a time, it cannot provide the ground cross covariance necessary for this full covariance matrix.  Therefore, one must build the components necessary to calculate, via Equation 5-1, the full ground covariance matrix,  , using multiple calls to several CSM functions.  The steps necessary to build these components are described in this subsection.  It is assumed that there are n points for which ground covariance is generated for   ( ).
 
Equation 5 - 1  Full ground covariance matrix.

The   matrix ( ) is the mensuration error covariance of the n input points provided by the user.
The   matrix ( ) is the unmodeled error of the n input points.  This is generated using n calls to getUnmodeledError() for each of the input points, providing the block diagonal portion of the matrix.  The off-diagonal portion is generated using multiple calls to getUnmodeledCrossCovariance() for each of the possible pairs of input points.
The   matrix ( ) is the adjustable parameter covariance, where p is the number of adjustable parameters.  These adjustable parameter covariance values are obtained from multiple calls to getCurrentParameterCovariance(), and the cross-covariance values are obtained from multiple calls to getCurrentCrossCovarianceMatrix().  This matrix is illustrated in Equation 5-2.

 
Equation 5 - 2  Matrix of adjustable parameter covariance.

The number of adjustable parameters p is obtained from getNumParameters().  The   matrix ( ) contains the partial derivatives of the model points with respect to the adjustable parameters, and is generated using multiple calls to computeSensorPartials() for each adjustable parameter a (where a varies from 1 to p).  This matrix is illustrated in Equation 5-3, and its individual components are shown in Equation 5-4.
 
Equation 5 - 3  Matrix of partial derivatives with respect to the adjustable parameters.
 
Equation 5 - 4  Components of the matrix of partial derivatives with respect to the adjustable parameters.

The   matrix ( ) contains the partial derivatives of the model points with respect to the ground points, and is generated using multiple calls to computeGroundPartials().  This matrix is illustrated in Equation 5-5, and its individual components are shown in Equation 5-6.
 
Equation 5 - 5 Matrix of partial derivatives with respect to the ground coordinates.
 
Equation 5 - 6 Components of the matrix of partial derivatives with respect to the ground coordinates.
After applying Equation 5-1,   takes on the form shown in Equation 5-7.  The solution for the   matrix ( ) can be used to calculate the relative accuracy between any pair of points used to develop the matrix.  For points i and j in  , their relative accuracy may be calculated using Equation 5-8.
 
Equation 5 - 7 Full Covariance Matrix among n Points.

 
Equation 5 - 8 Relative Error Covariance Matrix Between Two Points.

As with the absolute accuracy computation, CE90, LE90 and other related error metrics can be calculated using the relative error covariance matrix.
It is important to note that GPM follows the conventions of CSM and as such, the ground covariance ( ) in Equation 5-1 is in the ECEF coordinate system.  For some applications, it may be necessary to have the covariance in a local ENU system.  In these cases,   would need to be transformed into the ENU system.  In Equation 5-1 the pre and post multiplication by B-inverse (and its transpose, respectively) is basically this coordinate transform.  If the MCS is an ENU system, then the covariance in the ENU system can be computed directly (without the Jacobians and inverses required in Equation 5-1) as:
 
Equation 5 - 9 Computing an Error Covariance in the ENU system when the MCS system is ENU.

5.3	MULTI-IMAGE GEOPOSITIONING (MIG)

Multi-Image Geopositioning (MIG) allows one to solve for the best estimate of coordinates for a ground point, given multiple instances of that point being observed from different datasets.  It also provides a best estimate for the ground covariance of the point of interest.  For Sensor-Space datasets, the solution comes from a multi-ray intersection of lidar LOS vectors and associated range spheres.  In Ground-Space the solution is generated from a weighted average of input coordinates from multiple datasets.  This section demonstrates how to perform a MIG regardless of the GPM implementation.
The fundamental condition equations for a MIG are shown in Equation 5-10.  In this description, i = 1 to m, where m is the number of datasets, and j = 1 to n, where n is the number of points of interest for which a MIG is performed.  More information on the groundToModel function is provided in section 6.1.7.  For this example, it is assumed that each point of interest is visible in every dataset.  Although   will equal 1 when there is only a single point of interest, it is possible to perform a MIG on multiple points simultaneously.  The vector   is a set of model point coordinates for a selected point of interest   in dataset   and the vector    is the associated set of ground point coordinates for which a solution is obtained.
 
Equation 5 – 10 MIG Condition Equations.
These equations can be used in a least-squares solution to solve for the   ground point coordinates.  The linearized version of the condition equations are shown in Equation 5-11, where   contains the partial derivatives of F with respect to the GPM adjustable parameters,   contains the partial derivatives of F with respect to the ground coordinates, f is the misclosure vector, v is the residuals vector and ∆ is the vector of corrections to the estimates of the ground coordinates.  An iterative solution is needed, where the ground point coordinates are updated after each iteration using the solved values from the vector of corrections ∆.
 
Equation 5 – 11  MIG Linearized Condition Equations.
In order to develop the   matrix, calls to getNumParameters() are necessary to obtain the number of adjustable parameters for each dataset.  Then for each model point, a separate call to computeSensorPartials() is made for each adjustable parameter,  .  The   matrix takes the form shown in Equation 5-12, where each partial derivative entry corresponds to a separate call to computeSensorPartials(), and p is the number of adjustable parameters per dataset.  Note for this example, it is assumed that each dataset has the same number of adjustable parameters.
 
Equation 5 – 12  Matrix of partial derivatives with respect to the adjustable parameters.
In Equation 5-12:
 
and the   symbols correspond to the appropriately dimensioned zero matrices.
The   matrix, shown in Equation 5-13, is populated similarly to the   matrix, but with each partial derivative determined by a call to computeGroundPartials().
In order to solve the linearized MIG condition equations (Equation 5 - 4), the set of normal equations are used, shown in Equation 5-14.  The matrix   is the adjustable parameter covariance matrix, shown in Equation 5-15.  These adjustable parameter covariance values are obtained from multiple calls to getCurrentParameterCovariance()and the cross-covariance is obtained from getCurrentCrossCovarianceMatrix().
 
Equation 5 – 13  Matrix of partial derivatives with respect to the ground coordinates.
In Equation 5-13:
 
and the indexing is the same as for Equation 5-12.
 
Equation 5 – 14  Normal equations of linearized MIG condition equations.
 
Equation 5 - 15  A priori covariance matrix of the adjustable parameters, for m datasets with p adjustable parameters.
The MIG solution is obtained by applying the corrections (   ), a 3n × 1 matrix, obtained from the solution of the normal equations (Equation 5-14), to the initial point estimates, as shown in Equation 5-16,  where  contains the initial/current estimated ground coordinates and  contains the updated coordinates.
 
Equation 5 - 16  Calculation of MIG solution.
The ground-coordinate covariance matrix of the points of interest is obtained using Equation 5-17.

 
Equation 5 - 17  Covariance matrix of MIG solution points.

5.4	GENERAL DATA ADJUSTMENT

The CSM functions provide the flexibility to perform rigorous adjustments of point-cloud data, resulting in spatially aligned datasets, updated adjustable parameters and (typically) improved ground covariance values.  The adjustment process is not dependent upon which implementation of GPM (Sensor-Space or Ground-Space) is present in the datasets.  This section demonstrates a method of performing a data adjustment using the proposed CSM functions.  It is assumed that the user has a set of tie points (and associated uncertainties) measured in overlap areas among the multiple datasets.
The fundamental condition equations for an adjustment are represented by Equation 5-18.  The CSM function groundToModel() uses estimates of the unknown ground point coordinates    as input and returns model coordinates for those points.  The vector   consists of the measured model coordinates for the tie points.
 
Equation 5 - 18  Tie Points Condition Equation.
For this description, assume that there are a total of m point-cloud datasets (i=1 to m), p adjustable parameters per dataset (obtained from a CSM call to getNumParameters()) and n points (j=1 to n) that are observable once in each of the point-cloud datasets.   To solve the data adjustment, first the partial derivative matrices are developed.  The partial derivatives of the tie point condition equation with respect to the adjustable parameters (Equation 5-19) is populated using multiple calls to the CSM function computeSensorPartials().  In Equation 5-19,   is the vector of adjustable parameters associated with dataset  .  The partial derivatives with respect to ground coordinates (Equation 5-20) is populated using multiple calls to the CSM function computeGroundPartials().  
 
Equation 5 - 19  Partial Derivatives with Respect to the Adjustable Parameters.
 
Equation 5 - 20  Partial Derivatives with Respect to Ground Coordinates.
The linearized form of the condition equations is shown in Equation 5-21.  Here,   is the vector of differences between measured and computed (via groundToModel()) tie point coordinates, and   is the residual vector.  The vectors   and  , are the corrections to be applied to the   adjustable parameters and 3  ground coordinates of points, respectively.
 
Equation 5 - 21  Linearized form of condition equations.
In addition to the B matrices and the f vector, an input covariance matrix   (Equation 5-22) must be developed that reflects a   covariance matrix for the measurement of each individual tie point.
 
Equation 5 - 22  Input Covariance Matrix for tie points.
Also needed is an a priori covariance matrix for the adjustable parameters, given in Equation 5-23.  This matrix is populated using multiple calls to the CSM function getCurrentParameterCovariance() and the cross-covariance is obtained from getCurrentCrossCovarianceMatrix().
 
Equation 5 - 23  A priori covariance matrix for the adjustable parameters.
Using the partial derivative matrices, the   vector, and the covariance matrix for the tie points, the normal equations can be formed as shown in Equation 5-24.  The a priori weight matrix for the adjustable parameters is set to the inverse of the a priori adjustable parameter covariance matrix (  ).  The a priori weight matrix for the ground coordinates, , is the inverse of the full a priori covariance matrix for ground coordinates,  .  The associated variances and covariances (including cross-covariances between points) for observed ground coordinates, such as those from surveyed control points or mensurated from an independent reference dataset, are included in  .  For points with no a priori ground coordinate observations, such as tiepoints not associated with a surveyed control point, the diagonal elements of   are set to very large  values and all entries along the associated rows and columns are set to zero. The variables   and    are initialized to zeros, then updated each iteration with the solved corrections to the adjustable parameters   and the corrections to the ground coordinates  , respectively.
 
Equation 5 - 24  Expanded Normal Equations.
Substituting for expanded normal equations with traditional symbols results in Equation 5-25.
 
Equation 5 - 25  Substituted Normal Equations.
Using these normal equations, an iterative process is used to solve for the final updates to the adjustable parameters and the ground coordinates.  In each iteration, updates to the adjustable parameters  and updates to the ground coordinates   are applied as shown in Equation 5-26, where   contains the initial/current approximations of the adjustable parameters, and   contains the initial/current estimate of the ground coordinates of tie points (and any observed control points).
 
Equation 5 - 26  Updates to Adjustable Parameters and Ground Coordinates.
These steps of calculating updates and computing updated parameters are repeated until convergence is reached.  The covariance of the adjustable parameters is obtained as shown in Equation 5-27, and the covariance matrix for computed ground point coordinates is shown in Equation 5-28.
 
Equation 5 - 27  a posteriori covariance of adjustable parameters.

 
Equation 5 - 28  a posteriori covariance of computed ground point coordinates.
 
6	GPM FOR SENSOR MODEL PLUG-IN BUILDERS

The section above described the use of CSM function calls in conjunction with GPM data to exploit the data for geopositioning and data adjustment operations.  This required a working knowledge of CSM, but did not require detailed knowledge of GPM.  This section begins with some general considerations for GPM adjustable parameters and then provides detailed insight into Sensor-Space (6.1) and Ground-Space (6.2) GPM, as required by sensor model plug-in builders that develop the CSM functions.
Before addressing the details of Sensor-Space and Ground-Space GPM, note that in either case adjustable parameters and their values are stored in the support data and can be non-zero.  If non-zero, they have not been applied to the points in the dataset and should be utilized during subsequent exploitation with the GPM model.  Once the parameters are applied to the points, then the flag is reset to zero.  Of course, when a vendor initially generates GPM they set the values of the adjustable parameters to zero.  See Section 7, particularly the discussion referencing Figure 7 - 5 and Figure 7 - 7 for details to handle potentially non-zero adjustable parameter values.
6.1	SENSOR-SPACE GPM

This subsection describes the Sensor-Space GPM model.  As mentioned in Section 1, this instantiation of GPM uses a generic physical sensor model that resembles the physics of the lidar data collection, but excludes some sensor-specific detail.  This model also employs the coordinate systems described in Section 3.3.
The following subsections describe Sensor-Space GPM concepts, including Collection Units, Posts, Correlation Groups, GPM metadata formats, the projective model, the stochastic/adjustment model, exploitation functions, and conversion between different covariance metadata formats.

6.1.1	COLLECTION UNITS 

A lidar dataset can usually be represented by a number of collection units (CUs), with each of these units representing an area in which the data was collected using a constant set of collection parameters and with consistent collection geometry, resulting in data with homogeneous uncertainties.  A pass, or strip, within a collection (during which only a repeated pattern of sensor pointing occurs) is a good example of a CU.  For a CU collected over a short period of time with minimal aircraft dynamics, it is reasonable to assume that the sensor component errors (e.g. GPS, IMU) within the CU vary so slightly that only a small set of CU-wide sensor adjustable parameters (e.g. one constant and one rate per sensor component) are needed to capture the majority of the sensor errors for the entire CU.  The same assumption can be made for the GPM adjustable parameters.  Therefore, in this situation, any lidar point collected in a CU could be rigorously adjusted using a single set of CU-wide GPM adjustable parameters.  Sensor-Space GPM CU parameters may be represented by both constant and rate parameters, allowing for first-order polynomial parameter modeling.


6.1.2	POSTS

Now assume a different CU for which the sensor errors vary throughout (perhaps due to a longer collection time or greater aircraft dynamics).  In this situation, one set of CU-wide sensor adjustable parameters, or one set of GPM adjustable parameters, may not be sufficient to capture the higher-frequency errors for the entire CU.  However, breaking the CU into separate CUs is not appropriate since the CU represents a single collection event.  In this case, a set of CU-wide sensor adjustable parameters combined with multiple sets of sub-CU adjustable parameters, distributed throughout the CU by time and associated with unique timestamps, could be applied.  Then, the higher-frequency errors not captured by the CU-wide adjustable parameters for any lidar point collected in this CU could be modeled by interpolating between sub-CU adjustable parameters, allowing the adjustments applied per point to change continuously throughout the CU.  The application of this set of adjustable parameters, and the propagation of its associated set of estimated error covariances, would be used in conjunction with the CU parameters and CU covariance to rigorously adjust and determine the predicted accuracy of the lidar point.  These sets of sub-CU adjustable parameters and associated covariances are defined as posts.
Figure 6 – 1 illustrates the posts concept for several passes of a lidar collection.  Note in the figure that the posts are located along the trajectories of the passes.  Since the timestamp for each post also has an associated sensor position, placing the posts in the sensor positions is convenient for illustration.  This is not to imply that posts only apply to lidar data closest in distance to the post.  Posts are associated with a particular epoch in time, and a post’s information will have its greatest effect on lidar data with associated timestamps close to that of the post itself.

6.1.3	CORRELATION GROUPS

The covariance of the Sensor-Space GPM adjustable parameters, including parameters associated with CUs and/or posts, can be stored using one of two methods.  The first method, called direct storage, stores the entire full covariance matrix for all the CU and post parameters, including all cross-covariances among the parameters.  The second method, called indirect storage, stores only the block covariances along the diagonal of the full covariance matrix, and models the cross-correlations needed to form the full covariance matrix.  
Not all possible cross-covariances are modeled when using indirect covariance storage.  Parameters that have significant within-CU or within-post covariances are grouped together into what are called correlation groups [17].   Every parameter is in one and only one correlation group.  All of the parameters within a correlation group share the same model to describe the reduction in correlation as a function of separation (time or distance).   Covariances within a CU or post (and therefore cross-covariances among separate CUs or posts) are non-zero only between parameters within the same correlation group.  Since the true correlation reduction as a function of separation will differ for each parameter, fidelity is lost when using a single set of correlation model parameters for a correlation group.  If it is desired to maintain a higher-fidelity decorrelation 
 
Figure 6 - 1  Representation of posts within lidar passes.
function, it may be beneficial to group parameters with similar correlation functions, or keep a parameter in its own correlation group.  However, this sacrifices the within-CU covariance.     
For example, suppose for each post,   and   exhibit significant correlation only with each other, and   does not have a significant correlation with any of the other parameters. The resulting estimated within-post covariance matrix would appear for these parameters as:

 
and the estimated cross-covariance matrix of this post  , and another post,   would appear as:
 .
Since the covariances between   and the other parameters are close to zero, they are stored as zero (TBR) , and similarly the cross-covariance terms are set to zero when constructing the full covariance matrix.  Thus,   and   would be included in one correlation group (CG1), and   would be considered the only element in a second correlation group (CG2).
Only one set of correlation function parameters (See Section 3.2.1) is used for an entire correlation group, rather than a separate set per parameter within the group.  After a data adjustment, it is possible that most or all adjusted parameters will be significantly correlated. In this case, direct covariance storage should be used if it is desired to carry these correlations since there are no correlation restrictions among parameters in that method.  That is, correlation groups only apply to indirect covariance storage.  
Using the above example, assume a set of correlation function parameters for CG1 ( , )1, a set of like parameters for CG2 ( , )2, and the time difference between posts   and  is  .  Using the correlation function in Equation 3-1 one could calculate associated correlation coefficients for CG1 and CG2 between posts   and , named   and  .  Then the calculation of the estimated cross-covariance matrix between posts   and  would be
 

6.1.4	COVARIANCE METADATA FORMATS

The Sensor-Space GPM covariance metadata can be represented in two general formats, namely the Data Stream Format and the Parameter Format.  The Data Stream Format stores the Sensor-Space GPM covariance metadata  (for position, attitude and possibly range) at the same rate as the input metadata (Section 7) used to generate GPM.  The input metadata is typically the result of a filtering process applied to sensor metadata (e.g. GPS/IMU) which operates at a high frequency.  During Sensor-Space GPM generation, each of these input covariance metadata events are converted into GPM covariance metadata events (designated as posts), resulting in a stream of GPM covariance metadata at the same rate as the input covariance metadata.  The uncertainties stored by the Data Stream Format are as follows:
•	For each data stream post, a   covariance matrix representing uncertainties in the Path Coordinate System of the following data:
o	 ,  ,  : positional offsets 
o	 ,  ,  : angular offsets 
o	 : range offset 
•	One   covariance matrix representing uncertainties in the Model Coordinate System of positional offsets  ,  ,   for the entire dataset.
For general exploitation of GPM datasets, the high-frequency covariance metadata found in the Data Stream Format is unnecessary since the parameter errors are highly correlated, and the covariances do not change significantly when sampled at such a high rate; therefore much of it may be redundant and not beneficial to downstream processing.  Additionally, it cannot be efficiently instantiated within CSM using the current CSM paradigm of loading all of the “image” metadata at once, while not interfacing with the actual data.  The Parameter Format addresses this issue by consolidating the Data Stream covariances into a condensed format for both exploitation and storage, using a flexible set of adjustable parameters to represent the GPM covariance values.  The Parameter Format consists of one of the following options:
Option 1:  Polynomials
•	Each Collection Unit (CU)  , consists of:
o	A representative timestamp for the entire CU.
o	Some combination of the following adjustable parameters defined in the Model-space Coordinate System (MCS) and the Path Coordinate System (PCS):
	MCS parameters:   ,  ,  : positional offset adjustable parameters  for the entire CU in the MCS.
	PCS parameters:
•	 ,  ,  : positional offset constants for the entire CU 
•	 ,  ,  : angular offset constants for the entire CU
•	 : range offset constant for the entire CU
•	 ,  ,  : positional offset rates for the entire CU 
•	 ,  ,  : angular offset rates for the entire CU
•	 : range offset rate for the entire CU
•	The full covariance matrices of all the adjustable parameters for each CU, partitioned into correlation groups, are stored allowing for correlations to exist for these parameters across different CUs.
•	The positional offset adjustable parameters ( ,  ,  ) in the MCS are modeled per CU, however minimal variation is expected in these values among the CUs from a given collection or adjusted as a single unit.  It is recommended that very high (e.g. > 0.9) correlation coefficients are used for these parameters for modeling their correlation between CUs.
•	For indirect storage of covariance (see Appendix D), the MCS parameters cannot be correlated to the PCS parameters; and the PCS constant parameters cannot be correlated to the PCS rate parameters.  If, after data adjustment, correlations among these three groups are to be modeled, then direct storage of covariance must be used.

Option 2: Posts
•	Discrete characterizations of covariance events (i.e. posts) at specified epochs (generally at a lower frequency than the Data Stream) along the entirety of each CU. Each post,  , consists of:
o	A timestamp
o	Some combination of the following adjustable parameters:
	 : positional offsets
	 : angular offsets 
	 : range offset 
•	The full covariance matrices of all the post adjustable parameters for each CU, partitioned into correlation groups.  For indirect covariance storage, correlations are permitted among the posts within a CU, but not across different CUs.  If, after adjustment, correlations between posts in different CUs are to be modeled, direct storage must be used.



Option 3:  Combination of Polynomials and Posts.
•	The dataset is divided into a series of CU’s and each CU has associated parameters as outlined in Option 1.
•	Each CU is divided into a series of posts and each post has adjustable parameters as outlined in Option 2.
•	The adjustment applied to a point and the covariance associated with a point are based on a combination of both CU parameters and post parameters.
•	When both polynomials and posts are implemented, the rules regarding correlations in Options 1 and 2 must be followed.  In addition, for indirect covariance storage, correlations between post parameters and polynomial parameters are not allowed.  If, after adjustment, correlations between posts, CU constants, and CU rates are to be modeled, direct storage must be used.

The Parameter Format gives one the flexibility to choose which adjustable parameters, and associated covariances, to carry in the metadata.  For example, one may implement Option 3 using position, angle and range parameters for the CU polynomials (offsets and rates), and perhaps just angle parameters for the posts to capture any residual angular variation in the data not captured in the CU polynomial parameters.
When GPM is initially generated (Section 7), the resulting GPM covariance metadata will either be in the Data Stream Format or the Parameter Format.  However, for CSM exploitation, the Parameter Format is required.  Therefore, if a GPM dataset in Data Stream Format is to be used in the CSM API, it must be converted to the Parameter Format by the sensor model plug-in upon instantiation within CSM.  A method to perform this conversion is provided in Section 6.1.8.
Sections 6.1.5 through 6.1.7 assume the GPM metadata is in Parameter Format.

6.1.5	PROJECTIVE MODEL

The Sensor-Space GPM projective model provides the mathematical relationships among the key components of the Sensor-Space GPM point cloud.  Specifically, it describes the relationships among the range, the sensor position and angular attitude, and the ground point.  The projective model is shown in Equation 6 - 1.
 
Equation 6 - 1  Sensor-Space GPM Projective Model.
In this model,   represents a point in the point cloud in the Model-space Coordinate System (MCS).  The sensor position, again in the MCS, is represented by  .  The rotation from the Ray Coordinate System (RCS) to the MCS is represented by  .   Finally, the vector   represents the range vector from the sensor to the ground point in the RCS.  
The  rotation matrix is actually defined by two other rotation matrices, the rotation from the RCS to the Path Coordinate System (PCS),  , and the rotation from the PCS to the MCS,  .   This relationship—shown in Equation 6 – 2 —becomes important when defining the adjustment model.
 
Equation 6 - 2  Subcomponents of the rotation from the RCS to the MCS.

6.1.6	STOCHASTIC/ADJUSTMENT MODEL

The Sensor-Space GPM Stochastic/Adjustment Model is a modification of the GPM Projective Model which designates the adjustable GPM parameters having probabilistic (stochastic) properties associated with them.  This model is necessary for both error propagation and data adjustment.  In order to form the Stochastic/Adjustment Model, the GPM Projective Model (Equation 6 - 1) is expanded to include a series of adjustable parameters, all of which have initial values of zero.  The Stochastic/Adjustment Model is detailed in Equation 6 - 3.
 
Equation 6 - 3 Sensor-space GPM Adjustment / Stochastic Model.
For Sensor-space GPM, three distinct, and seven aggregate adjustable parameters have been identified.  First, there are three distinct coordinate translations defined ( ,  ,   which provide adjustments to the sensor position in the MCS.  The aggregate adjustable parameters include three translations   which provide adjustments to the sensor position in the PCS, a range bias ( , and three rotation parameters represented by the combined adjustment rotation matrix,  , above.  As shown in Equation 6 - 4,   is actually composed of small angle rotations about the XP, YP and ZP axes ( ,  respectively  of the PCS. 
 
Where:
  
Equation 6 - 4   Rotation Adjustable Parameters.
When expanded, the GPM Stochastic/Adjustment model appears as follows:
 
Equation 6 - 5  Sensor-space GPM Stochastic Model with Adjustment Parameters Expanded.
With the exception of the MCS coordinate translation parameters , the adjustable parameters in Equation 6 - 5 consist of multiple contributors depending on which option of the Parameter Format (Section 6.1.3) is implemented.  Thus, the true adjustable parameters are the contributors to the parameters shown in Equation 6 - 5.  That is, a GPM adjustment consists of solving for corrections to these component parameters rather than their aggregate values.  Equation 6 - 6 provides all the possible contributors for each of the aggregate adjustable parameters.  In practice some subset of these contributors may be used.  The contributions from posts (e.g.   ) are values of interpolated post adjustable parameters based on the timestamp of the model point (See Appendix B).  Note that these contributions each consist of two adjustable parameters—one for each of the adjacent posts from which they were interpolated.    is a normalized time difference between the model point’s timestamp (either from the point record or interpolated from the Time Reference Grid),  , and the reference timestamp for the CU,  . The reference timestamp is defined as   where,   and   are based on the start and end time of the covariance record.  Thus,  .
 
 
 
 
 
 
 
Equation 6 - 6  Contributions to Adjustment Parameters.

It is important to note that if an adjustment is applied (Section 5, Equation 5 - 26) to a Sensor-Space GPM dataset, and that dataset will remain in the Sensor-Space implementation, then the trajectory data must be updated using the solved MCS translation parameters  , and the aggregate PCS translation parameters  .  The updated trajectory values are calculated using Equation 6-7.
 
Equation 6 - 7  Updating trajectory values post-adjustment.

6.1.7	EXPLOITATION OF SENSOR-SPACE GPM 

To this point, the basic Sensor-Space GPM concept has been presented.   This section builds upon what has been discussed and illustrates how Sensor-Space GPM datasets are exploited.  It starts with  fundamental concepts of Sensor-Space GPM, and then continues with the computations necessary to write foundational CSM functions for exploiting GPM, including modelToGround(), groundToModel(), computeSensorPartials() and computeGroundPartials(). 

6.1.7.1	Fundamental Concepts in Sensor-Space GPM Exploitation

Before explaining the details of exploiting Sensor-Space GPM, there are some fundamental concepts related to GPM that must be discussed.  The first of these is a description of what actually happens when one mensurates a point.  This process is illustrated at a high level in Figure 6 - 2.

 
Figure 6 - 2  Sensor-Space GPM Mensuration of a single point.
Once a point of interest is selected, a timestamp associated with that point must be established.  If the point of interest happens to be an actual point stored in the point cloud, the time may be retrieved directly if time is stored as an additional attribute with the point records. If the point of interest is not an exact point stored in the file, but the point-cloud file stores timestamps per point record; a time is interpolated for the point based on a three-dimensional nearest-neighbor interpolation from the point of interest to the point-cloud points.   This determination of point time from the point cloud could be performed by the SET and passed to the sensor model as a parameter or the interpolation could be performed by the sensor model based on the point’s coordinates.  As an alternative, if times are not stored with the point records but a Time Reference Grid is stored for the collection unit, a time is interpolated for the point of interest from the Time Reference Grid based on three-dimensional nearest-neighbor interpolation to the posts of the reference grid.  It is important to note that if times are stored per point record and a Time Reference Grid exists for the CU, the time interpolated from the reference grid should be used for related GPM operations.
After a time is determined for the point of interest, the approximate sensor location at the time the point was collected can be re-established based on linear interpolation from the trajectory associated with that CU. Once both the coordinates for the sensor location and the point of interest (in the MCS) are known, the range vector from the sensor to the point of interest can be established. Finally, the PCS and RCS coordinate systems as defined in Section 3 can be established.   
The values obtained from the process shown in Figure 6 – 2 are used within several CSM functions to assist in the exploitation of the dataset.  For example, the modelToGround() function uses the interpolated sensor position, calculated range and rotations  to develop a refined coordinate for the point of interest by applying the GPM adjustable sensor parameters to the original point cloud (the model). The function also calculates a ground covariance for the point of interest.  The calculations necessary to write modelToGround() and other CSM functions for Sensor-Space GPM are described in the following subsections.
6.1.7.2	modelToGround()

Definition:  given one model point, apply the GPM adjustable parameters to the point to transform  ,  ,   model coordinates (MCS) and convert the result to ECEF  ,  ,   ground coordinates.  Optional error covariance for the model coordinates (e.g. mensuration error) can be included as input, which will provide ground covariance information as additional output.  The time associated with the point (Point Time) can also be passed into this function as an optional parameter from the exploitation tool, alleviating the need for the sensor model to determine a point time from interpolation in the point cloud or the time grid.

Input:
•	 ,  ,   model point coordinates
•	Optional:  error covariance matrix of the model point
•	Optional: point time

Output:
•	 ,  ,   ground point coordinates
•	Optional:  error covariance matrix of the ground point

Note:  the user will provide the model point, and optionally the associated error covariance, but the GPM adjustable parameters and associated covariance information are handled internally to the sensor model plug-in.  Also, the timestamp associated with the input  ,  ,   model point coordinates is not an input parameter.  Therefore its value is obtained using one of two methods.  If time is stored as a per point attribute in the input file, a timestamp may be retrieved by searching the dataset for the point with coordinates closest to the input  ,  ,   model-point coordinates based on three-dimensional distance and using its associated timestamp.  If instead a Time Reference Grid is stored as additional metadata in the file, then a time for the point is established by searching the Time Reference Grid for the post with coordinates closest to the input  ,  ,   model-point coordinates and using the time associated with that post.  If time is a per-point attribute in the CU and a Time Reference Grid is associated with the CU, the time interpolated from the Time Reference Grid should be used in GPM operations.
The modelToGround() function is simply an application of the GPM adjustment model (Equation 6-5) followed by a coordinate conversion to ECEF.  To begin, one first follows the flow in Figure 6 - 2, which provides the sensor position, the LOS, the range, and the definitions of the PCS and RCS.  Then Equation 6 - 5 is applied, providing updated model coordinates ( ,  ,  ) with any adjustable parameter values applied.  Any post adjustable parameters needed for Equation 6 - 5 are interpolated for the input model point using the method in Appendix B.  Finally, the updated model coordinates are converted from MCS to ECEF, resulting in the output ( ,  ,  ) ground-point coordinates.
The remainder of this subsection describes the calculations needed to obtain the optional covariance of the output ground point.  First, the covariance matrix   of the adjustable parameters is formed for all the parameters in the Parameter Format chosen for the dataset (Section 6.1.4).  An example   is provided in Equation 6 - 8, for an indirectly-stored dataset using both polynomial and post adjustable parameters, consisting of two CUs, with the first CU having   posts and the second CU having   posts.  Note that the matrices in Equations 6-8 and 6-9 would be full when using direct storage, although the rest of the equations in this subsection would still be valid as shown.

 
Equation 6 - 8  Example Adjustable Parameter Covariance Matrix.

For further description, one of the component submatrices within   is detailed in Equation 6 - 9.  Here,   is the CU adjustable parameter covariance matrix for the first CU.  In this example, the CU adjustable parameters are offsets ( ) and rates ( ).  There are three correlation groups, the first one containing ( ), the next one containing ( ),  and the third one having only  .  Note that correlations only exist within each correlation group, and that this defines which of the associated cross-covariance terms can be nonzero (e.g. in  ,   can be nonzero, but   cannot).
The next step in calculating the output ground covariance is to generate the partial derivatives of the model coordinates with respect to the adjustable parameters.  This matrix ( ) is obtained from calls to computeSensorPartials(), which is described in subsection 6.1.7.4. An example   matrix is shown in Equation 6 - 10.  In this example, the CU adjustable parameters are the same as those used in the previous   example.  The post adjustable parameters consist of   and  , and there are   posts for the first CU and   posts for the second CU.  The subscript i is an index for the CUs, and j is an index for the posts.  Note that for a given model point of interest, many of these partial derivative entries would have a value of zero.
 
Equation 6 - 9  Example CU Parameter Covariance Matrix.

 
where
 
and
 
Equation 6 - 10  Partial Derivatives of Model Coordinates with Respect to the Adjustable Parameters.
The matrix of partial derivatives (B) of the model-space coordinates with respect to the ground-space coordinates is shown in Equation 6 –11.  In the case of LSR MCS systems, this is equivalent to the rotation matrix used in the conversion from the MCS to the ECEF coordinate system.  This matrix can be obtained with a call to computeGroundPartials() using the previously calculated ground  ,  ,   coordinates as input.

 
Equation 6 - 11  Partial Derivatives of Model Coordinates with Respect to Ground Coordinates.
The symmetric covariance matrix of the point coordinates is then computed as shown in Equation 6 - 12.  In the equation   is the mensuration error covariance matrix provided as input into modelToGround(), and   is the unmodeled error covariance matrix (Section 3.2.2).
 
Equation 6 - 12  A posteriori Ground Covariance Matrix at a Point.

6.1.7.3	groundToModel()

Definition:  given a ground-point’s coordinates as input, determine its associated model coordinates (MCS).  If an optional ground covariance matrix is provided as input, then the sensor model will employ full covariance propagation of it and the associated sensor parameter covariance matrix to output a full error covariance matrix of the returned 3D coordinates of the model point.
Input:
•	 ,  ,   ground-point coordinates
•	Optional:  error covariance matrix of the ground point

Output:
•	 ,  ,   model-point coordinates in the MCS
•	Optional:  error covariance matrix of the model point

Note:  the user will provide the ground point, and optionally the associated error covariance, but the GPM adjustable parameters and associated covariance information are handled internally to the sensor model plug-in.
The groundToModel() function uses an iterative solution to the GPM adjustment model (Equation 6-5), which is performed using repeated calls to modelToGround().  The input ground coordinates are converted from ECEF to MCS coordinates and used as the initial value for the model point.  At each iteration, the calculated value of  (converted to MCS) is added to the model point coordinates until convergence to some tolerance (TBD) is reached (Equation 6-13).

 
Equation 6 - 13  Iterative solution for groundToModel().
To calculate the optional covariance for the calculated model point coordinates, the sensor covariance   (Equation 6 - 8), the partial derivatives of the model coordinates with respect to the sensor parameters   (Equation 6 - 10), and the partial derivatives of the model coordinates with respect to the ground coordinates   (Equation 6 - 11) are obtained as with modelToGround().  The model point covariance is calculated as shown in Equation 6 - 14, where   is the input error covariance matrix in ground space.
 
Equation 6 - 14  A posteriori Model Covariance Matrix at a Point.

6.1.7.4	computeSensorPartials()

Definition:  given a ground   point and a designated sensor parameter, calculate the partial derivatives of the  ,   and   model coordinates with respect to the designated parameter.
Input:
•	 ,  ,   ground-point coordinates
•	Index of the designated sensor parameter S.

Output:
•	Partial derivatives of the  ,  ,   model-point coordinates with respect to the designated sensor parameter a.

Note:  the user will provide the ground point, but the GPM adjustable parameters are handled internally to the sensor model plug-in.
This function uses numerical partial derivatives.  Using the input  ,  ,   ground point coordinates, the computeSensorPartials() function first calculates the ( ,  ,  ) model point coordinates via a call to groundToModel().  The numerical partial derivatives of the model point with respect to the sensor parameter of interest,   are then calculated by
 
where   is the result from groundToModel() when perturbing the sensor parameter of interest,  , by  , and   is the result from groundToModel() when perturbing   by  .  To perturb the sensor parameter of interest, one must change its value using the CSM function setCurrentSensorParameter() before calling groundToModel(). The values of   are TBD.
6.1.7.5	computeGroundPartials()

Definition:  given ground   coordinates, returns partial derivatives of model coordinates with respect to geocentric ECEF ground coordinates, resulting in a total of nine partial derivatives.
Input:
•	 ,  ,   ground-point coordinates

Output:
•	Partial derivatives of the  ,  ,   model-point coordinates with respect to the ECEF ground coordinates.

This function uses numerical partial derivatives.  Using the input  ,  ,   ground point coordinates, the computeGroundPartials() function first calculates the ( ,  ,  ) model point coordinates via a call to groundToModel().  Next, the X ground point coordinate is perturbed by a small amount , and groundToModel() is called again using ( ,  ,  ), producing model coordinates  . This is also done using ( ,  ,  ), producing model coordinates  .  This process is repeated for the Y and Z ground point coordinates.  The   matrix of partial derivatives is calculated by
 
This matrix is equivalent to the rotation matrix used in the conversion from the ECEF to the MCS coordinate system.  As with computeSensorPartials(), the values of   are TBD.
6.1.7.6	getUnmodeledError()

Definition:  for a given data point, provide the unmodeled error covariance specific to that point.
Input:
•	 ,  ,   model-point coordinates

Output:
•	The estimated unmodeled error covariance at the  ,  ,   model-point coordinates.

The getUnmodeledError() function calculates a   unmodeled error covariance matrix for the input model-point coordinates, employing the unmodeled error model described in Section 3.2.2.  If only one unmodeled error covariance post is used in the model point’s dataset, then the covariance matrix associated with that post is returned.  If multiple unmodeled error covariance posts exist for the model point’s dataset, then nearest-neighbor interpolation is used to calculate the output unmodeled error matrix.
6.1.7.7	getUnmodeledCrossCovariance()

Definition:  for two specified data points, return the unmodeled error cross-covariance between the points.
Input:
•	Two sets of  ,  ,   model-point coordinates from two separate model points.

Output:
•	The estimated unmodeled error cross-covariance for the two model points.

The getUnmodeledCrossCovariance() function calculates a   unmodeled error cross-covariance matrix for the input model-point coordinates, employing the unmodeled error model described in Section 3.2.2 and using the 4-parameter correlation model from Section 3.2.1.  Section 3.2.2, including Equation 3-3 through Equation 3-5, describe how to calculate the   cross-covariance matrix returned by this function.

6.1.8	CONVERTING DATA STREAM FORMAT TO PARAMETER FORMAT

As described in Section 6.1.3, the Data Stream Format stores the GPM metadata (position, attitude and possibly range) at the same rate (e.g. 1 Hz) as the input metadata used to generate GPM.  However, the high-frequency covariance metadata found in the Data Stream Format is unnecessary since the covariance values do not change significantly at such a high rate, and adjustable parameters are not solved for at such a rate.  Also, CSM requires that the metadata be in the Parameter Format.  This subsection describes a method of converting Data Stream(DS) metadata to the Parameter Format.
The flexibility of the Parameter Format allows one to choose which adjustable parameters will be used in the CUs and/or posts to model the adjustability and covariance of the dataset.  In order to describe the conversion process, an example Data Stream, consisting of  ,  ,  ,  ,   per epoch, will be converted to an Option 3 Parameter Format.  Suppose the Data Stream can be divided into the following correlation groups based on the significance of covariance between parameters:
•	Data Stream parameters:
o	 ,  ,   – DS correlation group 1
o	 ,   – DS correlation group 2
o	  – DS correlation group 3

The Option 3 Parameter Format is defined as:
•	CU parameters (grouped by correlation groups):
o	 ,  ,   – CU correlation group 1
o	 ,   – CU correlation group 2
o	  – CU correlation group 3
o	 ,  ,   – CU correlation group 4
o	 ,  – CU correlation group 5
o	  – CU correlation group 6 
•	Post parameters:
o	 ,  – post correlation group 1

Note that the Parameter Format correlation groups must consist of constituent components of the Data Stream correlation groups (e.g.  CU parameters ,  ,  ,  , and post parameters  ,   each make up correlation groups since the Data Stream parameters  ,   are a correlation group).
For a given epoch within the Data Stream, its covariance values will be distributed among CU parameters and post parameters.  The covariance values for each DS correlation group are distributed among parameters using pre-determined multipliers (F-values) for each correlation group in the Parameter Format.  These multipliers indicate what percentage of Data Stream covariance is distributed between CU parameters (constants only, rates are handled separately) and post parameters.  For any input DS correlation group, the sum of its associated F-values (not including those associated with rates) must be unity.  Establishing appropriate predetermined F values for the various sensors and datasets is TBR.  For the current example, any given DS correlation group could be assigned to a CU correlation group or divided between two correlation groups (CU constant and post).
In the case of the Data Stream for this example, positional offset ( ,  ,  ) covariance values will only be assigned to the CU constants (i.e. F = 1.0).  The angular covariance values ( ,  ) will be divided between CU constants and posts.  The ( ) angular covariance values will only be assigned to the CU constants.
The nature of the rate parameters necessitates handling them as a special case.  For any point in a CU, the rate contribution to the total covariance will vary depending upon the time difference from the CU reference time (usually the time near the center of the CU).  Therefore, rate F-values are assigned a modest number (currently recommended < 0.25, TBR) in addition to the previously assigned F-values, which actually causes the sum of all the F-values associated with a Data Stream value to exceed unity.  However, the effect from this results in conservative (i.e. larger) estimates of covariance away from the reference time of a CU, which is a small cost when considering the benefits of having rate terms in a data adjustment.
Below is a summary of this distribution and associated F-values chosen for each correlation group in the current example.

•	Data Stream ( ,  ,  ) :  Fconst = 1.0, Frates = 0.2
•	Data Stream ( ,  ):  Fconst = 0.7, Frates = 0.2, Fposts = 0.3
•	Data Stream ( ):  Fconst = 1.0, Frates = 0.1

Now the parameter covariances for a given CU are generated.  First, a reference timestamp is determined for the CU.  The recommended method is to compute the temporal midpoint of the CU based on the start and stop times of the sensor covariance record (see Section 6.1.6).  Next, the CU parameter covariances are calculated for each correlation group.  CU correlation group 1, which contains three parameters, needs a   matrix to represent its constituents’ variances and covariances.  One method to obtain this matrix is to calculate the mean of all the ( ,  ,  ) variance and covariance values in the Data Stream (within the temporal bounds of the CU).    The best method to obtain this matrix in the future is TBR.  However, once obtained, the   matrix   is multiplied by its assigned F-value (Fconst = 1.0), resulting in a   covariance for CU correlation group 1.  A similar procedure is used for CU correlation group 4 (the positional rates) by multiplying   by its assigned F-value (Frates = 0.2).
The angular Data Stream values are handled the same way as the translation values in this example.  First, as with the ( ,  ,  ) values, calculate the mean of all the ( ,  ) variance and covariance values within the CU temporal bounds of the Data Stream, resulting in a  covariance matrix.  This  matrix is multiplied by the appropriate Data Stream F-value (Fconst = 0.7), as listed above, resulting in a   covariance for CU correlation group 2.  The   covariance for CU correlation group 5 is obtained similarly except with an F-value of Frates = 0.2.  The mean of all   variance values is computed to define the variance for CU correlation group 3.  This same   variance is then multiplied by the appropriate F value (Frates = 0.1) to obtain the variance associated with CU correlation group 6.
Finally, the parameter covariances for the posts within a CU are generated.  When implementing posts, two must be generated at the temporal bounds of the CU, and any remaining posts must fall within these bounds.  For more guidance on generating posts, refer to Section 7.  The covariance matrices for posts can be obtained by designating windows of Data Stream covariances, each of which are only associated with a single post.  The most intuitive designation scheme for this is to assign unique temporal regions (i.e. windows) of the CU’s Data Stream for each post.  The mean of the ( ,  ) variance and covariance values in each window results in a 2x2 matrix  , which is then multiplied by the appropriate F-value.  Repeating this for every post in the CU results in covariance matrices associated with post correlation group 1 for each post.  The best method for computing representative covariance values per post is still TBR.
Equation 6 - 15 illustrates the resulting covariance matrix for a given CU—including its   post covariances—as a function of the Data Stream correlation group covariances for the current example.  The sigmas (  along the diagonal of the right-hand-side (bottom) matrix in Equation 6 -15 are the covariance matrices associated with the Data Stream.


 
Equation 6 - 15  Resulting CU covariance (upper matrix) after conversion from Data Stream (lower matrix).

6.2	GROUND-SPACE GPM


The Ground-Space GPM can be applied whenever the complexity of the point-cloud collection and processing concept of operation precludes the straightforward definition of a sensor-space projective model.  Examples of this include point-cloud datasets created by combining multiple lidar scans with diverse geometry and point clouds derived from other modalities (i.e EO) where the Sensor-Space projective model does not apply.  The Ground-Space GPM is defined in one of the GPM supported 3D coordinate systems for the MCS, i.e. in the CSM model space.  It is important to note that the MCS coordinate system may not be the same coordinate system that is being utilized to store the points in the point clouds.  In Ground-Space GPM, the adjustable parameters are translations associated with the anchor point locations within the CU, and CU-wide three-dimensional conformal (3DC) transformation parameters (the definition of collection unit (CU) is the same here as it is in Sensor-Space GPM).  The full covariance matrix for the anchor points’ translations along with the 3DC transformation parameters are pre-computed and carried with the data either by directly storing the full covariance or by storing correlation functions in the indirect scenario.  As with Sensor-Space GPM, Ground-Space GPM can be used to perform essential geopositioning and error propagation operations via CSM function calls, and therefore enables higher-level exploitation such as data adjustment.  

6.2.1	ANCHOR POINT MODEL

Anchor points constitute a set of 3D locations with an associated full covariance matrix.  The core concepts are that an anchor point characterizes the error phenomena of the point cloud in its vicinity. The full anchor point covariance matrix characterizes the overall relationships between errors at locations and their associated covariances and correlations.  When only anchor points are implemented, the absolute uncertainty of any point and the relative uncertainty of any point pair can be reliably estimated by effectively interpolating between the anchor points.  Figure 6 – 3 is a graphical illustration of interpolated absolute (left) and relative uncertainty (right).  In the left figure, the colors of the anchor points represent the variance at their location and the colors across the dataset area represent the interpolated variance.  On the right, the anchor point colors represent the relative variance between them and the point located in the center, and the colors across the dataset represent the interpolated relative variance with respect to the center point, where the darker colors represent lower relative variance.   It should be mentioned that explicit interpolation between anchor point covariances does not actually occur.  Instead, arbitrary point covariances are found by error propagation based on model equations which use interpolation between the adjustable parameters. The anchor point adjustable parameters in the Ground-Space GPM are translations associated with anchor point locations.  A description of the recommended method for interpolation of these translations is given in Appendix B.  Anchor points should be distributed throughout a point cloud area in such a way that the interpolation can sufficiently capture error phenomena.  For details on developing anchor points, refer to Section 7.
  
Figure 6 - 3  Interpolation of Uncertainties using Anchor Points.
The full covariance matrix (“full” implies that off-diagonal block covariances are included) for anchor points is stored either directly, or by storing the constituent parameters needed to reconstruct it indirectly.  Either way, it can be retrieved from the GPM metadata using the structures described in Appendix E.  The full anchor point covariance matrix,  , has the form shown in Equation 6 - 16, where   is the number of anchor points.
 , where
 , and  
Equation 6 - 16  GPM Anchor Point Covariance Matrix.
While direct storage for Ground-Space GPM involves carrying the entire matrix   shown in Equation 6 - 16, indirect storage is implemented by storing only   for each anchor point, and reconstructing the full   using coefficients describing the correlation between errors associated with anchor points.  As with the Sensor-Space GPM implementation, the adjustable parameters are divided into correlation groups, with each group having its own correlation functions. Also as with Sensor-Space GPM, there is a tradeoff when grouping adjustable parameters based on within-anchor point covariance or based on similar spatial decorrelation.  The correlation model used is described in Section 3.2.1, and has three separate sets of correlation coefficients for components   and   per correlation group.  The correlation between the errors associated with two anchor points   and   is calculated using the product of these coefficients as shown in Equation 6 - 17.  The correlation coefficient for each correlation group   is applied to form their associated cross-covariance blocks  using Equation 6 - 18, thereby enabling the formation of the full covariance matrix, guaranteed symmetric and positive definite. The recommended method for computing the square root of a covariance matrix is given in Appendix C.  
 
Equation 6 - 17  Anchor Point Correlation Coefficient Calculation.
 
Equation 6 - 18  Indirect Storage Method for Obtaining Off-Diagonal Blocks of   
As an example, consider the case where ground-space covariances are divided by horizontal (correlation group 1) and vertical (correlation group 2) components.  Then, for each anchor point, there are two covariance matrix blocks as shown in Equation 6 - 19.
 
Equation 6 - 19  Example Ground-Space GPM Covariance Matrix Associated with an Anchor Point  
The cross-covariance matrix used to form part of the full covariance matrix between anchor points   and   is calculated as shown in Equation 6 - 20.
 
Equation 6 - 20  Example Ground-Space GPM Cross-Covariance Matrix Calculation for Anchor Points .
6.2.2	 3-D CONFORMAL (SEVEN PARAMETER) TRANSFORMATION MODEL

As with the sensor-space implementation, Ground-Space GPM can accommodate CU-wide transformation parameters.  For Ground-Space GPM, there can only be one CU per dataset. These adjustable parameters appear as a combination of the seven parameters associated with 3-dimensional conformal (3DC) coordinate transformation.  They can include up to three rotations ( ,  , and   used to form rotation matrix ), three translations ( ), and a single scale factor correction ( ), applied as shown in Equation 6-21 and illustrated in Figure 6-4.  In the figure, arbitrary distance   is included to illustrate the effect of the scale factor correction (which is negative in the figure). Note that, as with the coefficients in the sensor-space implementation of CU-wide polynomials, not all of the seven transformation parameters need to be included as adjustable parameters.  Those parameters that are not included as adjustable parameters are considered zero constants in the transformation model.

 
Where
 
and
 
Equation 6 – 21  3DC Coordinate Transformation Model.
 
Figure 6 - 4  Three-Dimensional Conformal Coordinate Transformation.
In Equation 6-21,   represents normalized and re-centered model-space coordinates prior to transformation.  These are formed via Equation 6-22, where   are the original model-space coordinates,   are the re-centering values, and   is a normalizing scale factor.  Note the analogy of this with the Sensor-Space GPM process of normalizing the timestamp and utilizing a reference time (Section 6.1.7).  The re-centering values are the coordinates of the centroid of the CU, and the scale factor is such that it normalizes all re-centered point coordinates with respect to the longest distance between points in the CU. All of these values are stored and carried in the GPM metadata.  After the transformation is applied, the result, , must be multiplied by  , and the re-centering offset must be removed by adding   to obtain the final adjusted coordinates  .  The full transformation equation is shown in Equation 6-23a.  Equation 6-23b is a simplified equivalent version, with an algebraic cancellation applied.
 
Equation 6 - 22  Normalized and Re-Centered Model Space Coordinates.
 
Equation 6 – 23a  Ground Space GPM 3DC Transformation.
 
Equation 6 – 23b  Simplified equivalent to Equation 6-23a.
The covariance matrix associated with the 3DC transformation adjustable parameters, for some CU, , can be formed as shown in Equation 6-24.  In this equation,  ,  , and   are sequential rotations about the re-centered model-space x, y, and z axes, respectively, and are those used to form   of Equation 6-21.  When not all of the 3DC transformation parameters are used, the covariance matrix will often consist of a subset of the appropriate elements of Equation 6-24, an example of which is given in subsection 6.2.4.1.
 
Equation 6 - 24  3DC Transformation Covariance Matrix for Some CU,  .
If from a sensor model implementation standpoint, it becomes advantageous to always include all seven 3DC parameters regardless of which parameters are actually set and stored in the metadata, the following guidance will be adhered to.  3DC parameters not being stored in the GPM metadata will be considered fixed and the parameter values will be set to zero.  The covariance for these fixed parameters will be set based on the following:
3DC Adjustable Parameter 	Standard Deviation if Parameter Fixed
Δx, Δy, Δz	 
Δω, Δφ, Δκ	
 
                      Where
  
  
 
                            And
 = Maximum extent in dimension i from GPM Master metadata
 = Minimum extent in dimension i from GPM Master metadata

Δs	 
Table 6-1: Standard deviations to be used for 3DC parameters held as fixed

6.2.3	COMBINED MODEL

The Ground-Space GPM allows for a combination of the anchor point and 3DC transformation models.  In this mode, both the 3DC transformation and corrections due to anchor point translations are applied simultaneously (see Section 6.2.4.1).  The full covariance matrix for the Ground-Space combined model associated with some point in CU   is that shown in Equation 6-25.  
 
Equation 6 - 25 Ground-Space Combined Model Covariance Matrix.
In Equation 6-25,   is the covariance matrix shown in Equation 6-24, and   is the covariance matrix   shown in Equation 6-16 associated with CU  .  The off-diagonal block,  , contains the covariances between the 3DC transformation parameters and the anchor points.  It is expected that this sub-matrix will be all zeros prior to any adjustment and possibly fully populated (non-zero) after adjustment.  
Since both anchor points and the 3DC transformation can be parameterized such that either there are no anchor points or there are no 3DC transformation parameters, the combined model can be considered the general case for Ground-Space GPM adjustment and error propagation.  That is, it applies even if some components of both, or all components of one of the two individual models has no effect.  For example, if only anchor points are used, then   will have zero rows and columns and   will have 3  rows and columns.  

6.2.4	EXPLOITATION OF GROUND-SPACE GPM

The Ground-Space GPM CSM function calls are given in the following subsections.  Note that the implementations of getUnmodeledError() and getUnmodeledCrossCovariance() are not repeated here since they are the same whether using Ground-Space or Sensor-Space GPM.  One can refer to the Sensor-Space section for their description.  

6.2.4.1	 modelToGround()

The modelToGround() function takes model-point coordinates as input, transforms the model coordinates using the adjustable parameters, and converts the result to ECEF. Optionally, the covariance matrix for the model coordinates (e.g. the mensuration error) can be included as input, which leads to the inclusion of the ground covariance information as additional output.  Since adjustable parameter error covariance values are available to the model internally, their effect will also be applied to the optional ground covariance calculation.  In the Ground-Space GPM implementation, the adjustable parameters are translations at anchor point locations, and the CU-wide 3DC transformation parameters.  These parameters are zero if no adjustment has been performed.  
User Input:
•	 ,  ,   model-point coordinates
•	Optional: Model-point covariance matrix
•	Note: While Point Time is an optional input into modelToGround, a time per point is not required for Ground-Space GPM.  Therefore time, would not be used as an optional parameter for Ground-Space.

Function Output:
•	  ,  ,   ground-point coordinates
•	Optional: Ground-point covariance matrix

The modelToGround() function is the application of Equation 6 - 26.  
 
Equation 6 - 26.  modelToGround() coordinate calculation for the Ground-Space GPM.
In Equation 6 - 26,   is the conversion from MCS model space to ECEF ground space (which isn’t needed if MCS is defined as ECEF),    are the model space coordinates of point  after applying the 3DC transformation using Equation 6-23, each   is a column vector of the coordinate corrections (translations) associated with anchor point , and   contains weights associated with point   and is parameterized as follows:
 ,
where   is the weight associated with anchor point   for point  , and   is a   identity matrix.  See Appendix B for a description of how to calculate .  The distances used in computing   are based on  coordinates, not the transformed .
If the mensuration covariance matrix (  is supplied, the  ground point covariance matrix,  , is computed as shown in Equation 6 - 27.  
 
Equation 6 - 27.  modelToGround() covariance matrix calculation for the Ground-Space GPM.
In Equation 6 - 27,   is the covariance matrix for adjustable parameters as defined in Equation 6-25,   contains the partial derivatives of model space coordinates with respect to the adjustable parameters,   ( contains the partial derivatives of model space coordinates with respect to ground space coordinates, and   and   are the covariance matrices associated with mensuration and unmodeled error, respectively.    is constructed using multiple calls to computeSensorPartials(), and   is constructed using multiple calls to computeGroundPartials() in a fashion similar to that of the Sensor-Space GPM implementation.
As an example, consider the case where the translation components of the 3DC are used in addition to  anchor points.  Also, suppose no adjustment has been performed and there are no correlations between the anchor point and 3DC adjustable parameters.  Then, the matrix components of Equation 6-27 would be formed as follows. 
The adjustable parameter covariance matrix would appear as:
 
The   matrix would appear as:
 
 
 
The   matrix is formed as in the sensor space implementation:
 

6.2.4.2	groundToModel()

The groundToModel() function takes ground-point coordinates as input, converts to MCS, and transforms the resulting coordinates using the associated adjustable parameters. The covariance matrix for the ground coordinates can be optionally included as input, which leads to the inclusion of the model covariance information as additional output.  Since adjustable parameter error covariances are available to the model internally, their effect will also be applied to the optional model covariance calculation.  
Input:
•	 ,  ,   ground-point coordinates
•	Optional:  Ground-point covariance matrix

Output:
•	 ,  ,   model-point coordinates
•	Optional:  Model-point covariance matrix

The groundToModel() function is the application of Equation 6 - 28, using the same symbol definitions as for Equation 6 - 26.  
 
Equation 6 - 28.  groundToModel() coordinate calculation for the Ground-Space GPM.
The function   is a coordinate conversion from ECEF to MCS, and the inverse 3DC transformation is applied as shown in Equation 6-29a where the symbol definitions are the same as those for Equation 6-23.  Equation 6-29b is a simplified equivalent version, with an algebraic cancellation applied.
 
Equation 6 – 29a.  Inverse 3DC Transformation.
 
Equation 6 – 29b.  Simplified Equivalent Inverse 3DC Transformation.
Since  is based on the distances from point model coordinates to anchor point coordinates, the solution is iterative.  The first iteration uses the values of the ground coordinates converted to MCS as initial approximations for model-space coordinates in order to build  .  The resulting    coordinates calculated using Equation 6 - 29 are then used to rebuild .  The process is repeated until changes in the solved   are less than some tolerance (TBD).  
If the ground-point covariance matrix is supplied ( , the  model-point covariance matrix, , is computed as shown in Equation 6 - 30.  Matrices   and   are as defined in Equation 6-27, and   is the unmodeled error covariance matrix.
 
Equation 6 - 30.  groundToModel() covariance matrix calculation for Ground-Space GPM.
6.2.4.3	computeSensorPartials()

In the ground-space implementation, computeSensorPartials() calculates the partial derivatives of the  ,   and   model coordinates with respect to a designated ground-space adjustable parameter given an arbitrary ground   point.
Input:
•	 ,  ,   ground-point coordinates
•	Index of the designated adjustable parameter

Output:
•	Partial derivatives of the  ,  ,   model-point coordinates with respect to the designated adjustable parameter.

Although the user provides the ground point, as with other CSM functions, the GPM adjustable parameters are handled internally to the sensor model plug-in.
The only distinction between this function implementation and its sensor-space counterpart is that the adjustable parameters are the (3DC) parameters and the translations associated with anchor points, as opposed to sensor parameters.  
This function uses numerical partial derivatives.  Using the input  ,  ,   ground-point coordinates, the computeSensorPartials() function first calculates the ( ,  ,  ) model point coordinates via a call to groundToModel().  The numerical partial derivatives of the model point with respect to the ground-space adjustable parameter of interest,   are then calculated by
 
where   is the result from groundToModel() when perturbing the sensor parameter of interest,  , by  , and   is the result from groundToModel() when perturbing   by  .  To perturb the sensor parameter of interest, one must change its value using the CSM function setCurrentSensorParameter() before calling groundToModel(). The values of   are TBD.

6.2.4.4	computeGroundPartials()

Given ground   coordinates, computeGroundPartials() returns partial derivatives of model coordinates with respect to ground coordinates, resulting in a total of nine partial derivatives.
Input:
•	 ,  ,   ground-point coordinates
Output:
•	Partial derivatives of the , ,   model-point coordinates with respect to the ECEF ground coordinates.

The partial derivatives of this model point with respect to the ground coordinates are calculated using numerical methods.   The changes in model coordinates resulting from adding small increments to the ground coordinates are calculated using calls to groundToModel(), with the ratio of the two serving as the output partial derivative:
(e.g.,  ) 
As with the sensor-space implementation of this function, the value of   is TBD.


7	POPULATING / GENERATING GPM FOR SENSOR BUILDERS AND DATA PROVIDERS

So far this document has focused on the use of GPM for the exploitation of point-cloud datasets.  However, in order for this exploitation to take place the GPM-enabled datasets must be available to the SET.  This GPM generation takes place upstream of the exploitation during the initial processing and creation of the point-cloud datasets.  In addition, GPM data may be generated during the initial processing and then refined at later processing stages.  This portion of the document focuses on the GPM generation performed by the data vendors and provides an example based on lidar collection and processing.  Lidar provides a good example because it leverages both the Sensor-Space and the Ground-Space implementations of GPM.  As will be seen, it discusses GPM generation from physical sensor models in general terms since GPM generation can vary greatly from sensor to sensor.  Similarly, there will be differences in generating GPM for a point cloud derived from another modality versus a lidar-derived point cloud.  However, the general concepts of propagating from a sensor-specific model to a generic model and accounting for processing steps such as registration remain the same.
As shown in Figure 7 - 1 below (Source: NGA Lidar Formulation Paper 2011), lidar sensors generally have similar subsystems that consist of a set of core components including: ranging subsystem (laser transmitter, laser receiver), scanning/pointing subsystem, position and orientation subsystem, system controller, and data storage [18, 19, 20].  All of these components are critical to the development of a 3D dataset. Thus, developing a dataset requires a detailed physical sensor model.  However, even with common subsystems across different sensors, the specific implementation of the subsystems varies greatly from sensor to sensor.  For example, a lidar system may be a flying spot scanner or an array collector; it may operate in linear mode or Geiger mode; it may utilize a gimbal or a series of pointing mirrors, etc.
 
Figure 7 - 1  General Lidar Sensor Components.
In all cases, a physical sensor model uses raw measurements collected by the instrument(s) (e.g. sensor position, scan angle, range) to develop coordinates ( ) for points measured by the sensor. One such physical model, as described in the NGA Lidar Formulation Paper, is shown in Equation 7-1 below and describes the relationships among some basic components of a lidar collection system, including the GPS, IMU and sensor.  A series of translations and rotations, obtained from sensor observations and constants, must be applied to a lidar pulse measurement for direct geopositioning of the sensed ground object.  

The coordinates of a sensed ground point are obtained from Equation 7 - 1:
	
 
Equation 7 - 1  Sample Lidar Physical Model (Source: NGA Lidar Formulation paper).
The components of Equation 7 - 1 are described below:
 	vector from the scanner to the ground point in the scanner reference frame (range)
 	vector from the gimbal center of rotation to the sensor in the gimbal reference frame
 	vector from the IMU to the gimbal center of rotation in the platform reference frame
 	vector from the GPS antenna phase-center to the IMU in the platform reference frame
   	vector from the ECEF origin to the GPS antenna phase-center in the ECEF reference frame (GPS observations)
 	vector from the ECEF origin to the ground point in the ECEF reference frame
 	rotation matrix from scanner reference frame to sensor reference frame (scan angles)
 	rotation matrix from the sensor reference frame to the gimbal reference frame (gimbal angles)
 	rotation matrix from the gimbal reference frame to the platform reference frame (boresight angles)
 	rotation matrix from the platform reference frame to the local-vertical reference frame (IMU observations)
 	rotation matrix from the local-vertical reference frame to the ellipsoid-tangential reference frame
 	rotation matrix from the ellipsoid-tangential (NED) reference frame to the ECEF reference frame

A graphical representation of such a model is shown in Figure 7 - 2.
Although this paper will not go into great detail on this notional model, it is important to note that a similar physical model is defined and being used to generate the ground points in all mapping lidar systems.  Similarly, physical models will exist for sensors from other modalities that are used for point-cloud generation.  However the specifics of the model vary between sensors as does the post-processing steps required to generate a useable product.  

 
Figure 7 - 2  Graphical depiction of Lidar Sensor Model Components (Source: NGA Lidar Formulation Paper).
While the physical model is currently being used by data providers to develop ground coordinates, it is generally not being leveraged for another use, namely error propagation.  By identifying the uncertainties of the individual input contributors (e.g. range, scan angle, etc.) used to calculate the point cloud, one can use this model to propagate the individual errors through the system and develop an estimated uncertainty of the final ground points.  Using Equation 7 - 1, this can be performed by developing a partial-derivative matrix (  ) of the ground point ( ) with respect to each physical sensor parameter ( ).  A covariance matrix ( ) must also be developed that describes the uncertainties and the correlations among parameters.  These two matrices can then be used to develop a ground covariance of the lidar point via .  While this approach would work, the model used would be specific to each lidar sensor and the inputs may be unique at the dataset level.  If one wanted to use the physical sensor model parameters as the adjustable parameters for future data adjustments or exploitation, the model specific to that sensor is needed. So, each SET would need to have a current sensor model for each sensor-specific dataset to be exploited.  Therefore, this method would become cumbersome and would complicate interoperability.
As discussed earlier, the goal of GPM (previously ULEM) is to increase interoperability by providing a common set of metadata and adjustable parameters to facilitate downstream exploitation.  To generate this data, a propagation process similar to the one described above is performed.  However, instead of propagating the sensor-specific error contributors to a   ground covariance, they are propagated to the   Sensor-Space GPM covariance discussed earlier in the document that includes system position, pointing, and ranging uncertainty.  A graphical representation of this conversion is shown in Figure 7 - 3.
 
Figure 7 - 3  From Sensor-Specific to Sensor-Space GPM.
All of the error contributors in the physical model must be examined and those parameters that impact a specific GPM Sensor-Space covariance component must be propagated to the GPM covariance.  The equations below illustrate notionally how the various components of the lidar model would propagate to the GPM model.
 
Equation 7 - 2  Contributors from Lidar model to Sensor-Space GPM Range Uncertainty.
 
Equation 7 - 3  Contributors from Lidar model to GPM Position Uncertainty.

 
Equation 7 - 4  Contributors to Line-of-Sight Uncertainty from Lidar Model.
Mathematically, this propagation is performed by first identifying the individual error contributors shown on the left side of Figure 7 - 3.  Remember that the actual contributors will be sensor specific.  The estimated uncertainties of these physical sensor parameters must then be determined and used to develop a covariance matrix ( ).  Using the sensor model and the processing code as a guide, either numerical or analytic partial derivatives are developed that describe the contribution of the various physical sensor parameters ( ) to the GPM parameters ( ) and a partial derivative matrix must be developed ( ).  The sensor uncertainties are then propagated into GPM space using .  Once this is performed, all downstream processing relies on this GPM covariance and the associated adjustable parameters. 
While the concept is simple, the execution of such a conversion can be complex and again varies widely between sensors.  There may be many additional contributors to be considered such as the calibration of individual components, the atmospheric models utilized, etc.  Additionally, to properly develop , one not only needs to know the variance of specific parameters, but also the correlation of each parameter with the other parameters.  When the sensor errors are propagated to Sensor-Space GPM space, the goal is to have a fully populated covariance matrix.  Decisions must be made on the major error contributors and how much fidelity to propagate from the full physical model into GPM space.  There is also a question on how often to calculate this covariance matrix. Some of the input parameters, such as calibration, may be considered static for a collection while others, such as the GPS/IMU uncertainty, will vary across a collect.  So, these kinematic error contributors must be logged and accounted for appropriately.
In addition to computing and recording the covariance at specific timestamps, there is also the need to account for cross-covariance and the correlation between individual covariance records in the pre-adjusted data.  Section 3 of this document described the GPM correlation model, Section 6 discusses how it is exploited, and the appendices describe how it is stored.  However, these correlation parameters must be determined by the people who generate the data in order to be used during processing and exploitation.  Ideally, many of the a priori inputs for these parameters will come directly from the existing sensor metadata.  An example of this would be a GPS/IMU processing software that outputs a full covariance for position and orientation and also provides the correlations between epochs.  When these correlations are available, the SPDCF function must be fit to these values to define the correlation parameters stored in the GPM Data Stream or Parameter Format (indirect storage).  However, these values are not always available, and in these cases the inputs must come from other sources and analyses. For example, auto-correlation of metrics that are available from the processing may be analyzed to estimate these values.  The values may also be estimated using empirical testing, but this can be difficult, costly, and labor intensive. Whatever the method, when indirect storage is used, care must be taken when fitting the SPDCF function to avoid potential pitfalls like those highlighted in [25].  For instance, the SPDCF function must be defined so that the correlation between adjustable parameters at any two times is not larger than the smallest-to-largest ratio of the standard deviations of the two parameters.    Even with the shortcomings, defining correlations is important for being able to compute the cross- covariances required for exploitation.  Without proper correlation information, the adjustable parameters cannot be weighted appropriately in adjustment since their a priori cross-covariances cannot be estimated.  
Another component that must be developed for Sensor-Space GPM is the GPM trajectory file.  This is generally easy to develop as a trajectory is needed in the upstream processing already and it is readily available from the GPS/IMU solution.   Generally, the trajectory solved in standard processing has more fidelity than is required for GPM, so it can be subsampled for GPM to reduce the impact on file size.   In some systems this trajectory information is pulled directly from a separate trajectory file during GPM generation, while in others, the trajectory is extracted from existing metadata that is stored in the post-processed point cloud.
The majority of the discussion above relates to error contributors from the sensor that are observed during data collection and impact initial data used for point-cloud development.  However, many sensors and associated processing, exploitation, and dissemination (PED) architectures have subsequent processing steps that can impact these a priori error covariance estimates. Such steps include sequential registrations, block adjustments, noise removal, surface finding, etc.  Once these subsequent processing steps have occurred, the a priori error covariance and associated correlations are no longer valid.  So, it is very important that these subsequent processing steps be carefully tracked and their impacts accounted for in covariance and correlation values. 
While various forms of point cloud-to-point cloud registration are currently used in many lidar PEDs, many of them are not rigorous in that metrics are not tracked and recorded to determine the quality of the registration and to update the covariance information.  While it is up to the data provider to decide exactly what adjustment process to use, the proper population of GPM requires that rigorous data adjustments be employed that allow for the updating of covariance information.  One example of a rigorous adjustment that is recommended is described in detail in Section 5.  Inputs to the adjustment include the a priori sensor covariance information as previously discussed.  The adjustment produces full covariance information that includes covariances for the GPM adjustable parameters and the cross-covariances among them. 
When posts are used for Sensor-Space GPM data adjustment (refer to Section 5), it is necessary that locations for the posts be selected.  It is important that the post at the beginning of each collection unit (CU) be positioned (temporally) so that it occurs at or before the earliest timestamp for the CU point data.  Similarly, the last post for the CU should be selected so that it occurs at or after the latest timestamp associated with the CU.  The spacing of the posts along the CU will depend on the correlation characteristics of the dataset.  The posts should be placed so that the cross-correlation of all parameters in each correlation group is sufficiently high (e.g.   0.9) (TBD) between a pair of sequential (temporally) posts (Figure 7-4).   
Figure 7-4  Post placement within a collection unit.
Figure 7 - 5  shows the notional application of sensor-space adjustment.  It should be noted it is generic and would be modified based on specific sensor and processing architecture.  For example, the “Lidar Processing” step could vary greatly between sensors. For some sensor PEDs, such as those for Geiger-mode sensors, there may be feed-back loops such that after an adjustment, the adjusted data is fed through a processing step again (e.g. coincidence processing). 

 
Figure 7 - 5  Notional Application of Sensor-Space Adjustment for Lidar.
During the processing chain, the data processor must decide which of the GPM generation and storage methods to use for the final lidar point clouds.  While potentially necessary prior to adjustment, it becomes critical after adjustment.  For lidar, the data could be converted and stored as Sensor-Space GPM as shown in Figure 7-5, or adjusted using Sensor-Space GPM and then converted to Ground-Space GPM as described below (see Figure 7-7). For other lidar systems as well as other modalities, it could be adjusted using a non-GPM adjustment and then converted to Ground-Space GPM. In this case, an error propagation process similar to that described to go from a physical sensor model to Sensor-Space GPM is used to go from the sensor / processing specific model to Ground-Space GPM by propagating the uncertainties to Anchor Points and/or 3DC parameters.  All are acceptable approaches as long as GPM-compliant data is included in the final products and the final predicted uncertainties accurately reflect the dataset uncertainties.  
For any of the approaches, the data processor must also decide whether to store this covariance data using the direct or indirect method.  The full covariance after adjustment may be too large to conveniently store in the dataset and thus indirect storage may be required.  If the indirect method is used, the cross-covariance terms from the adjustment would be used to determine the correlation model parameters discussed in Section 3, and then populated into the datasets in place of the cross-covariance terms.  As discussed above and highlighted in [24], care must be taken when defining these correlation parameters to ensure valid results. 
For some datasets, it may not be desirable to store the final dataset with Sensor-Space GPM.  One example of this is when multi-look data with varying collection geometries and collection times is combined to develop the final product.  In this case, it may be difficult to store a unique time tag per point since multiple collections may have contributed to each point.  This is an example where Ground-Space GPM would be used.  Point-cloud generation from other modalities such as EO, is another example.  A notional view of the creation process for lidar is shown in Figure 7 - 7.   The majority of the flow is similar to that shown for Sensor-Space GPM.  However, additional processing is necessary to combine the individual flightlines / data collects into one dataset.  On the GPM side, the Sensor–Space GPM data (assuming it has been adjusted) is used to determine the ground covariance at each anchor point and the cross-covariance between anchor points.  This ground-space covariance information is then used to populate the Ground-Space GPM metadata in the combined point cloud, replacing any sensor-space metadata.
During this GPM conversion process, the selection of anchor point locations must be made.  This selection process requires constraints similar to those imposed during the selection of post locations for Sensor-Space GPM.  First, it is important that the anchor points encompass the data points of interest to prevent extrapolation during exploitation.  Second, the correlation between adjacent pairs of anchor points must be sufficiently high for each   component (e.g.   0.9) (TBD).  Figure 7-6 illustrates these requirements on anchor point placement. Note that anchor points need not be laid out in a regular grid.
 
Figure 7-6  Anchor Point layout in Ground-Space GPM

Figure 7 - 5 and Figure 7 - 7 show data adjustments as if they are occurring at the time of initial processing.  It is expected that in the near term this will be the standard procedure for most processing architectures and those responsible for the initial development of data.  However, subsequent adjustments could be applied to datasets and these could occur within sensor-space, ground-space or both.  An example of this would be a large adjustment of multiple previously-adjusted tiles of data that have edge overlap.  Adjustments are performed as described in Section 5.  
Similarly, Figure 7 - 5 and Figure 7 - 7 indicate that the transforms associated with the updated adjustable parameters are being applied to the datasets versus storing the updated adjustable parameters for future application.  Recall that applying the adjustable parameters includes both transforming point coordinates (Equation 6-3) and updating the trajectory (Equation 6-7) in the case of Sensor-Space GPM.  However, since applying the transforms to the datasets may be processing intensive, there may be some advantages to storing the adjustable parameters in the file and applying them as needed.  Both options are available in GPM.  If the parameter values stored in the GPM metadata are non-zero, then the parameters have not been applied to the point-cloud points and they should be used when a model is instantiated.  However, if the adjustable parameters have been applied to the points, then the updated points should be written to the file and the adjustable parameters stored in the file should be zeroed out.  Nevertheless, when an adjustment is performed the adjustable parameter covariance is updated with the a posteriori adjustment covariance, whether the adjustable parameters have been applied or only stored. 
Regardless of whether the adjusted parameters have been applied to the point cloud or not, the updated covariances associated with them must be used as a priori adjustable parameter covariance estimates in subsequent adjustments and the parameter initial estimates are as stored in the file (zero if adjustments have been applied or not performed, and non-zero if adjustable parameters have been computed but have not been applied to the points).  

 
Figure 7 - 7  Notional Development of Ground-Space GPM for lidar.
So far, the raw sensor metadata has been discussed and a process to convert that to GPM has been presented. The use of Ground-Space and Sensor-Space GPM adjustments has also been discussed.  However, there are yet more error contributors that should be accounted for if applied during processing.  These include items such as surface finding and averaging.  If processes take place during the data generation that move the point-cloud points, then the errors associated with those processes should be tracked.  It is possible that items such as surface finding may be applied during exploitation, in which case they would be accounted for as part of the exploitation tool mensuration error.  However, if applied during the point cloud generation, they must be addressed in the covariance information that is carried with the point cloud.  Detailed descriptions will not be provided here since both the processes and their impact of output covariance data can vary widely.
 

8	REFERENCES

[1]  DMA-TR-8400.1  DMA Technical Report: Error Theory as Applied to Mapping, 	Charting, and Geodesy

[2]  ISO TC/211, 19113:2002 Geographic information – Quality Principles, November 	20, 2002.

[3]  ISO TC/211, 19116:2004 Geographic information – Positioning Services, December 	17, 2007.

[4]  ISO TC/211 211n2047, Text for ISO 19111 Geographic Information - Spatial 	referencing by coordinates, as sent to the ISO Central Secretariat for issuing as FDIS, 	July 17, 2006.

[5]  Collins, George W., The Foundations of Celestial Mechanics, Pachart Foundation dba 	Pachart Publishing House, 2004.

[6]  Gelb, Arthur, Applied Optical Estimation, The MIT Press, May 15, 1974

[7]  McGlone, C., Mikhail, E., Bethel, J., Mullen, R.  Manual of Photogrammetry.  ASPRS; 5th 	edition (2004)

[8]  Albota, M., Heinrichs, R., Kocher, D., Fouche, D., Player, B., O’Brien, M., Aull, B., 	Zayhowski, J., Mooney, J., Willard, B., and Carlson, R.,   Three-Dimensional Imaging 	Laser Radar with a Photon-Counting Avalanche Photodiode Array and Microchip 	Laser, Applied Optics Vol. 41, No 36, December 20, 2002

[9]  Aull, B., Loomis, A., Young, J., Heinrichs, R., Felton, B., Daniels, P., and Landers, D.,  	Geiger-Mode Avalanche Photodiodes for Three-Dimensional Imaging, MIT Lincoln 	Laboratory Journal, Vol. 13, No. 2, 2002, pp. 335-350.

[10]  ISO TC/211, 19115:2003 Geographic information – Metadata, August 23, 2007.

[11]  Merriam-Webster Online Dictionary – Merriam Webster Online (www.Merriam-		  Webster.com) copyright © 2012 by Merriam-Webster, Incorporated.

[12]  MIL-HDBK-850, Military Handbook: Glossary of Mapping, Charting, and Geodetic 	 	  Terms, January 21, 1994.

[13]  Theiss, H., 2010, “Modification of CSM API to Support Stereo Image Pairs”, CSMWG 		Meeting, Melbourne FL, 13 Jan 2010

[14]  Dolloff, J., 2010, “Parameter Ranges for a Valid CSM Decay model”, NGA White Paper, 06 July 2010


[15]	Community Sensor Model Working Group, Community Sensor Model (CSM) Technical  Requirements Document (TRD) Version 3.0, 29 September 2010
	Note: The GPM text above references CSM Versions 3.0.2 which was under development at the time this document was developed.

[16]  MIL-STD-600001, Department of Defense Standard Practice: Mapping, Charting and Geodesy Accuracy, February 26, 1990

[17]	Dolloff, J., Lofy, B., Sussman, A., Taylor, C., Strictly Positive Definite Correlation Functions, Signal Processing, Sensor Fusion, and Target Recognition XV, Proc. Of SPIE Vol. 6235 62351A-1.[18]  Brenner, C., Aerial Laser Scanning. International Summer School “Digital Recording and 3D Modeling”. April 2006

[19]  Liadsky, J.  Introduction to LIDAR. NPS Workshop, May 24, 2007.

[20]  Wehr, A. Airborne Laser Scanning – An Introduction and Overview

[21]  Dolloff, J. and Theiss, H., 2011, “Interpolation into an Uncertainty Grid”, (Draft)

[22]  The American Society for Photogrammetry and Remote Sensing, LAS Specification Version 1.3 – R11, October 24, 2010

[23]	Dolloff, J., “Assembling a Multi-Imaging Event Error Covariance Matrix”, NGA White Paper, 06 July 2010.

[24]	Dolloff, J. and Theiss, H., 2012, “Matrix Square Roots with Error Covariance Representation Applications”, NGA White Paper, 02 November 2011.

[25]	Dolloff, J. and Theiss, H., 2011, “Correlation of Measurement Errors with Different Uncertainties: Effects on scalar systems, stereo extraction, and the quality assurance of meta-data”, NGA White Paper, 27 December 2011.

[26]	Johns Hopkins University Applied Physics Laboratory, BPF3 File Format Definition, 23 May 2013.

 

9	GPM STORAGE ROADMAP

This section provides an overview for the file storage of GPM metadata.  File formats are defined for storing GPM metadata as variable length records (VLRs) in the LAS file format [22], or as bundled files in the BPF3 file format [26].  It should be noted that although the term VLR is used extensively in this document and VLR is a term that is generally considered specific to LAS, in this document VLR is used in a general sense to describe the binary data content being stored per GPM data block.  As illustrated with the BPF bundled files, the same metadata can be carried within data formats other than LAS.
9.1	GPM IMPLEMENTATION STORAGE OPTIONS

GPM storage options have been developed to accommodate the different GPM implementations outlined in Section 1.3.  This information is provided primarily for GPM metadata generators and tool developers.  The two fundamental GPM implementations, Sensor-Space GPM and Ground-Space GPM, have completely separate but similar storage solutions.  The GPM metadata generators or modifiers choose one or the other storage solutions based on data content and complexity.  This concept is outlined in Figure 9 – 1.  A more detailed overview for each GPM metadata storage solution is provided in the following subsections.
 
Figure 9 – 1  Top-level GPM Metadata Storage Options




9.2	SENSOR-SPACE GPM STORAGE

Sensor-Space GPM is comprised of two configurations.  One makes use of metadata in a Data Stream Format.  The other configuration uses Parameter Format and is based on collection units and posts, and has two covariance storage options, direct and indirect.  These Sensor-Space GPM storage options are shown in Figure 9 – 2.  The different storage options are mutually exclusive, but they do share some common components.  For any of the Sensor-Space storage options, the Trajectory Record(s), the Unmodeled Error Record (see Appendix F), and the GPM Master VLR (see Appendix G) are always included.  For the Parameter Format (collection unit/posts) storage case, an Adjustable Parameter Record is included as a separate metadata file, and the covariance metadata is included using either the direct or indirect format Sensor Covariance Records.  For both Data Stream and Parameters format an optional Per Point Error Record exists (see Appendix H). Details of the Sensor-Space metadata storage options are contained in Appendix D.









 

























Figure 9 – 2  Sensor-Space GPM Metadata Storage Overview.
9.3	GROUND-SPACE GPM STORAGE

Ground-Space GPM storage is divided into two options, as shown in Figure 9 – 3.  With this storage option, the Unmodeled Error Record (see Appendix F) and the GPM Master VLR (see Appendix G) is always included.  The Ground-Space adjustable parameters and covariance metadata are stored using either the direct or indirect format Ground-Space Data Records.  An optional Per Point Error Record also exists (see Appendix H). Details of the Ground-Space metadata storage options are contained in Appendix E.











Figure 9 – 3 Ground-Space GPM Metadata Storage Overview.






 
Appendix A  : Additional Sources of Mensuration Error

For GPM, the traditional mensuration error described in Section 3.2.3 is only one contributor to the overall mensuration error.  In GPM, “mensuration error” can also be used to capture contributions from other random error sources. This appendix discusses two such additional mensuration error sources and shows how they are applied during exploitation. 
One such random error source is associated with data processing and is related to the handling of the data within the SET or ELT.  An example of an error contributor related to data handling / exploitation is a surface finding algorithm that is running real-time within the ELT.  This surface finding would have an error associated with it that is specific to the algorithm and the ELT, and represents an example of a processing mensuration error.
The covariance matrices for these processing contributions to mensuration errors are included in the predicted overall mensuration error covariance at the time of measurement.  The errors are assumed to be uncorrelated from point to point and their covariances are stored in a block diagonal matrix similar to the one used for analyst contribution as shown in Equation A-1.
 
		where
 
Equation A - 1.  Processing error contribution to mensuration error.
In addition to the traditional mensuration error and the processing mensuration error  , there may exist additional per-point 3D random error  ,.  These would be additional random errors that could not be removed as part of an adjustment and could not be adequately modeled using unmodeled error, but that must be accounted for in order to provide adequate estimates of the errors in the point data.  The sources of such error could vary, but one example would be the contributions from a random ranging error in a lidar system (versus a range bias solved for in an adjustment).  A second potential source is associated with the number of image rays and the geometry of the intersecting image rays used in the development of points in an Electro-Optical based point cloud.  These contributors provide additional error that can vary significantly from one point to another in an EO point cloud.  The 3D random errors for an individual point are captured in a full  covariance matrix, with the errors for multiple points captured in a block diagonal matrix as in Equation A-2.     Additional details on populating the matrices for individual points in the block diagonal matrix in Equation A-2 are provided in Appendix H.

 
		where
 
Equation A - 2.  Processing error contribution to mensuration error.

Thus, the mensuration error covariance matrix ( ) for GPM consists of multiple components: 1) the random mensuration error covariance associated with the analysts   , 2) random error covariance associated with the processing system / exploitation tool  , and 3) 3D random per-point error  , .  These contributors are combined at the time of exploitation as shown in Equation A - 3, developing the covariance matrix of the mensurated points.  This combined mensuration error is then what would be used as the mensuration error in the final exploitation algorithms.
   
Equation A - 3.  Developing covariance of final mensurated point.
 

Appendix B  Interpolation of Adjustable Parameters

Both Sensor-Space and Ground-Space GPM use interpolation between posts and anchor points, respectively, in their model equations.  The methods in this appendix are based on experiments described in [21].  The first subsection of this appendix describes interpolation in sensor-space, and the second describes interpolation in ground-space.  The methods presented here are the default interpolation methods for GPM adjustable parameters.  In addition to these methods, the GPM allows for alternate methods to be used.  Specifically, it may be advantageous to use nearest-neighbor interpolation instead.  Ultimately, additional alternatives may be defined, and thus the recommended methods presented in this section can be considered TBR.  To support a variety of interpolation schemes, there is a flag in the GPM metadata which specifies the interpolation method to be used with the associated dataset.

B.1 Sensor-Space Interpolation

The post interpolation method is based on the weighted average of the bookending posts.  Weights are determined by the difference between the time associated with a point and the times at the posts.  The interpolated adjustable parameters for a given time,  , are calculated as shown in Equation B - 1 using the immediately previous post at time , and the immediately subsequent post at time .  The vector   contains the interpolated sensor parameters for arbitrary time ,   and   are the adjustable parameter vectors associated with the bookending posts at times  and  , respectively, and  and   are the weights associated with these posts.  Note that only a subset of the seven adjustable parameters might be associated with the posts, and which actual parameters are used is contingent upon the Parameter Format design of the dataset (Section 6).
 
Equation B - 1.  Interpolation of Sensor-Space Adjustable Parameters.
In Equation B - 1, weights are determined such that the result is a linear interpolation, and are calculated by:
 .


B.2 Ground-Space Interpolation 

Ground-space anchor point interpolation consists of using the spatial distance from anchor points to weight their contribution in finding arbitrary point translation.  The interpolated translation for some arbitrary point, , is shown in Equation B-2, where   is the arbitrary point translation vector,  is the translation vector (composed of anchor point adjustable parameters) associated with anchor point  , and subscripts   refer to the n closest anchor points to point .  
 
Equation B - 2.  Interpolation of Ground Space Adjustable Parameters.
In Equation B-2,   is the weight associated with anchor point  ,    is the 3D distance from the arbitrary point to anchor point  , and   is a normalizing scale factor such that 
 .
The constant   is a dampening parameter, and the recommended value of   is 0.25 times the nominal anchor point spacing.  However, the value of D to be used for a specific file is stored as a GPM metadata element.
In the equations above, n refers to the number of closest anchor points to be included in the interpolation process.  While it is possible to include all anchor points in every interpolation, it can become computationally intensive and may greatly increase processing times.  In testing to date, using a smaller number of anchor points, such as n=6, gives nearly equivalent results and provides greater processing throughput.  
 


Appendix C  : Square Root of a Matrix

To apply the decorrelation factor and develop a cross-covariance between two point-cloud points, this document proposes taking the product of the square roots of two covariance matrices as shown below.  A thorough discussion on this method, including the validity thereof, is given in [23].  This appendix provides one method, based on Singular Value Decomposition (SVD), that could be used to perform such a calculation.
 
Equation C - 1.  Cross-covariance between two points, A and B.
Call the matrix ΣA matrix A.
 
Equation C - 2.  Developing the product matrix A.
The square root matrix of   is determined by finding a matrix   that satisfies the condition .  One method to determine M if the product matrix A is a symmetric, positive semi-definite matrix is through the use of eigenvectors and eigenvalues.  First, the eigenvalues (λ) of A are determined and used to populate a diagonal matrix   where each element on the diagonal of   represents an eigenvalue.  The eigenvectors (υ) are determined and used to populate a matrix VA in which each column in VA represents an eigenvector of A. This leads to the relationship:
 
 Equation C - 3.  Relationship between Matrix A and the Eigenvalues and Eigenvectors.
Matrix   is a diagonal matrix with positive values on the diagonal.  Thus, the square root of matrix   ( ) is developed by taking the square root of the diagonal elements of , satisfying the condition:
 
 Equation C - 4.  The square root of the eigenvalue matrix.
Finally, since   is an orthogonal matrix (i.e. ), the square root of A can be determined as follows:
 
 Equation C - 5.  Determining the square root of matrix A.
Defining matrix B to represent matrix , a similar development produces the following equation:

 
 Equation C - 6.  Determining the square root of matrix B.
Thus the product of the square roots is shown in Equation E-7.
 
 Equation C - 7.  The product of the square roots of   and  .
This is one potential method to compute the square root of a matrix and provided as an example.  There are other methods that could be used and other methods that may be required for specific circumstances.  As communicated in an earlier footnote, some of these alternate methods (e.g. Cholesky decomposition) require that the second matrix in the product of Equation C - 1 be transposed, so the cross-covariance is calculated as 

 

However, since covariance matrix square roots are symmetric in the Eigen-decomposition method presented here, this step is unnecessary. 



 

Appendix D : Sensor-Space GPM Storage Format

The Overview section provided general insight into the components of the GPM model.  This appendix provides more detailed insight into storing each of the components of a file containing GPM metadata for Sensor-Space format.  It starts with the point record, then investigates the platform trajectory, and finally looks at the sensor covariance data. 
Throughout this appendix, where not specified, all positional and distance units are in meters, all angular units are in milliradians and all time units are in seconds.  In accordance with both the LAS and BPF specifications, all data is in little-endian format.

GPM Sensor-Space Point Record
The GPM Sensor-Space model is based on a lidar point-cloud dataset consisting of a series of individual point records known as model points.  At a minimum, Sensor-Space GPM point records must consist of:
 
Equation D - 1.  Minimum GPM Sensor-Space Point Record.
which is the 3D coordinate of the model point and a time tag.  If there are multiple flightlines being combined, each with a unique trajectory, a trajectory identifier will also be required.  Additional information could be stored per point such as the intensity of the point, although this information is not currently used by GPM.  Table D - 1 below indicates how a GPM point record is mapped to an LAS 1.3 format (The GeoKey Tag VLRs required by the LAS specification are also required for GPM). Table D-2 indicates how a Sensor-Space GPM point record is stored within BPF3.
It should be noted that the points in Tables D-1 and D-2 are in the native coordinate system used in the LAS/BPF file, which may not be the same as the MCS.  In these cases, the point coordinates must be converted to the MCS prior to exploitation with the GPM model. 
Table D - 1:  GPM Sensor Space Point Record (LAS).
ID	Parameter	Definition	Obl. LAS1.3	Description	Name/Role Name
1	Point x record	The x position of a specific point. 	M	The x position of the lidar returns stored per point record.  This value is used in combination with the x Scale Factor and x Offset to determine the x coordinate of a given point.	LASF_X
2	Point y record	The y position of a specific point. 	M	The y position of the lidar returns stored per point record.  This value is used in combination with the y Scale Factor and y Offset to determine the y coordinate of a given point.	LASF_Y
3	Point z record	The z position of a specific point.	M	The z position of the lidar returns stored per point record.  This value is used in combination with the z Scale Factor and z Offset to determine the z coordinate of a given point.	LASF_Z
4	Point Source ID	This field indicates the file from which this point originated.  	M	Unsigned short that ranges from 1 to 65,535 inclusive with 0 being used for the special case where the point originated in the current file.  Point Source ID indicates the file from which this point originated.	For GPM this is the Point Source ID number stored in the GPM Master VLR for the CU that this point is associated with.  It is used to link this point to a specific CU and is also used to refer to the proper covariance and trajectory VLRs.  If the same point is associated with multiple trajectories, the point record will be duplicated and this field will be updated to reflect the proper trajectory association (defined in a VLR).
5	GPS Time	Time tag value at which the point was acquired.	M	The double floating point time tag value at which the point was acquired. It is GPS Week Time if the Global Encoding low bit is clear and Adjusted Standard GPS Time if the Global Encoding low bit is set (see Global Encoding in the Public Header Block description). Conditional in that it is used for LAS 1.3 record formats 1 and 3.	
6	PPE LUT index	Per Point Error (PPE) Look-up table index 	User Defined	A pointer providing the index into the Per Point Error (PPE) Look-up Table (LUT) that provides for the retrieval of the PPE covariance associated with a given point.  
When LAS1.4 is adopted within the community, the PPE_LUT_Index will be added as a user defined addition to each point record and  documented within the LAS1.4 using the EXTRA_BYTES VLR.  

When LAS 1.2 or 1.3 is being used, then the “USER DATA” field is used to store the PPE_LUT_index.  This limits the number of LUT covariance entries to 256.  If this is not adequate, then LAS 1.4 must be adopted to meet the requirement for additional covariance.

	PPE_LUT_Index



Table D - 2:  GPM Sensor-Space Point Record (BPF3)
ID	Parameter	Definition	Obl. BPF3	Description	BPF3 Label
1	Point x record	The x position of a specific point. 	M	The x position of the lidar returns stored in the point data.  This value is used in combination with the x Offset from the metadata subheader and the transform from the header to determine the x coordinate of a given point.	X
2	Point y record	The y position of a specific point. 	M	The y position of the lidar returns stored in the point data.  This value is used in combination with the y Offset from the metadata subheader and the transform from the header to determine the y coordinate of a given point.	Y
3	Point z record	The z position of a specific point.	M	The z position of the lidar returns stored in the point data.  This value is used in combination with the z Offset from the metadata subheader and the transform from the header to determine the z coordinate of a given point.	Z
4	Point Source ID	This field indicates the file from which this point originated.  	M	
Unsigned short that ranges from 1 to 65,535 inclusive with 0 being used for the special case where the point originated in the current file.  Point Source ID indicates the file from which this point originated.
For GPM this is the Point Source ID number stored in the GPM Master VLR for the CU that this point is associated with.  It is used to link this point to a specific CU and is also used to refer to the proper covariance and trajectory VLRs.  If the same point is associated with multiple trajectories, the point record will be duplicated and this field will be updated to reflect the proper trajectory association (defined in a VLR).	Point_Source_ID
Note:  This is a user defined dimension in BPF3 and will have a label of “Point_Source_ID” within the metadata subheader.
5	Point Time	Time tag value at which the point was acquired.	M	The double floating point time tag value at which the point was acquired. Since the base BPF3 does not specify a time dimension for the point data, care must be taken to ensure that the time format used to assign the time in the GPS Time field is consistent with the time used in the bundled GPM data (trajectory, covariance, etc.) and that it is consistent with the time / units used in correlation functions with the GPM metadata.	Point_Time
Note:  This is a user defined dimension in BPF3 and will have a label of “Point_Time” within the metadata subheader.
6	PPE LUT index	Per Point Error (PPE) Look-up table index 	User Defined	A pointer providing the index into the Point Per Error (PPE) Look-up Table that provides for the retrieval of the PPE covariance associated with a given point.  	PPE_LUT_Index
Note:  This is a user defined dimension in BPF3 and will have a label of “PPE_LUT_Index” within the metadata subheader.



GPM Trajectory Record
GPM requires a trajectory file (or multiple trajectory files if needed to model multiple flightlines) be saved as a time series to describe the platform position during the data collection.  Prior to data adjustment, this trajectory is developed directly from the sensor metadata.  After adjustment, this trajectory must be updated per flightline as outlined in Section 6.1.6.  At a minimum, each record in this file consists of:
 
Equation D - 2.  Trajectory Point Record.
which is the platform location (xs, ys, zs) given in the same Model-space Coordinate System (MCS) as the laser return points, and a GPS time tag (tGPS) associated with this position fix.   During data exploitation, the time tag for a point of interest can be determined and the user can then interpolate the sensor position from the trajectory file at the given time.  A sample of encoding the trajectory file into an LAS variable length record (VLR) is shown below in Table D - 3 and Table D - 4.  Table D - 5 defines the header information for BPF3 file storage.  The metadata in Table D - 4 would then immediately follow this header information.
Table D - 3:  GPM Trajectory VLR Header Information.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	270		1	Unsigned short	2 bytes
H5	Record Length After Header	(136 + N * 32) bytes		1	Unsigned short	2 bytes
H6	Description	GPM_Trajectory_File		1	Char[32]	32 bytes

Table D - 4:  GPM Trajectory Metadata.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Data
MD2	Trajectory_File	The variable length record carrying the sensor trajectory information.	Lines MD3-MD10	1		
MD3	Trajectory_ID	The unique identifier for a given trajectory.
This is the number used in the Point Source ID field that uniquely associates a point with a trajectory and CU.		1	int	4 bytes
MD4	Sensor Trajectory Records	The number of records in this sensor trajectory VLR.		1	int	4 bytes
MD5	COLLECTION_UNIT_ID	Collection Unit identification string unique to the CU this trajectory is associated with as defined in the GPM Master VLR.		1	Char[128]	128 bytes
MD6	SENSOR_TRAJECTORY	The trajectory of the sensor over a given collection, providing the sensor geoposition at specified times.	Lines MD7-MD10	N		
MD7	PLATFORM_TIME	Sensor Location Time
P(t).  Time for a specific platform location		1	double	8 bytes
MD8	SENSOR_GEOLOC_X	Sensor Geolocation at time  P(t).  The x-coordinate of the sensor reference point (S) at time P(t) with respect to the MCS.		1	double	8 bytes
MD9	SENSOR_GEOLOC_Y	Sensor Geolocation at time  P(t).  The y-coordinate of the sensor reference point (S) at time P(t) with respect to the MCS.		1	double	8 bytes
MD10	SENSOR_GEOLOC_Z	Sensor Geolocation at time  P(t).  The z-coordinate of the sensor reference point (S) at time P(t) with respect to the MCS.		1	double	8 bytes

Table D -5:  BPF3 Bundled File Header Information for Trajectory Data.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	Length of this bundled file data following this header.
(136 + N * 32) bytes		1	UInt32	4 bytes
H4	Filename	GPM_Trajectory_File		1	Char[32]	32 bytes


GPM Sensor Covariance Record
One of the key benefits of GPM is the ability to propagate errors to points on the ground to be able to estimate the ground covariance at specific locations.  GPM accommodates two different formats for storing the sensor parameter covariance information, as introduced in Section 1.3.1 and discussed in greater detail in Section 6.  These methods are referred to as “Data Stream Format” and “Parameter Format”.  The first, detailed here, uses an indirect storage method, in which full 7x7 covariance matrices are stored for each epoch of available covariance information (i.e. covariance epoch).  Cross-covariance information among the epochs is determined using a correlation model, whose parameters are stored in the record.  

GPM Data Stream Sensor Covariance Record
One of the key components of the error propagation is the covariance information for the GPM sensor parameters defined in Section 6.1.  This symmetric sensor covariance matrix for each epoch is formed as shown below which only shows the upper-triangular portion of the matrix:  
 
Equation D - 3.  GPM Data Stream Sensor Covariance Matrix.
In this matrix, [ ] represents the variances in the sensor position adjustable parameters in the path coordinate system; [ ] represents the variances in the orientation adjustable parameters of the line-of-sight in the path coordinate system; and [ ] represents the variance in the range component.  Finally, all of the off-diagonal covariance elements are stored to describe the relationships among the various components.  In addition, a single 3x3 covariance matrix representing positional offset uncertainties ( ,  ,  ) in the Model-space Coordinate System(MCS) is stored.  Prior to adjustment, the frequency and spacing of covariance epochs may be driven by the available covariance data from the sensor.  This covariance data is stored in a metadata record or multiple records if needed to model multiple flightlines.  If multiple records are needed, the positional offset uncertainties are repeated in each one.  After adjustment, a covariance epoch takes the form of an adjustment post.  An example of encoding the Data Stream into an LAS variable length record is provided in the Table D - 6 and Table D - 7 below.  Storage in BPF3 file simply involves using the header information in Table D - 8 in place of Table D - 6.

Table D - 6:  Data Stream Sensor Covariance VLR Header Information.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	271		1	Unsigned short	2 bytes
H5	Record Length After Header	162 + NUM_CORR_GROUPS * 17 + NUM_COV_RECORDS * 120 bytes		1	Unsigned short	2 bytes
H6	Description	GPM_Data_Stream_Storage		1	Char[32]	32 bytes

Table D - 7:  GPM Data Stream Sensor Covariance Metadata.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Data
MD2	DATA_STREAM _STORAGE_FILE	The variable length record carrying the indirect storage of sensor-space data stream covariance information for this collection unit.	MD3- MD51	1	N/A	
MD3	COV_ID	The unique identifier for a given covariance record.
This is the number used in the Point Source ID field that uniquely associates a point with a trajectory and with covariance information.		1	int	4 bytes
MD4	COLLECTION_UNIT_ID	Collection Unit identification string unique to the CU this covariance is associated with as defined in the GPM Maser VLR.		1	Char[128]	128 bytes
MD5	INTERPOLATION_MODE	Flag indicating the interpolation mode for the parameters in this collection unit.
Value = 0
A value of 0 signifies nearest neighbor interpolation.
A value of 1 signifies interpolation as defined in Appendix B.
Values 2 through 65535 reserved.  Table of additional values and association with specific interpolation methods is TBD.		1	Unsigned short	2 bytes
MD6	NUM_CORR_GROUPS	The number of correlation groups contained in this VLR.		1	Unsigned short	2 bytes
MD7	GLOBAL_SPCDF_CORRELATION_PARMETER	 
 
Parameters (A, α, β, τ) used to describe the correlation decrease between points as a function of delta time.
NOTE:  This record occurs M times, where M is the value of NUM_CORR_GROUPS.	Lines MD8-MD12	M	N/A	
MD8	PARAM_INDEX_FLAGS	Seven binary flags in order (Δx,Δy, Δz, θ1 , θ2 , θ3, Δr), starting at the lowest order bit, that indicate which parameters are included in the current correlation group. (i.e., Δx bitmask = 1, θ1 bitmask = 8, etc.).  The eighth bit is left zero.		1		1 byte storage (7 bits used) 
MD9	PARAM_A	Parameter A controlling the maximum correlation that can be obtained.		1	float	4 bytes
MD10	PARAM_ALPHA	Parameter alpha (α) used with A to define the  minimum correlation value that can be obtained.		1	float	4 bytes
MD11	PARAM_BETA	Parameter Beta (β), controlling the shape of the correlation curve and the speed of the decay.  		1	float	4 bytes
MD12	PARAM_TAU	Parameter Tau (τ), a time constant.		1	float	4 bytes
MD13	MCS_COV	This record contains the 3x3 Model-space Coordinate System positional offset error covariance for the entire dataset.
 
Symmetric matrix
Variance (σ2) and covariance data for adjustable parameters of MCS position offset (Δx,Δy,Δz).
	Lines MD14 – MD19	1	N/A	
MD14	MCS_VARX	The variance of the adjustable parameter Δx, which is the x coordinate adjustment to the Model-space coordinate system.		1	float	4 bytes
MD15	MCS_VARY	The variance of the adjustable parameter Δy, which is the y coordinate adjustment to the Model-space coordinate system.		1	float	4 bytes
MD16	MCS_VARZ	The variance of the adjustable parameter Δz, which is the z coordinate adjustment to the Model-space coordinate system.		1	float	4 bytes
MD17	MCS_VARXY	Covariance in Δx,Δy		1	float	4 bytes
MD18	MCS_VARXZ	Covariance in Δx,Δz		1	float	4 bytes
MD19	MCS_VARYZ	Covariance in Δy,Δz		1	float	4 bytes
MD20	SS_COV_EPOCH_LIST	This part of the variable length record specifies the time (t) of each covariance epoch along with its associated error covariance.	Lines MD21- MD51	1	N/A	
MD21	NUM_COV_RECORDS	The number of sensor-space covariance records contained in this VLR.		1	Unsigned short	2 bytes
MD22	SS_COV	This record contains the time t and the associated error covariance for a specific epoch in the collection unit.
NOTE:  This record will be repeated from 1 to N times, where the value of N is dependent on the number of epochs required to accurately model changes in the covariance and is specified by NUM_COV_RECORDS.
 
Symmetric matrix
Variance (σ2) and covariance data for adjustable parameters of sensor position  (Δx,Δy,Δz), line-of-sight (θ1 ,θ2,and θ3), and range (Δr).
	Lines MD23 – MD51	N	N/A	
MD23	SS_T	The timestamp that the subsequent error covariance is referenced to.		1	double	8 bytes
MD24	SS_VARX	The variance of the adjustable parameter Δx, which is the x coordinate adjustment in the PCS at a time of SS_T.		1	float	4 bytes
MD25	SS_VARY	The variance of the adjustable parameter Δy, which is the y coordinate adjustment in the PCS at a time of SS_T.		1	float	4 bytes
MD26	SS_VARZ	The variance of the adjustable parameter Δz, which is the z coordinate adjustment in the PCS at a time of SS_T.		1	float	4 bytes
MD27	SS_VART1	The variance of the adjustable parameter θ1, which is the adjustment to the pointing direction in the PCS at a time of SS_T.		1	float	4 bytes
MD28	SS_VART2	The variance of the adjustable parameter θ2, which is the adjustment to the pointing direction in the PCS at a time of SS_T.		1	float	4 bytes
MD29	SS_VART3	The variance of the adjustable parameter θ3, which is the adjustment to the pointing direction in the PCS at a time of SS_T.		1	float	4 bytes
MD30	SS_VARR	The variance of the adjustable parameter (Δr) along the LOS range vector at a time of SS_T.		1	float	4 bytes
MD31	SS_VARXY	Covariance in Δx,Δy		1	float	4 bytes
MD32	SS_VARXZ	Covariance in Δx,Δz		1	float	4 bytes
MD33	SS_VARXT1	Covariance in Δx,θ1		1	float	4 bytes
MD34	SS_VARXT2	Covariance in Δx,θ2		1	float	4 bytes
MD35	SS_VARXT3	Covariance in Δx,θ3		1	float	4 bytes
MD36	SS_VARXR	Covariance in Δx,Δr		1	float	4 bytes
MD37	SS_VARYZ	Covariance in Δy,Δz		1	float	4 bytes
MD38	SS_VARYT1	Covariance in Δy,θ1		1	float	4 bytes
MD39	SS_VARYT2	Covariance in Δy,θ2		1	float	4 bytes
MD40	SS_VARYT3	Covariance in Δy,θ3		1	float	4 bytes
MD41	SS_VARYR	Covariance in Δy,Δr		1	float	4 bytes
MD42	SS_VARZT1	Covariance in Δz,θ1		1	float	4 bytes
MD43	SS_VARZT2	Covariance in Δz,θ2		1	float	4 bytes
MD44	SS_VARZT3	Covariance in Δz,θ3		1	float	4 bytes
MD45	SS_VARZR	Covariance in Δz,Δr		1	float	4 bytes
MD46	SS_VART1T2	Covariance in θ1, θ2		1	float	4 bytes
MD47	SS_VART1T3	Covariance in θ1, θ3		1	float	4 bytes
MD48	SS_VART1R	Covariance in θ1, Δr		1	float	4 bytes
MD49	SS_VART2T3	Covariance in θ2, θ3		1	float	4 bytes
MD50	SS_VART2R	Covariance in θ2, Δr		1	float	4 bytes
MD51	SS_VART3R	Covariance in θ3, Δr		1	float	4 bytes

Table D - 8:  Sensor Data Stream Covariance BPF3 Bundled File Header Information.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	162+ NUM_CORR_GROUPS * 17 + NUM_COV_RECORDS * 120 bytes		1	UInt32	4 bytes
H4	Filename	GPM_Data_Stream_Storage		1	Char[32]	32 bytes



GPM Sensor-Space Collection Unit Parameter Record
GPM captures sensor-space data adjustments within Collection Units (CUs), as defined in Section 6.  CUs permit storing varying predicted error metadata via a combination of up to a first-order polynomial and “post” positions at specified times.  Sensor-Space GPM defines up to 17 adjustable parameters for each collection unit, and it defines up to 7 adjustable parameters for each post within each collection unit.  (Refer to Section 6 for the definition of these parameters).  The parameter record defines the order of the parameter storage, and which of the possible adjustable parameters are being used in a particular point-cloud file along with their values.  The adjustable parameter values may be specified or set to zero.  They will be zero if an adjustment has yet to be performed on the dataset or if adjustable parameters have been solved and already applied to the point-cloud points and associated trajectory.  The parameter values will be set (non-zero) if they have been solved, but have yet to be applied to the point data.

GPM Sensor-Space Collection Unit Parameter Order
The order of the post adjustable parameters is depicted in Figure D-1.  The definition of which adjustable parameters are included for a particular dataset is controlled by a 1-byte flag.    Each bit of the Index Flag is set to “1” if the parameter is included and set to “0” if it is not included (the highest order bit is not used).  The parameter order and parameter selection applies to both the parameter values defined here, and the parameter covariance values, defined in Table D-13 and Table D-16 .  The example flags in Figure D-1 indicate that the post adjustable parameters are  .  Note that the highest order bit is not used, and is always zero.  The lowest order bit corresponds to xp.

 
			           { 0      0       1       1      1         0        0        0    }



Figure D - 1.  GPM Sensor-Space Post Adjustable Parameters.
The order of the collection unit adjustable parameters is depicted in Figure D-2.  The definition of which adjustable parameters are included for a particular data set is controlled by a 4-byte flag.    Each bit of the Index Flag is set to “1” if the parameter is included and set to “0” if it is not included (the 15 highest order bits are not used).  The parameter order and parameter selection applies to both the parameter values defined here, and the parameter covariance values, defined in Table D-13 and Table D-16.  The example flags in Figure D-2 indicate that the collection unit adjustable parameters are  .  Note that last 15 bits are not used and are always zero.  The lowest order bit corresponds to  .
 
      {000…0   0      0      0        0       0       0      0      0     1      1     1       1       1      1    0      0      0    }


Figure D - 2.  GPM Sensor-Space Collection Unit Adjustable Parameters.

Within a given dataset (LAS file, for example) there can be multiple CUs, and for each CU there can be multiple posts.   The designated number of adjustable parameters defined for posts applies to all posts, and the designated number and definition of adjustable parameters for CUs applies to all CUs.  The method of encoding the adjustable parameter data into an LAS variable length record is provided in Table D – 9 and Table D – 10 below.  Storage in a BPF3 file simply involves using the header information in Table D – 11 in place of Table D - 9.

Table D - 9:  Sensor-Space Collection Unit Adjustable Parameter VLR Header Information.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	280		1	Unsigned short	2 bytes
H5	Record Length After Header	Variable		1	Unsigned short	2 bytes
H6	Description	GPM_Sensor_CU_Adjustable_Params		1	Char[32]	32 bytes

Table D - 10:  GPM Sensor-Space Collection Unit Adjustable Parameters.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Data
MD2	SENSOR_SPACE_CU_ADJUSTABLE_PARAMETER_STORAGE_FILE	The variable length record carrying the storage of sensor-space adjustable parameter information for this dataset.	MD3- MD21	1	N/A	
MD3	INTERPOLATION_MODE	Flag indicating the interpolation mode for the parameters in this data set.
Value = 0
A value of 0 signifies nearest neighbor interpolation.
A value of 1 signifies interpolation as defined in Appendix B.
Values 2 through 65535 reserved.  Table of additional values and association with specific interpolation methods is TBD.		1	Unsigned short	2 bytes
MD4	COLLECTION_UNIT_PARAM_INDEX_FLAGS	Seventeen binary flags in order (ΔXM,ΔYM, ΔZM,ΔxC,ΔyC, ΔzC, θ1C , θ2C , θ3C, ΔrC, ΔxC rate,ΔyC rate, ΔzC rate, θ1C rate , θ2C rate , θ3C rate, ΔrC rate), starting at the lowest order bit, right to left,  that indicate which parameters are included in the current dataset-wide collection unit definition. (i.e., ΔXM bit position = 1, θ2C bit position = 8, etc.).  The 15 high-order bits are left zero.  Q is the number of collection unit parameters included (i.e., the sum of the binary flags).		1	Unsigned integer	4 byte storage (17 bits used) 
MD5	POST_PARAM_INDEX_FLAGS	Seven binary flags in order (ΔxP,ΔyP, ΔzP, θ1P , θ2P , θ3P, ΔrP), starting at the lowest order bit, right to left, that indicate which parameters are included in the current dataset-wide post definition. (i.e., ΔxP bit position = 1, θ3P bit position = 6, etc.).  The eighth bit is left zero. P is the number of post parameters included (i.e., the sum of the binary flags).		1	Unsigned char	1 byte storage (7 bits used) 
MD6	NUM_COLLECTION_UNITS	The number of collection units contained in this VLR.		1	Unsigned short	2 bytes
MD7	COLLECTION_UNIT_PARMETERS	This record contains the collection unit parameters for a specific collection unit in the dataset.
NOTE:  This record will be repeated from 1 to N times, where the value of N is specified by NUM_COLLECTION_UNITS.
	Lines MD8-MD21	N	N/A	
MD8	CU_Trajectory_ID	The value used to identify the particular trajectory (Flight Line) this CU covariance is associated with.  This correlates with the Point_Source_ID stored in the point records and in the GPM Master VLR.		1	int	4 bytes
MD9	COLLECTION_UNIT_ID	Collection Unit identification string unique to the CU these parameters are associated with as defined in the GPM Master VLR.		1	Char[128]	128 bytes
MD10	CU_PARAMETERS		Lines MD11- MD14			
MD11	PARAM_1	Value of the collection unit parameter 1 as defined by COLLECTION_UNIT_PARAM_INDEX_FLAGS.		1	float	4 bytes
MD12	PARAM_2	Value of the collection unit parameter 2 as defined by COLLECTION_UNIT_PARAM_INDEX_FLAGS.		1	float	4 bytes
MD13	PARAMS	Continuation of collection unit parameter values as defined by COLLECTION_UNIT_PARAM_INDEX_FLAGS, 4 bytes each.		k	floats	4 bytes each
MD14	PARAM_LAST	Value of the final collection unit parameter Q as defined by COLLECTION_UNIT_PARAM_INDEX_FLAGS.		1	float	4 bytes
MD15	POST_ADJUSTABLE_PARAMETERS	This part of the variable length record specifies the post adjustable parameters associated with this collection unit.	Lines MD16- MD21	1	N/A	
MD16	NUM_POSTS	The number of sensor-space posts associated with this collection unit. 		1	Unsigned short	2 bytes
MD17	POST_PARMETERS	This record contains the post parameters for a specific collection unit in the dataset.
NOTE:  This record will be repeated from 1 to MC times, where the value of MC is the number of posts in the current collection unit and is specified by NUM_POSTS.
	Lines MD18 – MD21	MC	N/A	
MD18	POST_PARAM_1	Value of post parameter 1 as defined by POST_PARAM_INDEX_FLAGS.		1	float	4 bytes
MD19	POST_PARAM_2	Value of post parameter 2 as defined by POST_PARAM_INDEX_FLAGS.		1	float	4 bytes
MD20	POST_PARAMS_CONTINUED	Continuation post parameter values as defined by POST_PARAM_INDEX_FLAGS, 4 bytes each.		L	floats	4 bytes each
MD21	POST_PARAM_LAST	Value of the final post parameter P as defined by POST_PARAM_INDEX_FLAGS, for this post location.		1	float	4 bytes

Table D - 11:  GPM Sensor-Space Collection Unit Adjustable Parameter BPF3 Bundled File Header Information.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	Variable		1	UInt32	4 bytes
H4	Filename	GPM_Sensor_CU_Adjustable_Params		1	Char[32]	32 bytes


GPM Sensor Collection Unit Covariance Record - Indirect
GPM accommodates two different methods of storing the sensor collection unit covariance information.  This section describes the indirect method, in which full covariance matrices for each collection unit and their posts are stored in block diagonal fashion.  Cross-covariance information among the CUs, and among posts within CUs, are determined using correlation models, whose parameters are also stored in the record.  The second method of covariance storage is the direct method, in which the full collection unit and post covariances—including cross-covariances—are all stored.  A separate record is described for each method below.
One of the key components of GPM-based error propagation is the covariance information for the GPM sensor parameters defined in Section 6.1.  This symmetric sensor covariance matrix is formed as shown below for a case of two collection units.  Note that each collection unit   has   posts associated with it.
 
Equation D - 4.  GPM Sensor Covariance Matrix.
In this matrix,  represents the collection unit   covariance matrix;   represents the   post covariance matrix within .  These are symmetric matrices, so only the diagonal and upper triangle elements are stored.  For indirect storage, the off-diagonal cross-covariance elements are computed using the correlation function parameters defined for each collection unit and post correlation group (see Section 6.1.1).  An example of encoding this data into an LAS variable length record is provided in the Table D-12 and Table D-13 below.  Storage in a BPF3 file simply involves using the header information in Table D-14 in place of Table D-12.

Table D - 12:  GPM Sensor Collection Unit Covariance VLR Header Information – Indirect.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	281		1	Unsigned short	2 bytes
H5	Record Length After Header	Variable		1	Unsigned short	2 bytes
H6	Description	GPM_Sensor_CU_Cov_Indirect		1	Char[32]	32 bytes

Table D - 13:  GPM Sensor Collection Unit Covariance Metadata – Indirect.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Data
MD2	SENSOR_COLLECTION_UNIT_INDIRECT_STORAGE_FILE	The variable length record carrying the indirect storage of sensor-space covariance information for this dataset.	MD3- MD36	1	N/A	
MD3	NUM_CU_CORR_GROUPS	The number of collection unit correlation groups contained in this VLR.		1	Unsigned short	2 bytes
MD4	GLOBAL_SPDCF_CU_CORRELATION_PARMETER	 
 
Parameters (A, α, β, τ) used to describe the correlation decrease between points as a function of delta time.  R is specified by NUM_CU_CORR_GROUPS.	Lines MD5-MD9	R	N/A	R * 20 bytes
MD5	CU_PARAM_INDEX_FLAGS	Seventeen binary flags in order (ΔXM,ΔYM, ΔZM, ΔxC,ΔyC, ΔzC, θ1C , θ2C , θ3C, ΔrC, ΔxC rate,ΔyC rate, ΔzC rate, θ1C rate , θ2C rate , θ3C rate, ΔrC rate), starting at the lowest order bit, right to left,  that indicate which parameters are included in the current correlation group. (i.e., ΔXM bit position = 1, θ2C bit position = 8, etc.).  The 15 high-order bits are left zero.		1	Unsigned integer	4 byte storage (17 bits used) 
MD6	PARAM_A	Parameter A controlling the maximum correlation that can be obtained.		1	float	4 bytes
MD7	PARAM_ALPHA	Parameter alpha (α) used with A to define the minimum correlation value that can be obtained.		1	float	4 bytes
MD8	PARAM_BETA	Parameter Beta (β), controlling the shape of the correlation curve and the speed of the decay.  		1	float	4 bytes
MD9	PARAM_TAU	Parameter Tau (τ), a time constant.		1	float	4 bytes
MD10	NUM_POST_CORR_GROUPS	The number of post correlation groups contained in this VLR.		1	Unsigned short	2 bytes
MD11	GLOBAL_SPCDF_POST_CORRELATION_PARMETER	 
 
Parameters (A, α, β, τ) used to describe the correlation decrease between posts as a function of delta time. S is specified by NUM_POST_CORR_GROUPS.	Lines MD12-MD16	S	N/A	S * 17 bytes
MD12	POST_PARAM_INDEX_FLAGS	Seven binary flags in order (Δx,Δy, Δz, θ1 , θ2 , θ3, Δr), starting at the lowest order bit, that indicate which parameters are included in the current correlation group. (i.e., Δx bit position = 1, θ3 bit position = 6, etc.).  The eighth bit is left zero.		1		1 byte storage (7 bits used) 
MD13	PARAM_A	Parameter A controlling the maximum correlation that can be obtained.		1	float	4 bytes
MD14	PARAM_ALPHA	Parameter alpha (α) used with A to define the  minimum correlation value that can be obtained.		1	float	4 bytes
MD15	PARAM_BETA	Parameter Beta (β), controlling the shape of the correlation curve and the speed of the decay.  		1	float	4 bytes
MD16	PARAM_TAU	Parameter Tau (τ), a time constant.		1	float	4 bytes
MD17	SS_COV_EPOCH_LIST	This part of the variable length record specifies the time t of each covariance epoch along with its associated error covariance.	Lines MD18- MD36	1	N/A	
MD18	NUM_CU_COV_RECORDS	The number of collection unit covariance records contained in this VLR.  One collection unit covariance record contains time and covariance data for a collection unit, as well as, time and covariance data for all of the CUs posts.		1	Unsigned short	2 bytes
MD19	CU_COV	This record contains the associated trajectory ID, the start and stop times and the associated symmetric error covariance for a specific collection unit in the dataset.  This is followed by from zero to M sets of post data.  This consists of a post time, followed by the post symmetric covariance data.  In all cases the upper-diagonal covariance matrix elements are stored in column major order .
NOTE:  This record will be repeated from 1 to N times, where the value of N is dependent on the number of collection units specified by NUM_CU_COV_RECORDS.
	Lines MD20 – MD28	N	N/A	
MD20	CU_Trajectory_ID	The value used to identify the particular trajectory (Flight Line) this CU covariance is associated with.  This is used in conjunction with a point’s Point Source ID to determine if a point is associated with this CU covariance.		1	int	4 bytes
MD21	COLLECTION_UNIT_ID	Collection Unit identification string unique to this CU as defined in the GPM Master VLR.		1	Char[128]	128 bytes
MD22	CU_START_TIME	The start time of a collection unit covariance.		1	double	8 bytes
MD23	CU_STOP_TIME	The stop time of a collection unit covariance.		1	double	8 bytes
MD24	Element_Index = 0	CU Covariance matrix element I = 0, J = 0		1	float	4 bytes
MD25	Element_Index = 1	CU Covariance matrix element I = 0, J = 1		1	float	4 bytes
MD26	Element_Index = 2	CU Covariance matrix element I = 1, J = 1		1	float	4 bytes
MD27		Continuation of Covariance matrix elements, including post covariance matrix elements, 4 bytes each.				
MD28	End Element_Index	Final CU covariance matrix element for this CU, I = Q, J = Q.		1	float	4 bytes
MD29	NUM_POSTS_THIS_COLLECTION_UNIT	The number, MC, of sensor-space posts associated with this collection unit.  Each post identified by a specific time.		1	Unsigned short	2 bytes
MD30	POST_COV	This record contains the posts associated with a specific collection unit in the dataset.  This is followed by from zero to MC sets of post data.  This consists of a post time, followed by the post symmetric covariance data.  In all cases the covariance matrix elements are stored in column major order.
NOTE:  This record will be repeated from 1 to MC times, where the value of MC is dependent on the number of posts specified by NUM_POSTS_THIS_COLLECTION_UNIT.
	Lines MD31 – MD36	MC	N/A	
MD31	POST_TIME	The time for this post in this collection unit.		1	double	8 bytes
MD32	Element_Index = 0	Post covariance matrix element I = 0, J = 0		1	float	4 bytes
MD33	Element_Index = 1	Post covariance matrix element I = 0, J = 1		1	float	4 bytes
MD34	Element_Index = 2	Post covariance matrix element I = 1, J = 1		1	float	4 bytes
MD35		Continuation of post covariance matrix elements, 4 bytes each.				
MD36	End Element_Index	Final Post covariance matrix element for this CU, I = P, J =P.		1	float	4 bytes

Table D - 14:  GPM Sensor Collection Unit Covariance BPF3 Bundled File Header Information – Indirect.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	Variable		1	UInt32	4 bytes
H4	Filename	GPM_Sensor_CU_Cov_Indirect		1	Char[32]	32 bytes

GPM Collection Unit Covariance Record – Direct
For the direct method of storing collection unit (CU) covariance information, the full covariance among N CUs is stored.  Each collection unit may also contain covariance information for MC post locations, where C is the index of the CU in which the posts reside.  The full covariance matrix contains the covariance components for each collection unit and their respective posts, as well as all of the cross-covariance terms.  An example of this is illustrated in Equation D-5.  Each collection unit matrix along the diagonal represents the covariance among the up to 14 adjustable parameters for 1 to N CUs.  Each CU matrix is followed by zero to MC post matrices.   Each post matrix represents the covariance among the up to 7 adjustable parameters.  The remainder of the full covariance matrix is populated with the appropriate cross-covariance terms.  The CU and post parameters included are those defined by the sensor adjustable parameter flags in Table D - 10.  The minimum CU record would contain covariance information for one collection unit with zero posts.  A typical CU record would define covariance information for multiple CUs, each with a different number of posts.  Table D-15 and Table D-16 lists the components of the sensor covariance record using the direct method in LAS VLR format.  Storage in BPF3 file makes use of the header information in Table D-17 in place of Table D-15

 
Equation D - 5.  Full covariance among 2 collection units.
Table D - 15:  Sensor Collection Unit Covariance VLR Header Information – Direct.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	282		1	Unsigned short	2 bytes
H5	Record Length After Header	Variable		1	Unsigned short	2 bytes
H6	Description	GPM_Sensor_CU_Cov_Direct		1	Char[32]	32 bytes

Table D - 16:  Sensor Collection Unit Covariance Metadata – Direct.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Data
MD2	SENSOR_COLLECTION_UNIT_DIRECT_STORAGE_FILE	The variable length record carrying the direct storage of sensor-space Collection Unit covariance information for this dataset.	MD3 –MD17	1	N/A	
MD3	NUM_COLLECTION_UNITS	The number, N, of sensor-space collection units contained in this VLR.  Each collection unit is associated with a trajectory ID, a CU time and may have up to MC posts.  Each post is associated with a specific time.		1	Unsigned short	2 bytes
MD4	SS_CU_EPOCH_LIST	This part of the variable length record specifies the list of times and trajectory IDs of each collection unit covariance epoch. Followed by the number and times of each post associated with a given collection unit.  The order of the CU epochs in the list is the order of the CU covariance matrices along the block diagonal of the full covariance matrix .
NOTE:  This record will be repeated from 1 to N times, where the value of N is dependent on the number of collection units specified by NUM_COLLECTION_UNITS.	Lines MD5 –MD10	N	N/A	
MD5	CU_Trajectory_ID	The value used to identify the particular trajectory (Flight Line) this CU covariance is associated with.  This is used in conjunction with the Point Source ID in a point record to determine if a point is associated with this CU.		1	int	4 bytes
MD6	COLLECTION_UNIT_ID	Collection Unit identification string unique to this CU as defined in the GPM Master VLR.		1	Char[128]	128 bytes
MD7	CU_START_TIME	The start time of a collection unit covariance.		1	double	8 bytes
MD8	CU_STOP_TIME	The stop time of a collection unit covariance.		1	double	8 bytes
MD9	NUM_POSTS_THIS_COLLECTION_UNIT	The number, MC, of sensor-space posts associated with this collection unit.  Each post is identified by a specific time.		1	Unsigned short	2 bytes
MD10	POST_TIME	The time for this post in this collection unit.		MC	double	8 bytes
MD11	CU_COV	Data represents the CU covariance matrices (see Section 6.) for each CU covariance epoch along the diagonal (along with any posts associated with each CU), and the cross-covariance matrices.  The data is stored in column major order.  The full matrix is symmetric and only the upper (block) triangular portion is stored.	Lines MD12 –MD17	1	N/A	
MD12	Element_Index = 0	CU Covariance matrix element I = 0, J = 0		1	float	4 bytes
MD13	Element_Index = 1	CU Covariance matrix element I = 0, J = 1		1	float	4 bytes
MD14	Element_Index = 2	CU Covariance matrix element I = 1, J = 1		1	float	4 bytes
MD15	Element_Index = 3	CU Covariance matrix element I = 0, J = 2		1	float	4 bytes
MD16		Continuation of Covariance matrix elements, including post covariance matrix elements, 4 bytes each.				
MD17	End Element_Index 
	Final covariance matrix element.		1	float	4 bytes
 

Table D - 17:  GPM Sensor Collection Unit Covariance BPF3 Bundled File Header Information – Direct.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	Length of this bundled file data following this header.
Variable bytes		1	UInt32	4 bytes
H4	Filename	GPM_Sensor_CU_Cov_Direct		1	Char[32]	32 bytes

Time Reference Grid Storage Format
This section defines the encoding of the Time Reference Grid metadata that can be utilized in Sensor-Space GPM in place of storing per-point times in the point records.  When a Time Reference Grid exists for a collection unit (CU), the time associated with a point in the point cloud will be determined based on a nearest-neighbor interpolation from the three-dimensional Time Reference Grid.  A description of an LAS variable length record (VLR) to store such a grid is provided in Table D-18 and Table D-19 below.  Encoding the data in a BPF3 file involves implementing the header information defined in Table D-20 followed by metadata in Table D-18.  
Table D-18:  LAS Variable Length Record Header Information for the Time Reference Grid.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	279		1	Unsigned short	2 bytes
H5	Record Length After Header	Variable depending on number of CUs with a Time Reference Grid and number of posts per each grid.		1	Unsigned short	2 bytes
H6	Description	Time_Reference_Grid		1	Char[32]	32 bytes

Table D-19:  Time Reference Grid VLR Metadata Information.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Metadata
MD2	TIME_REF_GRID_FILE	The variable length record carrying the Time Reference Grid information for a collection unit.	MD3-MD35	1	N/A	
MD3	NUM_TIME_REF_GRID_RECORDS	The number of Time Reference Grid records being represented in this VLR.  This number would be limited to the number of collection units (N) in the specific file.  Note: There may be cases where not all of the collection units in a file have a Time Reference Grid, so N can be less than the number of CUs.		1	Unsigned short	2 bytes
MD4	TIME_REF_GRID_RECORD	This portion of the VLR stores the Time Reference Grid metadata for a specific collection unit (1…N) and can repeat up to N times.	MD5-MD35	N	N/A	
MD5	TRAJECTORY_ID	The unique identifier for the given collection unit of interest.  This field only applies to Sensor-Space GPM and is associated with the Point Source ID stored per point record.  Neither this field nor this VLR apply to Ground-Space GPM.		1	Int	4 bytes
MD6	COLLECTION_UNIT_ID	Collection Unit identification string unique to this CU as defined in the GPM Master VLR.		1	Char[128]	128 bytes
MD7	TIME_REF_GRID_DEF	The definition of the Time Reference Grid for a given collection unit based on the origin, axis orientation, and number of posts per dimension.	MD8-MD19	1	N/A	
MD8	TIME_REF_GRID_ORIGIN_X	The x coordinate in MCS (x, y, z) space describing the location of the origin of the Time Reference Grid coordinate system.		1	double	8 bytes
MD9	TIME_REF_GRID_ORIGIN_Y	The y coordinate in MCS (x, y, z) space describing the location of the origin of the Time Reference Grid coordinate system.		1	double	8 bytes
MD10	TIME_REF_GRID_ORIGIN_Z	The z coordinate in MCS (x, y, z) space describing the location of the origin of the Time Reference Grid coordinate system.		1	double	8 bytes
MD11	TIME_ROT_THETA_X	The rotation angle θT,x (in milliradians) that is used in conjunction with θT,y and θT,z to rotate from the MCS (x,y,z) coordinate system to the uT,vT,wT system, where uT,vT,wT define the axes associated with the Time Reference Grid.   This is a rotation about the x-axis (counter-clockwise positive). The rotation sequence is applied as defined in Section 3.2.1.		1	double	8 bytes
MD12	TIME _ROT_THETA_Y	The rotation angle θT,y(in milliradians) that is used in conjunction with θT,x and θT,z to rotate from the MCS (x,y,z) coordinate system to the uT,vT,wT system, where uT,vT,wT define the axes associated with the Time Reference Grid.  This is a rotation about the y-axis (counter-clockwise positive).  The rotation sequence is applied as defined in Section 3.2.1.		1	double	8 bytes
MD13	TIME _ROT_THETA_Z	The rotation angle θT,z(in milliradians) that is used in conjunction with θT,x and θT,y to rotate from the MCS x,y,z coordinate system to the uT,vT,wT system, where uT,vT,wT define the axes associated with the Time Reference Grid.  This is a rotation about the z-axis (counter-clockwise positive).  The rotation sequence is applied as defined in Section 3.2.1.		1	double	8 bytes
MD14	TIME_REF_GRID_STEP_UT	The step size (post-spacing) in meters for the Time Reference Grid in the uT dimension of the local uT,vT,zT coordinate system.		1	float	4 bytes
MD15	TIME_REF_GRID_STEP_VT	The step size (post-spacing) in meters for the Time Reference Grid in the vT dimension of the local uT,vT,zT coordinate system.		1	float	4 bytes
MD16	TIME_REF_GRID_STEP_WT	The step size (post-spacing) in meters for the Time Reference Grid in the wT dimension of the local uT,vT,zT coordinate system.		1	float	4 bytes
MD17	TIME_REF_GRID_POSTS_UT	Specifies the number of posts in the Time Reference Grid in the uT direction (PuT).		1	Unsigned integer	4 bytes
MD18	TIME_REF_GRID_POSTS_VT	Specifies the number of posts in the Time Reference Grid in the vT direction (PvT).		1	Unsigned integer	4 bytes
MD19	TIME_REF_GRID_POSTS_WT	Specifies the number of posts in the Time Reference Grid in the wT direction (PwT).		1	Unsigned integer	4 bytes
MD20	TIME_REF_GRID_TIME_POSTS	This section defines the actual time associated with each post location within the Time Reference Grid.  The grid origin is defined as I=0, J=0, K=0 or (0,0,0) where I refers to the post index along the uT axis, J refers to the post index along the vT axis, and K refers to the post index along the wT axis.  It steps along the uT axis until the number of posts in uT is reached (I=PuT).  It then steps to the next element in vT (0,1,0) and repeats stepping from element (0,1,0) to element (PuT-1,1,0). This growth continues along uT and vT until element (PuT-1,PvT-1,0), at which time it steps to element (0,0,1) and then proceeds to progress along I (uT) followed by J (vT) in the K=1 (wT) plane.  This process continues (steps in I, followed by incremental steps in J, followed by incremental steps in K) until reaching element (PuT-1,PvT-1, PwT-1)  	MD21-MD35	P where P=(PuT X PvT x PwT)	N/A	
MD21	Element_Index = 0	Time Reference Grid element I=0, J=0, K=0		1	double	8 bytes
MD22	Element_Index = 1	Time Reference Grid element I=1, J=0, K=0		1	double	8 bytes
MD23		Continuation of increases to index I to increase the position along the uT axis until element PuT-1 is reached.				
MD24	Element_Index = PuT-1	Time Reference Grid element I= PuT-1, J=0, K=0		1	double	8 bytes
MD25	Element_Index = PuT	Time Reference Grid element I= 0, J=1, K=0		1	double	8 bytes
MD26	Element_Index = PuT+1	Time Reference Grid element I= 1, J=1, K=0		1	double	8 bytes
MD27		Continuation of increases to index I to increase the position along the uT axis, followed by incremental increases to J to increase position along the vT axis until element (PuT-1, PvT-1, 0)  is reached.				
MD28	Element_Index = (PuT x PvT)-1	Time Reference Grid element I= PuT-1, J= PvT-1, K=0		1	double	8 bytes
MD29	Element_Index = (PuT x PvT)	Time Reference Grid element I= 0, J= 0, K=1		1	double	8 bytes
MD30	Element_Index = (PuT x PvT)+1	Time Reference Grid element I= 1, J= 0, K=1		1	double	8 bytes
MD31		Continuation of increases to index I to increase the position along the uT axis, followed by incremental increases to J to increase position along the vT axis until element (PuT-1, PvT-1,1)  is reached.				
MD32	Element_Index = (PuT x PvT x 2)-1	Time Reference Grid element I= PuT-1, J= PvT-1, K= 1		1	double	8 bytes
MD33	Element_Index = (PuT x PvT x 2)	Time Reference Grid element I= 0, J= 0, K= 2		1	double	8 bytes
MD34		Continuation of increases to index I to increase the position along the uT axis, followed by incremental increases to J to increase position along the vT axis, followed by incremental increases to K to provide incremental increases to the position along the wT axis until element (PuT-1, PvT-1, PwT-1)  is reached.	 			
MD35	End Element_Index = (PuT x PvT x PwT)-1	Time Reference Grid element I= PuT-1, J= PvT-1, K= PwT-1		1	double	8 bytes
 

Table D-20:  BPF3 ULEM Bundled File Header Information for Time Reference Grid.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	Variable depending on number of CUs with a Time Reference Grid and number of posts per each grid.		1	UInt32	4 bytes
H4	Filename	Time_Reference_Grid		1	Char[32]	32 bytes





 

Appendix E : Ground-Space GPM Storage Format

In Ground-Space GPM, the adjustable parameters are translations associated with the anchor point locations within the dataset, and Collection Unit-wide three-dimensional conformal (3DC) transformation parameters (the definition of collection unit (CU) for Ground-Space GPM is the entire dataset).   The reasoning for implementing a model to accommodate ground-space adjustable parameters and error propagation is that it can be applied in cases where the complexity of the point-cloud collection and processing concept of operations precludes a straightforward definition of a sensor-space projective model or when a modality other than lidar is used to create the point cloud dataset, in which case a sensor-space representation is not appropriate.
This appendix describes how the components of the Ground-Space GPM can be stored in LAS or BPF3 file formats.  Ground-Space GPM is designed to accommodate storage for both collection unit and anchor point adjustable parameters, along with their associated covariance matrices.  The storage is flexible so as to permit 3DC parameters, anchor point-only parameters, or both 3DC and anchor point parameters.  Two different storage formats are defined.  One permits the indirect storage of anchor point cross-covariance parameters, the other permits direct storage of the anchor point cross-covariance parameters.  Both formats require storage of the full 3DC parameter covariance matrix.  For either storage option, the 3DC and/or anchor point metadata are contained in an LAS variable length record (VLR), or in a BPF3 bundled file.
Since both storage definitions provide the flexibility to use/store only a subset of the 3DC adjustable parameters (e.g. only translations), “active” parameters are identified with an index flag by setting individual bits in a single byte to one to indicate which adjustable parameters are included.  If all bits are set to zero, no 3DC parameters are defined and only anchor point adjustable parameters are included.
In the case of anchor point indirect storage, formatting is defined for the 3D coordinates along with the six unique elements of the symmetric covariance matrix associated with each anchor point in a metadata record.  The number of anchor points is specified in a field, and if it is set to zero, no anchor points are defined and only 3DC adjustable parameter values and covariance matrices are included.  A set of global values, applying to the entire dataset (CU), are also stored in the metadata record.  These global values consist of an interpolation mode flag and a set of CSM correlation function parameters that apply to the entire data set.  The storage accommodates assigning adjustable parameters to correlation groups, with each group having separate correlation parameters.  The groups are identified with an index flag by setting the bits in a single byte to one to indicate which adjustable parameters are grouped together (similar to the parameter index flag defined in Appendix D).  
The indirect method for encoding this 3DC and anchor point adjustable parameter and covariance data (along with 3D position and global information for the anchor points) into an LAS VLR  is provided in Table E - 3 and Table E - 4.  Table E - 3 defines the VLR header information for the indirect storage method. Table E - 4 defines the VLR metadata for carrying the 3DC and anchor point information using the indirect storage method.  A modification to the record header information permits this same metadata to be stored as a bundled file in a BPF3 file.  The definition of the BPF3 GPM base header and bundled file header information for the indirect storage method is contained in Table E - 5.  The remainder of the BPF3 bundled file would be the same as defined in Table E - 4.

For the case of 3DC and anchor point adjustable parameter and covariance direct storage, a single   symmetric covariance matrix is stored, where   corresponds to the number of 3DC parameters included and   corresponds to the number of anchor points defined for the data set.  In the same fashion as for indirect storage, the number of anchor points is specified, and if it is set to zero, no anchor points are defined and only 3DC adjustable parameters are included.  Also stored in the VLR are the interpolation mode flag, a global transform parameter, and the 3D coordinates for each anchor point.  Table E - 6 defines the VLR header information for the direct storage method.  Table E - 7 defines the VLR metadata carrying the 3DC and anchor point information using the direct storage method for the dataset.  Variance-covariance values are stored in column major order.  This is depicted in Equation E - 2.  A modification to the record header information permits this same metadata to be stored as a bundled file in a BPF3 file.  The definition of the BPF3 GPM bundled file header information for the direct storage method is contained in Table E - 8.  The remainder of the BPF3 bundled file would be the same as defined in Table E - 7.  The BPF3 GPM base header information will be inherited from the parent BPF3 file.  If no GPM file additions are included in the parent BPF3 file, the GPM base header will be zero-filled, except for the magic number field.  In some cases, particularly the direct storage of cross-covariance parameters, the number of parameters to be stored can be quite large, and may exceed the maximum storage size for an LAS 1.2/1.3 VLR.  In such a case, LAS version 1.4 could be used, leveraging its EVLR (Extended VLR) storage space. 
Throughout this appendix, where not specified, all positional and distance units are in meters, and all angular units are in milliradians.  In accordance with both the LAS and BPF specifications, all data is in little-endian format.
It should be noted that the points in Tables E-1 and E-2 are in the native coordinate system used in the LAS/BPF file, which may not be the same as the MCS.  In these cases, the point coordinates must be converted to the MCS prior to exploitation with the GPM model. 

Table E - 1:  GPM Ground-Space Point Record (LAS).
ID	Parameter	Definition	Obl. LAS1.3	Description	Name/Role Name
1	Point x record	The x position of a specific point. 	M	The x position of point cloud point stored per point record.  This value is used in combination with the x Scale Factor and x Offset to determine the x coordinate of a given point.	LASF_X
2	Point y record	The y position of a specific point. 	M	The y position of point cloud point stored per point record.  This value is used in combination with the y Scale Factor and y Offset to determine the y coordinate of a given point.	LASF_Y
3	Point z record	The z position of a specific point.	M	The z position of point cloud point stored per point record.  This value is used in combination with the z Scale Factor and z Offset to determine the z coordinate of a given point.	LASF_Z
4	PPE LUT index	Per Point Error (PPE) Look-up table index 	User Defined	A pointer providing the index into the Per Point Error (PPE) Look-up Table (LUT) that provides for the retrieval of the PPE covariance associated with a given point.  
When LAS1.4 is adopted within the community, the PPE_LUT_Index will be added as a user defined addition to each point record and  documented within the LAS1.4 using the EXTRA_BYTES VLR.  
When LAS 1.2 or 1.3 is being used, then the “USER DATA” field is used to store the PPE_LUT_index.  This limits the number of LUT covariance entries to 256.  If this is not adequate, then LAS 1.4 must be adopted to meet the requirement for additional covariance.
	PPE_LUT_Index



Table E - 2:  GPM Ground Space Point Record (BPF3)
ID	Parameter	Definition	Obl. BPF3	Description	BPF3 Label
1	Point x record	The x position of a specific point. 	M	The x position of the point cloud point stored in the point data.  This value is used in combination with the x Offset from the metadata subheader and the transform from the header to determine the x coordinate of a given point.	X
2	Point y record	The y position of a specific point. 	M	The y position of the point cloud point stored in the point data.  This value is used in combination with the y Offset from the metadata subheader and the transform from the header to determine the y coordinate of a given point.	Y
3	Point z record	The z position of a specific point.	M	The z position of the point cloud point stored in the point data.  This value is used in combination with the z Offset from the metadata subheader and the transform from the header to determine the z coordinate of a given point.	Z
4	PPE LUT index	Per Point Error (PPE) Look-up table index 	User Defined	A pointer providing the index into the Per Point Error (PPE) Look-up Table that provides for the retrieval of the PPE covariance associated with a given point.  	PPE_LUT_Index
Note:  This is a user defined dimension in BPF3 and will have a label of “PPE_LUT_Index” within the metadata subheader.


Table E - 3:  LAS Variable Length Record Header Information for Ground-Space with Indirect Storage of Anchor PointData.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	274		1	Unsigned short	2 bytes
H5	Record Length After Header	Variable number of bytes		1	Unsigned short	2 bytes
H6	Description	GPM_GndSpace_Indirect		1	Char[32]	32 bytes

Table E - 4:  LAS Variable Length Record Metadata Definition for Ground-Space with Indirect Storage of Anchor Point Data.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Metadata
MD2	GROUND_SPACE_WITH_ANCHOR_POINT_INDIRECT_STORAGE_FILE	The variable length record carrying the Ground-Space 3DC storage and/or indirect storage of anchor point information for this dataset.	MD3-MD60	1	N/A	
MD3	DATASET_ID	Dataset identification string as defined in the GPM Master VLR and used as the primary identifier for Ground Space GPM		1	Char[128]	128 bytes
MD4	GROUND_SPACE_3DC_UNIT_PARAMETERS	This part of the record carries the 3DC storage information for this dataset.	MD5-MD21	1	N/A	
MD5	3DC_PARAM_INDEX_FLAGS	Seven binary flags in order (Δx, Δy, Δz, ω, , , Δs), starting at the lowest order bit, right to left, that indicate which parameters are included in the current dataset-wide post definition. (i.e., Δx bit position = 1,  bit position = 6, etc.).  The eighth bit is left zero. C is the number of 3DC parameters included (i.e., the sum of the binary flags).
If all bits are set to zero, no additional 3DC parameter information is included in the record.		1	Unsigned char	1 byte storage (7 bits used)
MD6	3DC_NORMALIZATION_PARAMETERS	This part of the record carries three re-centering and one scaling factor parameters for the collection unit.	MD7-MD10	1	N/A	
MD7	CU_X_COORD_RE_CENTERING_VALUE	Re-centering value for the CU X coordinate.		1	double	8 bytes
MD8	CU_Y_COORD_RE_CENTERING_VALUE	Re-centering value for the CU Y coordinate.		1	double	8 bytes
MD9	CU_Z_COORD_RE_CENTERING_VALUE	Re-centering value for the CU Z coordinate.		1	double	8 bytes
MD10	CU_S_NORMALIZING_SCALE_FACTOR_VALUE	CU normalizing scale factor.		1	double	8 bytes
MD11	3DC_ADJUSTABLE_PARAMETERS	This part of the record carries the values of the 3DC adjustable parameters for the collection unit, as defined by the 3DC_PARAM_INDEX_FLAGS.	MD12-MD14	1	N/A	
MD12	PARAM_1	Value of 3DC parameter 1 as defined by 3DC_PARAM_INDEX_FLAGS.		1	double	8 bytes
MD13	PARAMS	Continuation of 3DC parameter values as defined by 3DC_PARAM_INDEX_FLAGS.		k	double	8 bytes
MD14	PARAM_LAST	Value of the final 3DC parameter (C) as defined by 3DC_PARAM_INDEX_FLAGS.		1	double	8 bytes
MD15	3DC_COVARIANCE_PARAMETERS	Data represents the CU covariance matrix.  The data is stored in column major order.  The full matrix is symmetric and only the upper (block) triangular portion is stored.  The letters I and J below represent indices (respectively) into the full matrix.	MD15-MD21	1	N/A	
MD16	Element_Index = 0	CU Covariance matrix element I = 0, J = 0		1	float	4 bytes
MD17	Element_Index = 1	CU Covariance matrix element I = 0, J = 1		1	float	4 bytes
MD18	Element_Index = 2	CU Covariance matrix element I = 1, J = 1		1	float	4 bytes
MD19	Element_Index = 3	CU Covariance matrix element I = 0, J = 2		1	float	4 bytes
MD20		Continuation of Covariance matrix elements, 4 bytes each.			floats	4 bytes each
MD21	End_Element_Index	CU final covariance matrix element I = C-1, J = C-1		1	float	4 bytes
MD22	ANCHOR_POINT_INDIRECT_STORAGE	This part of the record carries the indirect storage of anchor point information for this dataset.	MD23-MD60	1	N/A	
MD23	NUM_AP_RECORDS	The number of anchor point covariance records contained in this VLR.
If this value is equal to zero, nothing follows in this VLR.		1	Unsigned short	2 bytes
MD24	INTERPOLATION_MODE	Flag indicating the interpolation mode for the parameters in this data set.
Value = 0
A value of 0 signifies nearest neighbor interpolation.
A value of 1 signifies interpolation as defined in Appendix B.
Values 2 through 65535 reserved.  Table of additional values and association with specific interpolation methods is TBD.		1	Unsigned short	2 bytes
MD25	INTERP_NUM_POSTS	When INTERPOLATION_MODE is set to 1, INTERP_NUM_POSTS specifies the number of posts (n) to be used in the  interpolation as defined in Appendix B.
If INTERPOLATION_MODE is set to 0, then INTERP_NUM_POSTS should be set to 1.
If INTERPOLATION_MODE is set to something other than 0 or 1, then the default for INTERP_NUM_POSTS will be 0.
		1	Unsigned short	2 bytes
MD26	DAMPENING_PARAM	The Dampening Parameter “D” used when defining the normalizing scale factor when INTERPOLATION_MODE is set to 1.  If INTERPOLATION_MODE is set to a value other than 1, the DAMPENING_PARAM will be set to 0.		1	double	8 bytes
MD27	NUM_CORR_GROUPS	The number of correlation groups contained in this VLR.		1	Unsigned short	2 bytes
MD28	CORRELATION_GROUP_PARAMETERS	Parameters that describe the correlation for this group of adjustable parameters.

NOTE:  This record will be repeated from 1 to NGRPS times, where the value of NGRPS is specified by NUM_CORR_GROUPS.	MD29-MD47	NGRPS	N/A	
MD29	CORR_GROUP_INDEX_FLAG	Three binary flags that indicate which parameters are included in the current correlation group such that Δx bit position = 1, Δy bit position = 2, Δz bit position = 3.  The bits 4 through eight are set to zero.		1		1 byte storage (3 bits used) 
MD30	CORR_ROT_THETA_X	The rotation angle θx(in milliradians) that is used in conjunction with θy and θz to rotate from the local x,y,z coordinate system to the u,v,w system consistent with the correlation directions.  The rotation sequence is applied as defined in Section 3.2.1.		1	double	8 bytes
M31	CORR_ROT_THETA_Y	The rotation angle θy (in milliradians) that is used in conjunction with θx and θz to rotate from the local x,y,z coordinate system to the u,v,w system consistent with the correlation directions.  The rotation sequence is applied as defined in Section 3.2.1.		1	double	8 bytes
M32	CORR_ROT_THETA_Z	The rotation angle θz (in milliradians) that is used in conjunction with θx and θy to rotate from the local x,y,z coordinate system to the u,v,w system consistent with the correlation directions.  The rotation sequence is applied as defined in Section 3.2.1.		1	double	8 bytes
MD33	GLOBAL_SPCDF_CORRELATION_PARMETER_U	 
 
Parameters (A, α, β, D) used to describe the correlation decrease between points as a function of distance  .
Lines MD34-MD37	1	N/A	
MD34	PARAM_A_ U	Parameter   controlling the maximum correlation that can be obtained (ideally 1).		1	float	4 bytes
MD35	PARAM_ALPHA_ U	Parameter alpha ( ) contributing to the minimum correlation value that can be obtained.		1	float	4 bytes
MD36	PARAM_BETA_ U	Parameter Beta ( ), controlling the shape of the correlation curve and the speed of the decay.  		1	float	4 bytes
MD37	PARAM_D_ U	Parameter  , a distance constant.
	1	float	4 bytes
MD38	GLOBAL_SPCDF_CORRELATION_PARMETER_V	 
 
Parameters (A, α, β, D) used to describe the correlation decrease between points as a function of distance  .
Lines MD39-MD42	1	N/A	
MD39	PARAM_A_ V	Parameter   controlling the maximum correlation that can be obtained (ideally 1).		1	float	4 bytes
MD40	PARAM_ALPHA_ V	Parameter alpha ( ) contributing to the minimum correlation value that can be obtained.		1	float	4 bytes
MD41	PARAM_BETA_ V	Parameter Beta ( ), controlling the shape of the correlation curve and the speed of the decay.  		1	float	4 bytes
MD42	PARAM_D_ V	Parameter  , a distance constant.
	1	float	4 bytes
M43	GLOBAL_SPCDF_CORRELATION_PARMETER_W	 
 
Parameters (A, α, β, D) used to describe the correlation decrease between points as a function of distance  .
Lines MD44-MD47	1	N/A	
MD44	PARAM_A_W	Parameter   controlling the maximum correlation that can be obtained (ideally 1).		1	float	4 bytes
MD45	PARAM_ALPHA_W	Parameter alpha ( ) contributing to the minimum correlation value that can be obtained.		1	float	4 bytes
MD46	PARAM_BETA_ W	Parameter Beta ( ), controlling the shape of the correlation curve and the speed of the decay.  		1	float	4 bytes
MD47	PARAM_D_ W	Parameter  , a distance constant.
	1	float	4 bytes
MD48	AP_PARAM_AND_COV_LIST	This record contains the Anchor Point (AP) information.  It includes the x, y, z location, the x, y, and z adjustable parameter values and the associated error covariance for a specific location in the dataset.
NOTE:  This record will be repeated from 1 to N times, where the value of N is dependent on the number of anchor points required to accurately model changes in the covariance and is specified by NUM_AP_RECORDS.	Lines MD49-MD60	N	N/A	
MD49	AP_X	The x coordinate in local Cartesian (x, y, z) space describing the location that the subsequent error covariance is referenced to.		1	double	8 bytes
MD50	AP_Y	The y coordinate in local Cartesian (x, y, z) space describing the location that the subsequent error covariance is referenced to.		1	double	8 bytes
MD51	AP_Z	The z coordinate in local Cartesian (x, y, z) space describing the location that the subsequent error covariance is referenced to.		1	double	8 bytes
MD52	AP_DELTA_X	The x coordinate adjustable parameter value.		1	float	4 bytes
MD53	AP_DELTA_Y	The y coordinate adjustable parameter value.		1	float	4 bytes
MD54	AP_DELTA_Z	The z coordinate adjustable parameter value.		1	float	4 bytes
MD55	AP_VARX	The variance in the x dimension for the ground covariance matrix in local Cartesian (x, y, z) space describing the error covariance at a point.		1	float	4 bytes
MD56	AP_VARY	The variance in the y dimension for the ground covariance matrix in local Cartesian (x, y, z) space describing the error covariance at a point.		1	float	4 bytes
MD57	AP_VARZ	The variance in the z dimension for the ground covariance matrix in local Cartesian (x, y, z) space describing the error covariance at a point.		1	float	4 bytes
MD58	AP_COVXY	The covariance between the x and y dimensions for the ground covariance matrix in local Cartesian (x, y, z) space describing the error covariance at a point.		1	float	4 bytes
MD59	AP_COVXZ	The covariance between the x and z dimensions for the ground covariance matrix in local Cartesian (x, y, z) space describing the error covariance at a point.		1	float	4 bytes
MD60	AP_COVYZ	The covariance between the y and z dimensions for the ground covariance matrix in local Cartesian (x, y, z) space describing the error covariance at a point.		1	float	4 bytes



Table E - 5:  BPF3 ULEM Bundled File Header Information for Ground-Space with Indirect Storage of Anchor Point Data.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	Length of this bundled file data following this header.
Variable.		1	UInt32	4 bytes
H4	Filename	GPM_GndSpace_Indirect		1	Char[32]	32 bytes



Table E - 6:  LAS Variable Length Record Header Information for Ground-Space with Direct Storage of Anchor Point Data.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	275		1	Unsigned short	2 bytes
H5	Record Length After Header	Variable
		1	Unsigned short	2 bytes
H6	Description	GPM_GndSpace_Direct		1	Char[32]	32 bytes


Table E - 7:  LAS Variable Length Record Metadata Definition for Ground-Space with Direct Storage of Anchor Point Data.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Metadata
MD2	GROUND_SPACE_WITH_ANCHOR_POINT_DIRECT_STORAGE_FILE	The variable length record carrying the Ground-Space 3DC storage and/or direct storage of anchor point information for this dataset.	MD3-MD33	1	N/A	
MD3	DATASET_ID	Dataset identification string as defined in the GPM Master VLR and used as the primary identifier for Ground Space GPM		1	Char[128]	128 bytes
MD4	GROUND_SPACE_3DC_PARAMETERS	This part of the record carries the 3DC storage information for this dataset.	MD5-MD14	1	N/A	
MD5	3DC_PARAM_INDEX_FLAGS	Seven binary flags in order (Δx, Δy, Δz, , , , Δs), starting at the lowest order bit, right to left, that indicate which 3DC parameters are to be included. (i.e., Δx bit position = 1,  bit position = 6, etc.).  The eighth bit is left zero. C is the number of 3DC parameters included (i.e., the sum of the binary flags).
If all bits are set to zero, no additional 3DC parameter information is included in the record.		1	Unsigned char	1 byte storage (7 bits used)
MD6	3DC_NORMALIZATION_PARAMETERS	This part of the record carries three re-centering and one scaling factor parameters for the collection unit.	MD7-MD10	1	N/A	
MD7	CU_X_COORD_RE_CENTERING_VALUE	Re-centering value for the CU X coordinate.		1	double	8 bytes
MD8	CU_Y_COORD_RE_CENTERING_VALUE	Re-centering value for the CU Y coordinate.		1	double	8 bytes
MD9	CU_Z_COORD_RE_CENTERING_VALUE	Re-centering value for the CU Z coordinate.		1	double	8 bytes
MD10	CU_S_NORMALIZING_SCALE_FACTOR_VALUE	CU normalizing scale factor.		1	double	8 bytes
MD11	3DC_ADJUSTABLE_PARAMETERS	This part of the record carries the values of the 3DC adjustable parameters for the collection unit, as defined by the 3DC_PARAM_INDEX_FLAGS.	MD12-MD14	1	N/A	
MD12	PARAM_1	Value of 3DC parameter 1 as defined by 3DC_PARAM_INDEX_FLAGS.		1	double	8 bytes
MD13	PARAMS	Continuation of 3DC parameter values as defined by 3DC_PARAM_INDEX_FLAGS.		k	double	8 bytes
MD14	PARAM_LAST	Value of the final 3DC parameter C as defined by 3DC_PARAM_INDEX_FLAGS.		1	double	8 bytes
MD15	ANCHOR_POINT_DIRECT_STORAGE	This part of the record carries the direct storage of anchor point information for this dataset.	MD16-MD33	1	N/A	
MD16	NUM_AP_RECORDS	The number of anchor point location records contained in this VLR.		1	Unsigned short	2 bytes
MD17	INTERPOLATION_MODE	Flag indicating the interpolation mode for the parameters in this data set.
Value = 0
A value of 0 signifies nearest neighbor interpolation.
A value of 1 signifies interpolation as defined in Appendix B.
Values 2 through 65535 reserved.  Table of additional values and association with specific interpolation methods is TBD.		1	Unsigned short	2 bytes
MD18	INTERP_NUM_POSTS	When INTERPOLATION_MODE is set to 1, INTERP_NUM_POSTS specifies the number of posts (n) to be used in the interpolation as defined in Appendix B.
If INTERPOLATION_MODE is set to 0, then INTERP_NUM_POSTS should be set to 1.
If INTERPOLATION_MODE is set to something other than 0 or 1, then the default for INTERP_NUM_POSTS will be 0.
		1	Unsigned short	2 bytes
MD19	DAMPENING_PARAM	The Dampening Parameter “D” used when defining the normalizing scale factor when INTERPOLATION_MODE is set to 1.  If INTERPOLATION_MODE is set to a value other than 1, the DAMPENING_PARAM will be set to 0.		1	double	8 bytes
MD20	AP_LOC_PARAM_LIST	This record contains the x, y, z locations of the anchor points in the dataset, and the x, y, and z adjustable parameter values for each location.
NOTE:  This record will be repeated from 1 to N times, where the value of N is dependent on the number of anchor points required to accurately model changes in the covariance and is specified by NUM_AP_RECORDS.	Lines MD21-MD26	N	N/A	
MD21	AP_X	The x coordinate in local Cartesian (x, y, z) space describing the horizontal location that the subsequent error covariance is referenced to.		1	double	8 bytes
MD22	AP_Y	The y coordinate in local Cartesian (x, y, z) space describing the horizontal location that the subsequent error covariance is referenced to.		1	double	8 bytes
MD23	AP_Z	The z coordinate in local Cartesian (x, y, z) space describing the vertical location that the subsequent error covariance is referenced to.		1	double	8 bytes
MD24	AP_DELTA_X	The x coordinate adjustable parameter value.		1	float	4 bytes
MD25	AP_DELTA_Y	The y coordinate adjustable parameter value.		1	float	4 bytes
MD26	AP_DELTA_Z	The z coordinate adjustable parameter value.		1	float	4 bytes
MD27	GROUND_SPACE_CU_AND_AP_COVARIANCE_DIRECT_STORAGE	Data represents the C x C CU covariance matrix, the N 3 x 3 covariance matrices for each anchor point along the diagonal, and all of the off-diagonal covariance matrices.  The data is stored in column major order.  The full matrix is symmetric and only the upper (block) triangular portion is stored.  For J = 0 to (C +3N-1) columns, and for I = 0 to J rows.	Lines MD28-MD33	1	N/A	
MD28	Element_Index = 0	Covariance matrix element I = 0, J = 0		1	float	4 bytes
MD29	Element_Index = 1	Covariance matrix element I = 0, J = 1		1	float	4 bytes
MD30	Element_Index = 2	Covariance matrix element I = 1, J = 1		1	float	4 bytes
MD31	Element_Index = 3	Covariance matrix element I = 0, J = 2		1	float	4 bytes
MD32		Continuation of Covariance matrix elements, 4 bytes each.				
MD33	End Element_Index	Covariance matrix element N:  I = (C + 3N – 1), J = (C + 3N – 1)		1	float	4 bytes


 

Table E - 8:  BPF3 GPM Bundled File Header Information for Ground-Space with Direct Storage of Anchor Point Data.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	Length of this bundled file data following this header.
Variable		1	UInt32	4 bytes
H4	Filename	GPM_GndSpace_Direct		1	Char[32]	32 bytes




 

Appendix F : Unmodeled Error Storage Format

This appendix defines the encoding of the unmodeled error metadata for Sensor-Space or Ground-Space GPM.  A description of an LAS variable length record (VLR) is provided in Table F - 1 and Table F - 2 below.  Encoding the data in a BPF3 file involves implementing the header information defined in Table F - 3 followed by the unmodeled error metadata in Table F - 2.
Throughout this appendix, where not specified, all positional and distance units are in meters, all angular units are in milliradians and all time units are in seconds.  In accordance with both the LAS and BPF specifications, all data is in little-endian format.

Table F - 1:  LAS Variable Length Record Header Information for Unmodeled Error Data.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	276		1	Unsigned short	2 bytes
H5	Record Length After Header	2 + NUM_UE_RECORDS * ( 206 + NUM_UE_POSTS * 48 ) bytes		1	Unsigned short	2 bytes
H6	Description	GPM_Unmodeled_Error_Data		1	Char[32]	32 bytes

Table F - 2:  Unmodeled Error Covariance VLR Metadata Information.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Metadata
MD2	UNMODELED_ERROR_FILE	The variable length record carrying the unmodeled error information for this dataset.	MD3-MD36	1	N/A	
MD3	NUM_UE_RECORDS	The number of unmodeled error records (N) being represented in this VLR.  This number would be tied to the number of flightlines / collection units in the specific file.		1	Unsigned short	2 bytes
MD4	UE_RECORD	This portion of the VLR stores the unmodeled error information for a specific flightline / collection unit (1…N).	MD5-MD36	N	N/A	
MD5	TRAJECTORY_ID	The unique identifier for the given trajectory of interest.  This field only applies to sensor-space GPM and is associated with the Point Source ID stored per point record.  In the case of ground-space GPM, the value of this field should be set to zero.		1	Int	4 bytes
MD6	UNIQUE_ID	Unique identification string identifying the data this Unmodeled Error information is associated with.  This will be the DATASET_ID in the case of Ground Space GPM and the COLLECTION_UNIT_ID in the case of Sensor Space GPM.		1	Char[128]	128 bytes
MD7	CORR_ROT_THETA_X	The rotation angle θx(in milliradians) that is used in conjunction with θy and θz to rotate from the MCS (x,y,z) coordinate system to the u,v,w system consistent with the correlation directions.   This is a rotation about the x-axis (counter-clockwise positive). The rotation sequence is applied as defined in Section 3.2.1.		1	double	8 bytes
MD8	CORR_ROT_THETA_Y	The rotation angle θy (in milliradians) that is used in conjunction with θx and θz to rotate from the MCS (x,y,z) coordinate system to the u,v,w system consistent with the correlation directions.  This is a rotation about the y-axis (counter-clockwise positive).  The rotation sequence is applied as defined in Section 3.2.1.		1	double	8 bytes
MD9	CORR_ROT_THETA_Z	The rotation angle θz (in milliradians) that is used in conjunction with θx and θy to rotate from the MCS x,y,z coordinate system to the u,v,w system consistent with the correlation directions.  This is a rotation about the z-axis (counter-clockwise positive).  The rotation sequence is applied as defined in Section 3.2.1.		1	double	8 bytes
MD10	SENSOR_CORR_PARAMS_U	  
Parameters (A, α, β, τ) used to describe the correlation decrease between points as a function of travel in the u direction.	Lines MD11-MD14	1	N/A	
MD11	PARAM_A_U	Parameter A controlling the maximum correlation that can be obtained (ideally 1). In this case, it is relative to movement in the u direction.		1	float	4 bytes
MD12	PARAM_ALPHA_U	Parameter alpha (α) contributing to the minimum correlation value that can be obtained.   In this case, it is relative to movement in the u direction.		1	float	4 bytes
MD13	PARAM_BETA_U	Parameter Beta (β), controlling the shape of the correlation curve and the speed of the decay.  In this case, it is relative to movement in the u direction.		1	float	4 bytes
MD14	PARAM_TAU_U	Parameter Tau (τ), a distance constant.   In this case, it is relative to movement in the u direction.		1	float	4 bytes
MD15	SENSOR_CORR_PARAMS_V	 
 
Parameters (A, α, β, τ) used to describe the correlation decrease between points as a function of travel in the v direction.	Lines MD16-MD19	1	N/A	
MD16	PARAM_A_V	Parameter A controlling the maximum correlation that can be obtained (ideally 1). In this case, it is relative to movement in the v direction.		1	float	4 bytes
MD17	PARAM_ALPHA_V	Parameter alpha (α) contributing to the minimum correlation value that can be obtained.   In this case, it is relative to movement in the v direction.		1	float	4 bytes
MD18	PARAM_BETA_V	Parameter Beta (β), controlling the shape of the correlation curve and the speed of the decay.  In this case, it is relative to movement in the v direction.		1	float	4 bytes
MD19	PARAM_TAU_V	Parameter Tau (τ), a distance constant.   In this case, it is relative to movement in the v direction.		1	float	4 bytes
MD20	SENSOR_CORR_PARAMS_W	 
 
Parameters (A, α, β, τ) used to describe the correlation decrease between points as a function of travel in the w direction.	Lines MD21-MD24	1	N/A	
MD21	PARAM_A_W	Parameter A controlling the maximum correlation that can be obtained (ideally 1). In this case, it is relative to movement in the w direction.		1	float	4 bytes
MD22	PARAM_ALPHA_W	Parameter alpha (α) contributing to the minimum correlation value that can be obtained.   In this case, it is relative to movement in the w direction.		1	float	4 bytes
MD23	PARAM_BETA_W	Parameter Beta (β), controlling the shape of the correlation curve and the speed of the decay.  In this case, it is relative to movement in the w direction.		1	float	4 bytes
MD24	PARAM_TAU_W	Parameter Tau (τ), a distance constant.   In this case, it is relative to movement in the w direction.		1	float	4 bytes
MD25	UE_COV_POST_LIST	This part of the variable length record specifies the x, y, z location of each unmodeled error post along with its associated unmodeled error covariance.
	Lines MD26-MD36	1	N/A	
MD26	NUM_UE_POSTS	The number (P) of Unmodeled Error posts included in this UE record.		1	Unsigned short 	2 bytes
MD27	UE_COV_POST	This record contains the x, y, z location in the MCS and the associated unmodeled error covariance for a specific unmodeled error post in the dataset.
NOTE:  This record will be repeated from 1 to P times, where the value of P (is dependent on the number of posts required to accurately model the unmodeled error contribution.	Lines MD28-MD36	P	N/A	
MD28	UE_COV_POST_X	The x coordinate in MCS (x, y, z) space describing the location that the subsequent unmodeled error covariance is referenced to.		1	double	8 bytes
MD29	UE_COV_POST_Y	The y coordinate in MCS (x,y,z) space describing the location that the subsequent unmodeled error covariance is referenced to.		1	double	8 bytes
MD30	UE_COV_POST_Z	The z coordinate in MCS (x,y,z) space describing the location that the subsequent unmodeled error covariance is referenced to.		1	double	8 bytes
MD31	UE_COV_POST_VARX	The variance in the x dimension for the ground covariance matrix in MCS coordinate space describing the unmodeled error covariance at a point.		1	float	4 bytes
MD32	UE_COV_POST_VARY	The variance in the y dimension for the ground covariance matrix in MCS coordinate space describing the unmodeled error covariance at a point.		1	float	4 bytes
MD33	UE_COV_POST_VARZ	The variance in the z dimension for the ground covariance matrix in local MCS coordinate space describing the unmodeled error covariance at a point.		1	float	4 bytes
MD34	UE_COV_POST_VARXY	The covariance between the x and y dimensions for the ground covariance matrix in local MCS coordinate  space describing the unmodeled error covariance at a point.		1	float	4 bytes
MD35	UE_COV_POST_VARXZ	The covariance between the x and z dimensions for the ground covariance matrix MCS coordinate space describing the unmodeled error covariance at a point.		1	float	4 bytes
MD36	UE_COV_POST_VARYZ	The covariance between the y and z dimensions for the ground covariance matrix MCS coordinate space describing the unmodeled error covariance at a point.		1	float	4 bytes
 

Table F - 3:  BPF3 ULEM Bundled File Header Information for Unmodeled Error Metadata.
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	2 + NUM_UE_RECORDS * ( 206 + NUM_UE_POSTS * 48 ) bytes		1	UInt32	4 bytes
H4	Filename	GPM_Unmodeled_Error_Data		1	Char[32]	32 bytes

 

Appendix G: GPM Master VLR

This appendix defines the encoding of the mandatory GPM Master variable length record (VLR).  This VLR contains metadata that applies to the entire file and describes items  such as GPM version (0.0 for ULEM), the GPM implementation associated with the file, the number of collection  units in the file, and the model space coordinate system (MCS).   The encoding of the VLR would be handled as provided in Table G - 1 and Table G - 2 below.  Encoding the data in a BPF3 file involves implementing the header information defined in Table G - 3 followed by the metadata in Table G - 2.  If no GPM file additions are included in the parent BPF3 file, the GPM base header will be zero filled, except for the magic number field. 
This VLR is required for GPM.  No default values are assumed.  Note that this VLR was not a part of the original ULEM specification.  However, the GPM Master VLR is being made backwards compatible so that it can be used to provide useful information in legacy ULEM 1.0 files.  It is not mandatory for ULEM 1.0 files.
A section of this VLR defines the encoding of the Model-space Coordinate System (MCS) metadata for Sensor-Space or Ground-Space GPM.  As specified in Section 3.3.1, the MCS may be one of the following coordinate systems:
1.	Earth Centered Earth Fixed (ECEF).
2.	Local Space Rectangular (LSR) – requires origin and unit vectors, in ECEF space, that define the x, y, and z axes (respectively) of the LSR system.
3.	UTM – requires hemisphere and zone.  X and Y coordinates are Easting and Northing (respectively), and Z coordinates are Height Above Ellipsoid (HAE).
The list number assigned to each coordinate system above is used in the storage (MCS_ID) to determine which coordinate system has been chosen as the MCS for the dataset.  Depending on which coordinate system is chosen, additional metadata may need to be populated in the storage.  If certain metadata storage is not needed for the chosen coordinate system (e.g. origin for ECEF) then that storage location is set to a value of zero.
Defining the Local Space Rectangular (LSR) system for MCS_ID 2 requires additional metadata that includes coordinates of the origin and unit vectors, in ECEF space, that define the x, y, and z axes (respectively) of the LSR system.  The contiguous fields XOM through ZOM specify the origin (offset) of the LSR system relative to the ECEF coordinate system, and the contiguous fields XUXM through ZUZM the rotation. The conversion between ECEF and LSR coordinates is performed as follows:
 
Equation G - 1.  Conversion from ECEF to LSR coordinates.
Throughout this appendix, where not specified, all positional and distance units are in meters and all angular units are in milliradians.  In accordance with both the LAS and BPF specifications, all data is in little-endian format.

Table G-1: LAS Variable Length Record Header for GPM Master
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	227		1	Unsigned short	2 bytes
H5	Record Length After Header	Variable		1	Unsigned short	2 bytes
H6	Description	GPM_Master		1	Char[32]	32 bytes

Table J-2: Variable Length Record Content for GPM Master

Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Metadata
MD2	GPM_Master_VLR	The variable length record containing common GPM (or ULEM in the case of version 0.0) metadata associated with the entire file.	MD3-MD51	1	N/A	
MD3	GPM_Version	Field specifying the version of the GPM specification used to create the file.  
Allowed values include:
Value=0.0 (refers to the legacy ULEM 1.0 format)
Value=1.0 (refers to the current GPM1.0 format)		1	char [10]	10 bytes
MD4	GPM_Implementation	Field specifying the GPM implementation associated with the file.  Allowed values include:
Value=DataStream
Value=SensorSpace
Value=GroundSpace		1	Char[20]	20 bytes
MD5	MCS_Coord_System	Section defining the MCS coordinate system associated with this file.  Note that a common MCS will be used for all CUs within a given file.	MD6-MD20	1	N/A	
MD6	MCS_ID	Unique identifier for the chosen coordinate system assigned as the MCS.  Allowed values are 1, 2, and 3.
1 = ECEF
2 = LSR
3 = UTM		1	Unsigned short	2 bytes
MD7	MCS_ORIGIN_X	The Earth Centered Earth Fixed (ECEF) X coordinate (meters) of the origin of the Model-space Coordinate System (MCS) referred to as XOM in equation G-1.  Required only for MCS_ID 2, otherwise set to 0.		1	double	8 bytes
MD8	MCS_ORIGIN_Y	The ECEF Y coordinate (meters) of the origin of the MCS referred to as YOM in equation G-1.  Required only for MCS_ID 2, otherwise set to 0.		1	double	8 bytes
MD9	MCS_ORIGIN_Z	The ECEF Z coordinate (meters) of the origin of the MCS referred to as ZOM in equation G-1.  Required only for MCS_ID 2, otherwise set to 0.		1	double	8 bytes
MD10	MCS_XUXM 
	MCS Coordinate Unit Vector (XUXM). This field provides the ECEF X component of the unit vector defining the X-axis of the MCS. 
Used in conjunction with fields XUXM through ZUZM forming an orthogonal matrix.

Required only for MCS_ID 2, otherwise set to 0.		1	double	8 bytes
MD11	MCS_XUYM 
	MCS Coordinate Unit Vector (XUYM). This field provides the ECEF X component of the unit vector defining the Y-axis of the MCS. 

Used in conjunction with fields XUXM through ZUZM forming an orthogonal matrix.

Required only for MCS_ID 2, otherwise set to 0.		1	double	8 bytes
MD12	MCS_XUZM 
	MCS Coordinate Unit Vector (XUZM). This field provides the ECEF X component of the unit vector defining the Z-axis of the Local MCS. 
Used in conjunction with fields XUXM through ZUZM forming an orthogonal matrix.

Required only for MCS_ID 2, otherwise set to 0.		1	double	8 bytes
MD13	MCS_YUXM 
	MCS Coordinate Unit Vector (YUXM). This field provides the ECEF Y component of the unit vector defining the X-axis of the MCS. 

Used in conjunction with fields XUXM through ZUZM forming an orthogonal matrix.

Required only for MCS_ID 2, otherwise set to 0.		1	double	8 bytes
MD14	MCS_YUYM 
	MCS Coordinate Unit Vector (YUYM). This field provides the ECEF Y component of the unit vector defining the Y-axis of the MCS. 

Used in conjunction with fields XUXM through ZUZM forming an orthogonal matrix.

Required only for MCS_ID 2, otherwise set to 0.
		1	double	8 bytes
MD15	MCS_YUZM 
	MCS Coordinate Unit Vector (YUZM). This field provides the ECEF Y component of the unit vector defining the Z-axis of the Local MCS. 

Used in conjunction with fields XUXM through ZUZM forming an orthogonal matrix.

Required only for MCS_ID 2, otherwise set to 0.
		1	double	8 bytes
MD16	MCS_ZUXM 
	MCS Coordinate Unit Vector (ZUXM). This field provides the ECEF Z component of the unit vector defining the X-axis of the MCS. 

Used in conjunction with fields XUXM through ZUZM forming an orthogonal matrix.

Required only for MCS_ID 2, otherwise set to 0.
		1	double	8 bytes
MD17	MCS_ZUYM 
	MCS Coordinate Unit Vector (ZUYM). This field provides the ECEF Z component of the unit vector defining the Y-axis of the MCS. 

Used in conjunction with fields XUXM through ZUZM forming an orthogonal matrix.

Required only for MCS_ID 2, otherwise set to 0.
		1	double	8 bytes
MD18	MCS_ZUZM 
	MCS Coordinate Unit Vector (ZUZM). This field provides the ECEF Z component of the unit vector defining the Z-axis of the Local MCS. 
Used in conjunction with fields XUXM through ZUZM forming an orthogonal matrix.

 Required only for MCS_ID 2, otherwise set to 0.
		1	double	8 bytes
MD19	MCS_HEMI	Hemisphere designation, needed for UTM (MCS_ID = 3).  May be ‘N’ or ‘n’ for north, or ‘S’ or ‘s’ for south. 

For MCS_ID other than 3, MCS_HEMI=0.		1	Signed char	1 byte
MD20	MCS_ZONE	Numeric zone designation, needed for UTM (MCS_ID = 3).  Valid values are 1 – 60.

For MCS_ID other than 3, MCS_ZONE=0.		1	Unsigned char	1 byte
MD21	ID_INFORMATION		MD22 – MD23	1	N/A	
MD22	DATASET_ID	Dataset identification string.  This is comparable to the CSM “Image ID”.  It may simply consist of the name of the dataset file.  For Ground Space GPM, this is the primary identifier of the model.

Reference Appendix C of the CSM TRD for more details.		1	Char[32]	32 bytes
MD23	REFERENCE_DATE_TIME	An approximate UTC (Universal Time Coordinated) date and time associated with the Dataset.  This could be a collection time, but in some situations may be a processing time.  The returned string follows the ISO 8601 standard as documented in the CSM TRD.		1	Char[18]	18 bytes
MD24	DATASET_EXTENT_INFORMATION	Provides extent information (via minimum and maximum coordinates in the MCS) for the entire Dataset.	MD25 – MD31	1	N/A	
MD25	EXTENT_MIN_X	The smallest value for the model x-coordinate in the Dataset.		1	Double	8 bytes
MD26	EXTENT_MAX_X	The largest value for the model x-coordinate in the Dataset.		1	Double	8 bytes
MD27	EXTENT_MIN_Y	The smallest value for the model y-coordinate in the Dataset.		1	Double	8 bytes
MD28	EXTENT_MAX_Y	The largest value for the model y-coordinate in the Dataset.		1	Double	8 bytes
MD29	EXTENT_MIN_Z	The smallest value for the model z-coordinate in the Dataset.		1	Double	8 bytes
MD30	EXTENT_MAX_Z	The largest value for the model z-coordinate in the Dataset.		1	Double	8 bytes
MD31	NUM_COLLECTIONS	The number of Collections stored in this dataset.		1	UInt32	4 bytes
MD32	COLLECTION_RECORD	This record contains the information related to a particular Collection.
NOTE:  This record will be repeated from 1 to C times, where the value of C is equal to the value of NUM_COLLECTIONS.	Lines MD33-MD51	C	N/A	
MD33	COLLECTION_ID	Collection identification string provides an identifier that indicates a collection activity common to a set of CUs.  This ID must be unique among collection activities for a given model name and is used to determine parameter correlation and sharing.  

Reference Appendix C of the CSM TRD for more details. 		1	Char[32]	32 bytes
MD34	PLATFORM_ID	Platform identification string provides an identifier to indicate the specific platform that was used to acquire the data. This ID must be unique among platforms for a given model name and is used to determine parameter correlation and sharing.

Reference Appendix C of the CSM TRD for more details.		1	Char[32]	32 bytes
MD35	NUM_SENSORS	Field specifying the integer number (S) of Sensors that are associated with this Collection.		1	UInt32	4 bytes
MD36	SENSOR_RECORD	This record contains the information related to a particular Sensor.
NOTE:  This record will be repeated from 1 to S times, where the value of S is equal to the value of NUM_SENSORS associated with this collection.	Lines MD37-MD51	S	N/A	
MD37	SENSOR_ID	Sensor identification string provides an identifier to indicate the specific sensor that was used to acquire the data.  This ID must be unique among sensors for a given model name and is used to determine parameter correlation and sharing. 

Reference Appendix C of the CSM TRD for more details.		1	Char[32]	32 bytes
MD38	SENSOR_TYPE	Sensor Types and assumptions as described in the CSM TRD Section 1.4. Type refers to the method or phenomenology by which the sensor collects the data, for example lidar. 

Reference Appendix A of the CSM TRD for more details on valid values. 

If the sensor type is unknown, then the field should be populated with “CSM_SENSOR_TYPE_UNKNOWN”		1	Char[32]	32 bytes
MD39	SENSOR_MODE	Within a sensor type, the SENSOR_MODE further refines the sensor description.  Reference Appendix A of the CSM TRD for more details on valid values.  

If the sensor type is unknown, then the field should be populated with “CSM_SENSOR_MODE_UNKNOWN”		1	Char[32]	32 bytes
MD40	NUM_COLLECTION_UNITS	Field specifying the integer number (U) of Collection Units that are associated with this sensor in this collection.
NOTE:  For Ground-Space GPM, this value is set to 1, and is the last field in the GPM Master VLR.		1	UInt32	4 bytes
MD41	COLLECTION_UNIT_RECORD	This record contains the information related to a particular Collection Unit.
NOTE:  This record will be repeated from 1 to U times, where the value of U is equal to the value of NUM_COLLECTION_UNITS.
NOTE: For Ground-Space GPM, this COLLECTION_UNIT_RECORD is invalid, and is not written to the GPM Master VLR.	Lines MD41-MD51	U	N/A	
MD42	REFERENCE_DATE_TIME	An approximate UTC (Universal Time Coordinated) date and time associated with the Collection Unit.  This could be a collection time, but in some situations may be a processing time.  The returned string follows the ISO 8601 standard as documented in the CSM TRD.		1	Char[18]	18 bytes
MD43	COLLECTION_UNIT_ID	Collection Unit identification string provides an identifier to indicate a specific Collection Unit.  This ID must be unique among all Collection Unit IDs within the dataset and is used to determine parameter correlation and sharing. 

The format is DatasetID.CollectionID.SensorID.CU_Index where CU_Index ranges from 1 to NUM_COLLECTION_UNITS.

		1	Char[128]	128 bytes
MD44	POINT_SOURCE_ID	Value, usually supplied by the data provider, that provides an integer identifier for this CU that is unique among all of the CUs stored within this file

This is the value that correlates this CU to a point record via the Point_SOURCE_ID stored per point record.

Note that this value may not be globally unique among all files.  The same CU may use different POINT_SOURCE_ID values if the same CU data is used in multiple files.
		1	Unsigned short	2 bytes
MD45	CU_EXTENT_INFORMATION	Provides extent information (via minimum and maximum coordinates) for the entire Collection Unit.	MD45 – MD51	1	N/A	
MD46	EXTENT_MIN_X	The smallest value for the model x-coordinate in the Collection Unit.		1	Double	8 bytes
MD47	EXTENT_MAX_X	The largest value for the model x-coordinate in the Collection Unit.		1	Double	8 bytes
MD48	EXTENT_MIN_Y	The smallest value for the model y-coordinate in the Collection Unit.		1	Double	8 bytes
MD49	EXTENT_MAX_Y	The largest value for the model y-coordinate in the Collection Unit.		1	Double	8 bytes
MD50	EXTENT_MIN_Z	The smallest value for the model z-coordinate in the Collection Unit.		1	Double	8 bytes
MD51	EXTENT_MAX_Z	The largest value for the model z-coordinate in the Collection Unit.		1	Double	8 bytes

Table G - 3:  BPF3 GPM Master File Header 
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	Char[4]	4 bytes
H3	File Length	Variable.		1	UInt32	4 bytes
H4	Filename	GPM_Master		1	Char[32]	32 bytes


Appendix H: Storage and Retrieval of 3D Per-Point Error  

This appendix defines the encoding and the retrieval of the random 3D Per Point Error ( .    It begins by reviewing the Look-up Table (LUT) approach being used to store and retrieve these error contributions and then provides details on the metadata storage. 
The Look-up Table Approach:
As introduced in Appendix A, in addition to the traditional mensuration error associated with the analyst measurement of a point, GPM allows for other contributions to mensuration error including random 3D Per Point Error (PPE).  The PPE is additional random error that must be accounted for, but that cannot be removed as part of an adjustment and cannot be adequately modeled using unmodeled error.   It is expected that the PPE could vary significantly from point to point in a local region.  
To account for the contributions from the PPE, a Look-up Table (LUT) approach is employed in GPM.  The LUT will model the variation in the 3D random error from point to point with enough fidelity, while still limiting the amount of storage required for implementation. To implement the LUT, a table of PPE covariance is stored as defined in this Appendix—i.e. a table of P such “unique” covariances is stored. 
 
Equation H-1: Establishing a LUT of PPE covariance.
Each cloud point has an additional metadata field, see Appendices D and E, whose value is the domain of the LUT (i.e. a value of 1..P).  The 3   3 PPE error covariance   is thus obtained for any point in the cloud by obtaining the index from the additional metadata field in the point record and going into the lookup table to extract the covariance associated with that index.  For an arbitrary collection of n points chosen for exploitation, the full covariance matrix for PPE thus has zeroes for off-diagonal terms, i.e.
 
Equation H-2: Block diagonal covariance built of PPE covariances. 	
The superscript in each component diagonal matrix within Equation H-2 is the lookup table index for the point’s PPE covariance.

Per Point Error Storage Format:
The LAS variable length record used to store the PPE is defined in Tables H - 1 and Table H - 2 below.  Encoding the data in a BPF3 file involves implementing the header information defined in Table H - 3 followed by the LUT information from Table H - 2.  Throughout this appendix, where not specified, all positional and distance units are in meters.  In accordance with both the LAS and BPF specifications, all data is in little-endian format.

Table H-1: LAS Variable Length Record Header for Per Point Lookup Error Data
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“NGA”		1	Char[16]	16 bytes
H4	Record ID	228		1	Unsigned short	2 bytes
H5	Record Length After Header	34 + NUM_PPE_COV_RECORDS * 24  bytes		1	Unsigned short	2 bytes
H6	Description	Per_Point_Lookup_Error_Data		1	Char[32]	32 bytes

Table H-2: Per Point Lookup Error Covariance VLR Metadata Information
Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Metadata
MD2	PER_POINT_ERROR_FILE	The variable length record carrying the per-point lookup table error information for this dataset	MD3-MD11	1	N/A	
MD3	NUM_PPE_COV_RECORDS	Number of unique per-point error covariances in this lookup table enumerated (1..P).  Since the LAS record length after header (H5 in Table 2 ) is an unsigned short, the total data length is restricted to 65535 bytes.  This implies that the maximum number of PPE_COV_RECORDS, P, that can be stored is floor( (65535-34)/24) = 2729	1..P	1	Unsigned short	2 bytes
MD4	PPE_FIELD_NAME	When LAS 1.4 is used, this is the name in the LAS 1.4 Extra Bytes VLR (name field) of the lookup index field. This string is matched  with the field descriptor string to  identifiy  the 2 byte unsigned short (Extra bytes data_type 3) in which the LUT index is stored for each point.
For BPF3 this string is matched to the Label of the field (descriptor string) found in the Metadata Subheader to identify the metadata field number in which the LUT index is stored for each point.
For both the LAS 1.4 and the BPF3, this value should be set to: PPE_LUT_Index 
If PPE is being used with LAS 1.2 or 1.3, then this field name will refer to the existing LAS field that is being repurposed as the LUT pointer.  The User Data field should be used for this purpose. 
		1	Char[32]	32 bytes
MD5	PPE_COV_RECORD	This record stores one unique covariance for lookup	MD6-MD11	P	N/A	
MD6	PPE_COV_VARX	The variance in the x dimension for the ground covariance matrix in local Cartesian (x,y,z) space describing the per-point error covariance for lookup index K (K ranges from 1..P)			float	4 bytes
MD7	PPE_COV_VARY	The variance in the y dimension for the ground covariance matrix in local Cartesian (x,y,z) space describing the per-point error covariance for lookup index K (K ranges from 1..P)			float	4 bytes
MD8	PPE_COV_VARZ	The variance in the z dimension for the ground covariance matrix in local Cartesian (x,y,z) space describing the per-point error covariance for lookup index K (K ranges from 1..P)			float	4 bytes
MD9	PPE_COV_VARXY	The covariance between the x and y dimensions for the ground covariance matrix in local Cartesian (x,y,z) space describing the per-point error covariance for lookup index K (K ranges from 1..P)			float	4 bytes
MD10	PPE_COV_VARXZ	The covariance between the x and z dimensions for the ground covariance matrix in local Cartesian (x,y,z) space describing the per-point error covariance for lookup index K (K ranges from 1..P)			float	4 bytes
MD11	PPE_COV_VARYZ	The covariance between the y and z dimensions for the ground covariance matrix in local Cartesian (x,y,z) space describing the per-point error covariance for lookup index K (K ranges from 1..P)			float	4 bytes

Table H-3: BPF3 GPM Bundled File Header Information For Per Point Lookup Error Data
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		Bundled File Header	H2-H4	1	N/A	
H2	Magic Number	“FILE”		1	char[4]	4 bytes
H3	File Length	Length of this bundled file data following this header= 34 + NUM_PPE_COV_RECORDS * 24  bytes 		1	UInt32	4 bytes
H4	Filename	Per_Point_Lookup_Error_Data		1	Char[32]	32 bytes

 

Appendix I: Use of EXTRA_BYTES VLR for PPE Pointer Per Point Record

With the adoption of LAS 1.4, the LAS standard has documented a method to store additional data per LAS point record and to describe to any user what these extra bytes represent.  This description of the additional point data is handled through a Variable Length Record (VLR) known as the EXTRA BYTES VLR.  While LAS 1.4 has not been officially adopted and is not currently supported by ULEM or GPM, it is expected that it will be adopted in the future.  Further, this EXTRA BYTES concept provides a mechanism to add metadata GPM requires per point without repurposing existing LAS fields from the point record.  One place this method could be very advantageous is in storing a pointer to a Look-up Table per point record for the 3D Per Point Error (PPE).  This appendix documents, for future use, an EXTRA_BYTES VLR for the storage of the PPE pointer per point record.
 Table I-1: LAS Variable Length Record Header for Extra Bytes Describing the 3D PPE Look-up table Pointer
Row	Name	Definition	Domain	Max. Occur.	Format	Size
H1		VLR Header	H2-H6	1	N/A	
H2	Reserved	Value of zero.		1	Unsigned short	2 bytes
H3	User ID	“LASF_Spec”		1	Char[16]	16 bytes
H4	Record ID	4		1	Unsigned short	2 bytes
H5	Record Length After Header	N records x 192 bytes		1	Unsigned short	2 bytes

Table I-2: Variable Length Record Content for Extra Bytes Describing the 3D PPE Look-up table Pointer

Row	Name	Definition	Domain	Max. Occur.	Format	Size
MD1	VLR Metadata
MD2	PPE_LUT_Index	The variable length record defining the extra bytes associated with the PPE_LUT_Index value when implemented as extra bytes on a point record within LAS 1.4	MD3-MD13	1	N/A	
MD3	reserved	Reserved field that is required to be set to “0” per the LAS 1.4 specification.
Value=0		1	Unsigned char [2]	2 bytes
MD4	data_type	Data type to be used for the PPE_LUT_Index when it is appended to a point record.
Value=3
Data_type 3 refers to an unsigned short in the LAS 1.4 specifitaion.		1	Unsigned char	1 byte
MD5	options	A bit mask specifying whether the min and max range of the values have been set, whether the scale and/or offset values are set, and whether there is a special value that should be interpreted as NO_DATA.
For this VLR, all flags are not set.
Value=[0 0 0 0 0 0 0 0]		1	Unsigned char	1 byte
MD6	name	Name field that provides a descriptive name for the field added as extra bytes to each point record.
Value=PPE_LUT_Index		1	Char [32]	32 bytes
MD7	Unused	Reserved field that is required to be set to “0” per the LAS 1.4 specification.
Value=0		1	unsigned char [4]	4 bytes
MD8	No_data	Used to identify a special value that should be interpreted as “no data” for the field provided in Extra Bytes.  When a “no data” value is not to be used, this field should be set to “0”
Value=0		1	any type [3]	24 bytes
MD9	Min	Specifies the minimum value for the data being added to the point records as extra bytes.  If a minimum value is not being used, the value should be set to 0.
 Value=0		1	any type [3]	24 bytes
MD10	Max	Specifies the maximum value for the data being added to the point records as extra bytes.  If a maximum value is not being used, the value should be set to 0.
 Value=0		1	any type [3]	24 bytes
MD11	Scale	Specifies a scale factor to be applied to the value for the data being added to the point records as extra bytes.  If a scale value is not being used, the value should be set to 0.
 Value=0		1	Double [3]	24 bytes
MD12	Offset	Specifies an offset value to be applied in conjunction with the scale for the data being added to the point records as extra bytes.  If an offset value is not being used, the value should be set to 0.
 Value=0		1	Double [3]	24 bytes
MD13	Description	A description of the field being added as extra bytes to each point record.
Value=”GPM 3D PPE Look up table index  ”		1	Char [32]	32 bytes

 

 

Appendix J: Use of ULEM Files within the GPM Construct. 

The initial version of ULEM was approved as a GWG standard in the summer of 2013 and is referred to as ULEM in this Appendix.  This document introduces updates to the ULEM file format as well as introduces additional metadata that has been defined as part of the move to the more general Generic Point-cloud Model (GPM).  Because of several internal updates to existing ULEM Variable Length Record (VLR) structures, a GPM sensor model is not inherently backwards compatible with ULEM files.  This appendix describes how a ULEM file could be read using a GPM model, and what assumptions must be made to do so.
One change to the GPM format is the Unmodeled Error (UE) VLR.  GPM moved from modeling UE in a local planar coordinate system to using a three-dimensional system.  This change required updates to the UE VLR.  While ULEM files had x and y coordinates to define each UE post, GPM has x, y, and z coordinates.  Thus, when a ULEM file is read by a GPM model, the z coordinate for each UE post must be set to 0.  As part of the same change, GPM moved from having one rotation (θz) to rotate the local E, N space into a u,v space for correlation to using three sequential rotations (θx , θy,  θz) to rotate from x, y, z to a u, v, w system.  Therefore if a GPM model is to read a ULEM file, two of the rotations (θx and, θy) must be set to zero.    The values assigned to the correlation parameters for the w dimension must be set so that the correlation coefficient for w (ρw) equals 1.  For example Aw=1.0, αw=0.9999, βw=0, and Dw=10000. Finally, to remain general, when a ULEM file is read by a GPM sensor model, the unmodeled error posts must be read as if they can be irregularly spaced versus being constrained to an evenly spaced grid.  
Sensor-Space ULEM files could easily be read into a GPM Sensor-Space model. The majority of the content in the Sensor-Space VLRs have remained unchanged between the two versions.  However, the binary structures of the VLRs have been modified to store a unique Collection Unit ID per collection unit.   Therefore, when reading a ULEM file with a GPM model, a Collection Unit ID must be assigned if needed.  Additionally, ULEM files may not have the GPM Master VLR to describe the Model Coordinate System (MCS).  So, a GPM model reading a ULEM file must assume and set the MCS to be the same coordinate system stored for the points in the LAS header. If the GPM Master VLR is not present, the VLRs in the file will need to be scanned to determine if it contains Ground-Space or Sensor-Space ULEM and to determine the number of collection units (CUs) in the file.  Finally, a ULEM file will not have any Per-Point Error (PPE) included in the point records nor have the associated PPE VLRs.   So, during exploitation PPE will be set to zero when included as a contributor to the mensuration error.
Ground-Space ULEM can be read using similar assumptions.  As with Sensor-Space, a ULEM Ground-Space file may not have a GPM Master VLR.  If this is the case, the MCS coordinate system must be defined based on the metadata for the points in the LAS header.  Additionally, the ULEM file will not have a unique Dataset ID stored, so one must be assigned.  The exploitation tool / model will again have to scan the file to determine that it contains Ground Space ULEM and to recognize that only one CU is stored in the file.  The UE assumptions described above must once again be applied when a ULEM Ground-Space file is read by a GPM model.  In a similar fashion, there are correlation functions for the Anchor Points used in Ground-Space which are three-dimensional in GPM, but only two-dimensional in ULEM.  This change required updates to the Ground-Space GPM VLRs. When reading a ULEM file in a GPM model, these are handled in similar fashion to the way UE was handled.  Two of the rotation angles (θx and θy)  are set to zero and the correlation parameters are set so that the correlation coefficient in the w dimension (ρw) equals 1.  As before, PPE will not exist in a ULEM file and must be assumed to be 0 during exploitation.
While a GPM version model is not completely backwards compatible with a ULEM model, the two formats are very similar. This appendix has specified a few assumptions that if applied would allow a ULEM file to be read and exploited in the GPM construct.

