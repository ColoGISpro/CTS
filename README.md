Documentation is currently being compiled by the CPW GIS Unit. What follows is a excerpt from the documentation to give companies bidding on the RFP some background on the existing CTS workflow. 


T Drive
The folders on this server are named sequentially and reflect the six step workflow created by the CPW GIS Unit to aggregate 39k miles of trail from 90 contributes representing 225 trail managers into the CTS Schema for publication into the COTREX.CO applications.

  

T:\1_SchemaRepository
This directory contains a .zip file with the empty CTS schema in .xml format along with CTS Data Integration Tools (CTS-DITools) which are a set ArcGIS Desktop ModelBuilder tools (.tbx) that streamline the translation, publishing and updating of existing trail GIS data into a common schema for inclusion an all-inclusive digital map of recreational trails in the state of Colorado.

Each tool within  the CTS_Root/the CTS_Toolbox.tbx has documentation detailing the title Summary of what the tool does, usage notes, and a explanation of each parameter. The CTS schema can be found: CTS_Root\Workspace\XMLSchema\CTS_EDIT_V36.xml
Documentation for the CTS schema can be found CTS Data Dictionary  For a non-technical overview of how I toolbox was used refer to the CTS - Data Integration Guide which was created to provide guidance to data contributors.

T:\2_ContributorDatasets
This folder Contains a folder for each data contributor. Each folder was created programmatically using tool 0.1 of theCTS_Toolbox.tbx for consistency. What follows is a quick description of the purpose of each subfolder:
ContributorData\Defaults\CTS_ConfigureDefaultValues.gdb - is a geodatabase with two tables containing the default values  that are assigned to TrailsSegment and Trailheads when new data is imported into CTS_Edit.gdb
ContributorData\Published - contains time stamped folders for each file geodatabase that was published from the contributor.
CTS_Root\ContributorData\SourceData - contains contains time stamped folders with the data submitted by the contributor for publication

The most important file is the:  ContributorData\CTS_Edit.gdb which contains the following feature classes and tables:
CTS_Edit.gdb\CTS_Trails\CTS_Trailheads - A point feature class with the CTS_Trailhead fields on the right side of the table and the source data’s fields on the left.
CTS_Edit.gdb\CTS_Trails\CTS_TrailNodes  - always empty (this was never implemented) 
CTS_Trails\CTS_TrailRoutes - always empty (this was never implemented) 
CTS_Edit.gdb\CTS_Trails\CTS_TrailSegments - A polyline feature class feature class with the CTS_Segments fields on the right side of the table and the source data’s fields on the left.
CTS_Edit.gdb\CTS_Contributor_tbl  - A table with one record representing the data contributor the database belongs to. Many of the tools within the CTS_Toolbox.tbx toolbox utilize this table to lookup the value in the CTS_ContributorID field
 CTS_Edit.gdb\CTS_DataStatus_tbl - A table with one record which captures the status of weather the data should be published into COTREX apps.
CTS_Trailhead_Crosswalk_tbl - 
CTS_TrailSegs_Crosswalk_tbl - Both of the crosswalk tables have the same fields:
SQL_SelectQuery - A SQL SELECT Query which references the contributors fields on the right side of the  CTS_TrailSegments feature class.  
CTS_TargetField - What the 
CTS_TargetValue
Crosswalk_YesNo -  Bool weather the record should be crosswalked by the 2.3.0 tool in the CTS_Toolbox.tbl toolbox
Crosswalk_Order - The order which records are run by tools 

T:\3_PublishedDatasets
3_PublishedDatasets\3a_Hopper  - A container where all published geodatabases are stored before they are appended into the CTS_Consolidataed.gdb geodatabase.
3_PublishedDatasets\3b_Processed - A container where all published geodatabases are stored after they are appended to the CTS_Consolidataed.gdb geodatabase.

T:\4_ConsolidatedData
4_ConsolidatedData\CTS_Consolidataed.gdb  - Is a file geodatabase which contains two feature classes with every trail_segment and trailhead  consolidated within a single layer. 
T:\4_ConsolidatedData\CTS_ConsolidataedTools.tbx contains the following tool:
LoadPublishedIntoConsolidated - which takes published data from the 3a_Hopper noted above and does the following to the TS_Consolidataed.gdb:
Gets ContributorID
Deletes all records in TS_Consolidataed.gdb with that ContributorID
Appends the new records from the published database into TS_Consolidataed.gdb
Moves the published Geodatabase to the 3b_Processed folder

T:\5_DerivedData

To come later

T:\6_WebApps
Please see:
https://github.com/ColoGISpro/CTS-WAB


