---
tags:
  - documentation
  - reference-guide
  - work-order
  - import
  - xml
  - nautical-systems
  - version-7.0.0
  - abs-wavesight
  - technical
  - enterprise
  - september-2025
---

[← Back to Home](index.md)

# Nautical Systems

## Work Order XML Import

Reference Guide

September 2025

# Introduction

This *Work Order XML Import* document provides detailed instructions on using the Work Order Import facility to load work order data into the Nautical Systems application. It outlines the file requirements, preparation steps, and error-handling procedures, along with guidance on re-importing records. Additionally, it includes instructions for reviewing import results and managing backups to ensure data integrity within the *ABS Wavesight Nautical Systems*™.

**Release Date**--- September 2025

### About Version

Information in this document supports *ABS Wavesight Nautical Systems*™ versions **6.5.33** and higher.

### About ABS Wavesight™

ABS Wavesight™ is a software as a service (SaaS) company which includes a unique, integrated portfolio of digital solutions designed to assist ABS clients with their operations and compliance process, while promoting decarbonization goals. To learn more, refer to [www.abswavesight.com](http://www.abswavesight.com).

### Browser Considerations

This application is compatible with the latest versions of both *Google Chrome* and *Microsoft Edge*, however, for the best experience, it is recommended that you use *Google Chrome*.

# Overview

The purpose of this document is to define the requirements for the **Work Order Interface Importer**. This functionality enables work orders to be imported to **NS5** from an external system. Depending on the provided data, the import may also:

- Credits standard jobs in specific scenarios, and/or

- Update the maintenance history of one or more equipment items.

This feature is to be implemented via *InterfaceManager.exe* and made accessible through both the UI and the command line.

Important Implementation Details

- A new menu option should be available at: **Interfaces**--- **Import**--- **Work Order**. This should be added alongside existing import options.

- The import can also be triggered using the following command: *interfacemanager.exe --i -o=workorder*

- The *XML* file(s) to be imported must be placed in the following folder: **(\\Production\\Enterprise\\interface\\Workorder\\Import)**.

# XML File Format

The *XML* file format is a structured way to store and exchange data using tagged elements. It ensures data is well-organized, readable and easily processed across different systems. It is widely used for data exchange, configuration files, and system communication.

## Schema XSD

The following *XSD* defines the structure and required elements for importing Work Order data into the system.

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="NS5InterfaceExport">
    <xs:complexType>
      <xs:sequence>
        <xs:element maxOccurs="unbounded" name="WorkOrder">
          <xs:complexType>
            <xs:sequence>
              <xs:choice maxOccurs="unbounded">
                <xs:element name="WorkOrderID" type="xs:unsignedInt" />
                <xs:element name="Title" type="xs:string" />
                <xs:element name="DocumentNumber" type="xs:unsignedByte" />
                <xs:element name="Status" type="xs:string" />
                <xs:element name="WOType" type="xs:string" />
                <xs:element name="Priority" type="xs:string" />
                <xs:element name="PMJob" type="xs:string" />
                <xs:element name="StandardJobID" type="xs:string" />
                <xs:element name="StandardJobType" type="xs:string" />
                <xs:element name="ShipCode" type="xs:string" />
                <xs:element name="ShipNo" />
                <xs:element name="ShipID" type="xs:unsignedInt" />
                <xs:element name="ShipName" type="xs:string" />
                <xs:element name="ShipIMO" type="xs:unsignedInt" />
                <xs:element name="ConditionBased" type="xs:string" />
                <xs:element name="ScheduledOn" type="xs:string" />
                <xs:element name="DueOn" />
                <xs:element name="CompletedOn" type="xs:string" />
                <xs:element name="ClosedDate" />
                <xs:element name="CancelledDate" />
                <xs:element name="Extension" />
                <xs:element name="EquipmentName" type="xs:string" />
                <xs:element name="EquipmentCode" />
                <xs:element name="EquipmentID" type="xs:string" />
                <xs:element name="EquipmentClassNo" />
                <xs:element name="EquipmentIMO" type="xs:string" />
                <xs:element name="EquipmentCriticality" type="xs:string" />
                <xs:element name="Counter" type="xs:decimal" />
                <xs:element name="Event_Drydock" type="xs:string" />
                <xs:element name="ActionsRqd" type="xs:string" />
                <xs:element name="Questionnaire" />
                <xs:element name="JobDescription" type="xs:string" />
                <xs:element name="Findings" />
                <xs:element name="PreviousFindings" />
                <xs:element name="Closure_CmplRemarks" />
                <xs:element name="AdminInfo">
                  <xs:complexType>
                    <xs:sequence>
                      <xs:element name="AccountCode" type="xs:unsignedInt" />
                      <xs:element name="Project" type="xs:string" />
                      <xs:element name="JobCategory" type="xs:string" />
                      <xs:element minOccurs="0" name="Causes">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element name="JobCause" type="xs:string" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                      <xs:element name="ClassNo" />
                      <xs:element name="Department" type="xs:string" />
                      <xs:element name="ItemCategory" />
                      <xs:element name="User_Defined" />
                      <xs:element name="ScheduledBySystem" type="xs:string" />
                      <xs:element name="DrydockCategory" />
                      <xs:element name="ABCIndicator" />
                      <xs:element name="CostCenter" type="xs:string" />
                      <xs:element name="WBS" type="xs:string" />
                    </xs:sequence>
                  </xs:complexType>
                </xs:element>
                <xs:element name="Material">
                  <xs:complexType>
                    <xs:sequence minOccurs="0">
                      <xs:element name="Part">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element name="EquipmentName" type="xs:string" />
                            <xs:element name="EquipmentCode" type="xs:string" />
                            <xs:element name="EquipmentID" type="xs:unsignedInt" />
                            <xs:element name="PartID" type="xs:unsignedInt" />
                            <xs:element name="PartName" type="xs:string" />
                            <xs:element name="RequiredQty" type="xs:decimal" />
                            <xs:element name="UsedQty" type="xs:decimal" />
                            <xs:element name="Unit" type="xs:string" />
                            <xs:element name="UserDefined" type="xs:string" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                    </xs:sequence>
                  </xs:complexType>
                </xs:element>
                <xs:element name="Resources">
                  <xs:complexType>
                    <xs:sequence>
                      <xs:element minOccurs="0" name="ResourceDetails">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element name="Position" type="xs:string" />
                            <xs:element name="ActualHours" type="xs:decimal" />
                            <xs:element name="EstimatedHours" type="xs:decimal" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                      <xs:element name="SuggestedVendor" />
                      <xs:element name="EstimatedCost" type="xs:decimal" />
                    </xs:sequence>
                  </xs:complexType>
                </xs:element>
                <xs:element name="Attachments">
                  <xs:complexType>
                    <xs:sequence minOccurs="0">
                      <xs:element maxOccurs="unbounded" name="Attachment">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element name="ID" type="xs:unsignedInt" />
                            <xs:element name="File" type="xs:string" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                    </xs:sequence>
                  </xs:complexType>
                </xs:element>
                <xs:element name="EquipmentSpaceStructure">
                  <xs:complexType>
                    <xs:sequence>
                      <xs:element minOccurs="0" maxOccurs="unbounded" name="Equipment">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element name="Code" type="xs:string" />
                            <xs:element name="EquipmentID" type="xs:unsignedInt" />
                            <xs:element name="Name" type="xs:string" />
                            <xs:element name="ClassNo" />
                            <xs:element name="EquipmentIMO" type="xs:string" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                      <xs:element minOccurs="0" name="Space">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element name="SpaceName" type="xs:string" />
                            <xs:element name="SpaceID" type="xs:unsignedInt" />
                            <xs:element name="Index" type="xs:string" />
                            <xs:element name="ClassNo" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                      <xs:element minOccurs="0" name="Structrure">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element name="Index" />
                            <xs:element name="Name" type="xs:string" />
                            <xs:element name="StructureID" type="xs:unsignedInt" />
                            <xs:element name="ClassNo" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                      <xs:element minOccurs="0" name="MaintainedPart">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element name="Code" />
                            <xs:element name="Name" type="xs:string" />
                            <xs:element name="MaintainedPartId" type="xs:unsignedInt" />
                            <xs:element name="ClassNo" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                    </xs:sequence>
                  </xs:complexType>
                </xs:element>
                <xs:element name="Readings">
                  <xs:complexType>
                    <xs:sequence>
                      <xs:element maxOccurs="unbounded" name="Reading">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element minOccurs="0" name="ReadingDate" type="xs:unsignedInt" />
                            <xs:element name="MeasurementPointID" type="xs:string" />
                            <xs:element name="ReadingValue" type="xs:decimal" />
                            <xs:element name="ReadingUOM" type="xs:string" />
                            <xs:element name="Warning" type="xs:string" />
                            <xs:element name="Error" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                    </xs:sequence>
                  </xs:complexType>
                </xs:element>
                <xs:element name="Failure">
                  <xs:complexType>
                    <xs:sequence>
                      <xs:element name="FailureMode" type="xs:string" />
                      <xs:element name="FailureCause" type="xs:string" />
                      <xs:element name="OfflineDate" type="xs:unsignedInt" />
                      <xs:element name="OfflineTime" type="xs:string" />
                      <xs:element name="OnlineDate" type="xs:unsignedInt" />
                      <xs:element name="OnlineTime" type="xs:string" />
                      <xs:element name="FailedParts">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element maxOccurs="unbounded" name="Part">
                              <xs:complexType>
                                <xs:sequence>
                                  <xs:element name="EquipmentName" type="xs:string" />
                                  <xs:element name="EquipmentCode" type="xs:string" />
                                  <xs:element name="EquipmentID" type="xs:unsignedInt" />
                                  <xs:element name="PartID" type="xs:unsignedInt" />
                                  <xs:element name="PartName" type="xs:string" />
                                </xs:sequence>
                              </xs:complexType>
                            </xs:element>
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                    </xs:sequence>
                  </xs:complexType>
                </xs:element>
                <xs:element name="CMData">
                  <xs:complexType>
                    <xs:sequence>
                      <xs:element name="CMVendor" type="xs:string" />
                      <xs:element name="CMDate" type="xs:string" />
                      <xs:element name="CMType" type="xs:string" />
                      <xs:element name="CMDetails">
                        <xs:complexType>
                          <xs:sequence>
                            <xs:element name="Equipment" type="xs:string" />
                            <xs:element name="EquipmentID" type="xs:unsignedInt" />
                            <xs:element name="CMType" type="xs:string" />
                            <xs:element name="Problem" type="xs:string" />
                            <xs:element name="Recommendation" type="xs:string" />
                          </xs:sequence>
                        </xs:complexType>
                      </xs:element>
                    </xs:sequence>
                  </xs:complexType>
                </xs:element>
              </xs:choice>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
      <xs:attribute name="AppVersion" type="xs:string" use="required" />
      <xs:attribute name="CreatedOn" type="xs:unsignedInt" use="required" />
      <xs:attribute name="DBID" type="xs:unsignedByte" use="required" />
      <xs:attribute name="DBVersion" type="xs:string" use="required" />
      <xs:attribute name="SiteID" type="xs:unsignedByte" use="required" />
    </xs:complexType>
  </xs:element>
</xs:schema>
```

## Sample XML

The sample *XML* below illustrates the format and content of the imported Work Order data. It reflects how actual data is structured during import, based on the defined *XSD* schema.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<NS5InterfaceImport>
  <WORKORDER>
    <SHIPID>200000007</SHIPID>
    <WONUMBER>0000986438</WONUMBER>
    <STDJOBID>200000036</STDJOBID>
    <EQUIPMENT>
      <EQID>200000076</EQID>
    </EQUIPMENT>
    <EQUIPMENT>
      <EQID>200000077</EQID>
    </EQUIPMENT>
    <SPACE>
      <SPACEID>100000001</SPACEID>
    </SPACE>
    <SPACE>
      <SPACEID>100000003</SPACEID>
    </SPACE>
    <STRUCTURE>
      <STRUCTUREID>100000001</STRUCTUREID>
    </STRUCTURE>
    <STRUCTURE>
      <STRUCTUREID>100000003</STRUCTUREID>
    </STRUCTURE>
    <TITLE>NIL 1111</TITLE>
    <SCHEDDATE>20150424</SCHEDDATE>
    <CMPLDATE>20150424</CMPLDATE>
    <CLOSEDATE>20150424</CLOSEDATE>
    <DESC>DESCCCCCCCCCCCCCCCCCCCCCCCCCCC</DESC>
    <FINDINGS>FINDDDDDDDDDDDDDDDDDDDDDDD</FINDINGS>
    <JOBCATEGORY>CARGO GEAR REPAIRS</JOBCATEGORY>
    <ACCOUNTNO>100800</ACCOUNTNO>
    <PROJECTNO>AE5TL</PROJECTNO>
    <PRIORITY>A</PRIORITY>
    <COSTCENTER>ONE</COSTCENTER>
    <WBS>WBS1</WBS>
    <DEPTABBR>STW</DEPTABBR>
    <USERDEFINED></USERDEFINED>
    <PARTS>
      <MACHINERYPARTID>200000045</MACHINERYPARTID>
      <QTY>1</QTY>
    </PARTS>
    <PARTS>
      <MACHINERYPARTID>200000039</MACHINERYPARTID>
      <QTY>1</QTY>
    </PARTS>
    <RESOURCES>
      <CREWPOSTITLE>OS</CREWPOSTITLE>
      <ESTMANHOURS>11</ESTMANHOURS>
      <ACTMANHOURS>22</ACTMANHOURS>
    </RESOURCES>
    <RESOURCES>
      <CREWPOSTITLE>CHIEF ENGINEER</CREWPOSTITLE>
      <ESTMANHOURS>11</ESTMANHOURS>
      <ACTMANHOURS>22</ACTMANHOURS>
    </RESOURCES>
    <IMAGE></IMAGE>
  </WORKORDER>
</NS5InterfaceImport>
```

## Import File Header

This import file header defines the structure of the import data, specifying key tags and their requirements. The table below outlines each tag, whether it is required, its description and exceptions.

| **Tag No1** | **Tag No2** | **Tag No3**     | **Req**  | **Type**                     | **Size/Values**                           | **Description**                                                                                                                                                                                                                                                                                                                                           |
| ----------- | ----------- | --------------- | -------- | ---------------------------- | ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| WORKORDER   | Tag         |                 |          |                              |                                           |                                                                                                                                                                                                                                                                                                                                                           |
|             | SHIPID      |                 | Required | Decimal                      | 20 digits                                 | ·       Unique DatabaseID for a ship in the NS database.<br><br>·       Mandatory for Work Order import.                                                                                                                                                                                                                                                  |
|             | WONUMBER    |                 |          | Depends on system preference | 12                                        | ·       Work Order Number. It can be auto-generated or manually provided based on system settings.<br><br>·       System configuration that defines how Work Order Numbers are generated (Auto, Numeric, Alphanumeric, User-defined).                                                                                                                     |
|             | STDJOBID    |                 |          | Decimal                      | 20                                        | ·       The unique DatabaseID for Standard Job from NS database.<br><br>·       If provided in the import, the work order will be credited to the specified standard job, updating the last done date.<br><br>·       The work order will display under the standard job’s **Work Order** tab and in the maintenance history of the associated equipment. |
|             | EQUIPMENT   | Tag             |          |                              |                                           |                                                                                                                                                                                                                                                                                                                                                           |
|             |             | EQID            |          | Decimal                      | 20                                        | ·       Unique DatabaseID for Equipment from the NS database.<br><br>·       The equipment specified must belong to the same ship as the Work Order.                                                                                                                                                                                                      |
|             | SPACE       | Tag             |          |                              |                                           |                                                                                                                                                                                                                                                                                                                                                           |
|             |             | SPACEID         |          | Decimal                      | 20                                        | ·       Unique DatabaseID for Space from the NS database.<br><br>·       The space must also belong to the same ship as the Work Order.                                                                                                                                                                                                                   |
|             | STRUCTURE   | Tag             |          |                              |                                           |                                                                                                                                                                                                                                                                                                                                                           |
|             |             | STRUCTUREID     |          | Decimal                      | 20                                        | ·       Unique DatabaseID for Structure from the NS database.<br><br>·       The Structure must also belong to the same ship as the Work Order.                                                                                                                                                                                                           |
|             | TITLE       |                 |          | Character                    | 50                                        | If a standard job is linked to the work order, its title is included. If not, the title provided here is used as the Work Order title.                                                                                                                                                                                                                    |
|             | SCHEDDATE   |                 | Optional | Date                         |                                           | ·       Schedule date for the Work Order.<br><br>·       If provided during import the date is linked to the work order as schedule date. If not, the import execution date is used.                                                                                                                                                                      |
|             | CMPLDATE    |                 | Optional | Date                         |                                           | Date when the work order was completed.                                                                                                                                                                                                                                                                                                                   |
|             | CLOSEDATE   |                 | Optional | Date                         |                                           | Date when the work order was closed.                                                                                                                                                                                                                                                                                                                      |
|             | DESC        |                 |          | Character                    | 4 GB for MySQL and 2 GB for SQL Server    | ·       Remarks for the Work Order.<br><br>·       The text value for _<DESC>_ is encapsulated as _CDATA_.                                                                                                                                                                                                                                                |
|             | FINDINGS    |                 |          | Character                    | 4 GB for MySQL and 2 GB for SQL Server    | ·       Findings or observations for the Work Order.<br><br>·       The text value for _<FINDINGS>_ is encapsulated as _CDATA_.                                                                                                                                                                                                                           |
|             | JOBCATEGORY |                 |          | Character                    | 150                                       | Job Category description. Used to associate a category with the Work Order.                                                                                                                                                                                                                                                                               |
|             | ACCOUNTNO   |                 |          | Character                    | 50                                        | Account Number. Used to associate an Account No with the Work Order.                                                                                                                                                                                                                                                                                      |
|             | PROJECTNO   |                 |          | Character                    | 25                                        | Project Number. Identifies the project linked to the Work Order.                                                                                                                                                                                                                                                                                          |
|             | PRIORITY    |                 |          | Character                    | Acceptable values are:<br><br>A, B, C, D. | Priority level for the work order.                                                                                                                                                                                                                                                                                                                        |
|             | COSTCENTER  |                 |          | Character                    | 150                                       | ·       Cost Center. Identifies as the cost center for the Work Order.<br><br>·       Must belong to the same ship as the Work Order.                                                                                                                                                                                                                     |
|             | WBS         |                 |          | Character                    | 150                                       | Identifies the **WBS** linked the Work Order.                                                                                                                                                                                                                                                                                                             |
|             | DEPTABBR    |                 |          | Character                    | 150                                       | ·       Department abbreviation.<br><br>·       Associates a department with Work Order.<br><br>·       Mandatory or optional based on system preference.                                                                                                                                                                                                 |
|             | USERDEFINED |                 |          | Character                    | 75                                        | User-defined custom field for the Work Order.                                                                                                                                                                                                                                                                                                             |
|             | PARTS       | Tag             |          |                              |                                           |                                                                                                                                                                                                                                                                                                                                                           |
|             |             | MACHINERYPARTID |          | Decimal                      | 20                                        | ·       Identifier for the machinery part used during work order execution.<br><br>·       The Parent Equipment and the Work Order must belong to the same ship.                                                                                                                                                                                          |
|             | QTY         |                 |          | Decimal                      | 14, 4                                     | Quantity of usage during work order execution.                                                                                                                                                                                                                                                                                                            |
|             | RESOURCES   | Tag             |          |                              |                                           |                                                                                                                                                                                                                                                                                                                                                           |
|             |             | CREWPOSTITLE    |          | String                       | 100                                       | ·       Title of the crew position.<br><br>·       Required to capture resource details in the work order.                                                                                                                                                                                                                                                |
|             |             | ESTMANHOURS     |          | Decimal                      | 7, 1                                      | Estimated man-hours planned for executing the work order.                                                                                                                                                                                                                                                                                                 |
|             |             | ACTMANHOURS     |          | Decimal                      | 7, 1                                      | Actual man-hours spent on the work order.                                                                                                                                                                                                                                                                                                                 |
|             | IMAGE       |                 |          | Character                    | 50                                        | File Name for the attachment to be associated with the work order.                                                                                                                                                                                                                                                                                        |
# Error Logging

The table below outlines various scenarios that may occur during Work Order import and the corresponding error response messages generated in _XML_ format.

| **Tag Name**                                                                                  | **Error Message**                                                                                                                                          | **Validation Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ShipID**                                                                                    | _Ship Id is Mandatory for the Work Order Import._                                                                                                          | Triggered when the Ship ID is missing in the work order import.                                                                                                                                                                                                                                                                                                                                                                                                                             |
| _Error:_ _Incorrect Ship Id specified_                                                        | Triggered when the Ship ID is provided in an incorrect format.                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| _Invalid Ship Id.The ship id [SHIPID] associated with workorder number [WONO]does not exist._ | Triggered when the provided Ship ID does not exist or is not valid in the system.                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **WONO**                                                                                      | _This Work Order Number[WONO] already exists_                                                                                                              | Displayed if Work Order Number already exists in the system.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **STDJOBID**                                                                                  | _Un able to load WO since associated Standard Job is of type Serialized._                                                                                  | If the Standard Job is of type Serialized Item, the system will not associate it with the Work Order.                                                                                                                                                                                                                                                                                                                                                                                       |
| _Invalid StdJob Id OR Standard Job[STDJOBID ] does not belong to the given vessel[SHIPID]_    | If the referenced Standard Job does not belong to Ship provided in the import, the import fails.                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| _The Standard Job[STDJOBID] associated with [WONUM]is of Counter Based._                      | The import does not allow a work order to be associated with a Standard Job of counter-based type.                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **EQUIPMENT**                                                                                 |                                                                                                                                                            | ·       If the standard job is of type **MCH (Machinery)**, only the equipment linked to the Standard Job will be associated with the Work Order.<br><br>·       If the standard job is of type **MISC (Miscellaneous)**, all equipment referenced in the _<EQUIPMENT>_ section will be associated with the Work Order.                                                                                                                                                                     |
| **EQID**                                                                                      | _Invalid Equipment Id .The equipment id ["+equipments.getEqId()+"] associated with workorder number [WONUM]does not exist._                                | If the equipment does not belong to the ship specified in the work order, or if the system cannot locate the equipment using the given database ID, the following error message is displayed.                                                                                                                                                                                                                                                                                               |
| **SPACEID**                                                                                   | _Invalid Space Id .The Space id [SPACEID] associated with workorder number [WONUM]does not exist._                                                         | If the space does not belong to the ship specified in the work order, or if the system cannot locate the space using the given database ID, the following error message is displayed.                                                                                                                                                                                                                                                                                                       |
| **STRUCTUREID**                                                                               | _Invalid Structure Id .The Structure id [STRUCTUREID] associated with workorder number [WONUM]does not exist._                                             | If the structure does not belong to the ship specified in the work order, or if the system cannot locate the structure using the given database ID, the following message is displayed.                                                                                                                                                                                                                                                                                                     |
| **SCHEDDATE**                                                                                 | _Invalid Scheduled By Date._                                                                                                                               | If the schedule date is present but not in the correct format, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                                    |
| **CMPLDATE**                                                                                  | _Invalid Completed Date._                                                                                                                                  | If the completed date is present but not in the correct format, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                                   |
| **CLOSEDATE**                                                                                 | _Invalid Closed Date._                                                                                                                                     | If the closed date is present but not in the correct format, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                                      |
| _Completed Date is required if Close Date is given for workorder number[WONUM]._              | If closed date is provided but completed date is missing, the following error message is displayed.                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| _Closed date should be greater than or equal to complete date for workorder number[WONUM]._   | If closed date is earlier than completed date, the following error message is displayed.                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **JOBCATEGORY**                                                                               | _Invalid Job Category.The job category[JOBCATEGORY] associated with workorder number [WONUM]does not exist._                                               | If an invalid job category description is provided, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                                               |
| **ACCOUNTNO**                                                                                 | _Invalid Account Number.The account number[ACCOUNTNO] associated with workorder number [WONUM]does not exist._                                             | If an invalid account number is provided, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                                                         |
| **PROJECTNO**                                                                                 | _Invalid Project Number.The project number[PROJECTNO] associated with workorder number [WONUM]does not exist._                                             | If an invalid project number is provided, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                                                         |
| **PRIORITY**                                                                                  | System throws an exception.                                                                                                                                | If a priority is provided and not equal to A, B, C or D.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **COSTCENTER**                                                                                | _Invalid Cost center.The cost center[COSTCENTER] associated with workorder number [WONUM]does not exist._                                                  | If an invalid cost center is provided, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                                                            |
| _The cost center[COSTCENTER] associated with workorder number [WONUM] is not linked to Ship._ | If the cost center is not linked to the ship, the following message is displayed.                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **WBS**                                                                                       | _Invalid WBS.The WBS [WBS] associated with workorder number [WONUM]does not exist._                                                                        | If an invalid WBS number is provided, the following message is displayed.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **USERDEFINED**                                                                               | _Exception is shown when this field value is more than 75 characters._                                                                                     | If the field value exceeds 75 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **PARTS**                                                                                     |                                                                                                                                                            | ·       For each **<MACHINERYPARTID>** provided in the **<PARTS>** section, a **<QTY>** greater than **0** must be specified.<br><br>·       Each unique combination of **<MACHINERYPARTID>** and **<QTY>** is treated as a work order usage entry and will update the inventory quantity of the corresponding **MACHINERYPARTID** accordingly.<br><br>**Note**:<br><br>Each usage should be recorded only once, regardless of how many **<EQID>** values are referenced in the work order. |
| **MACHINERYPARTID**                                                                           | _Invalid MachineryPart Id.The machinery part[MACHINERYPARTID] associated with workorder number [WONUM]does not exist._                                     | If an invalid **MachineryPart ID** is provided in the parts section, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                              |
| **QTY**                                                                                       | _Quantity must be greater than zero._                                                                                                                      | If quantity is less than or equal to **0**, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                                                       |
| **RESOURCES**                                                                                 |                                                                                                                                                            | For each **<CREWPOSTITLE>** entry under the **<RESOURCES>** section, either **<ESTMANHOURS>** or **<ACTMANHOURS>** must be provided with a value greater than **0**.                                                                                                                                                                                                                                                                                                                        |
| **CREWPOSTITLE**                                                                              | _Invalid Crew position Title.The crew position title ["+woResources.getCrewPositionTitle()+"]associated with workorder number ["+woNumb+"]does not exist._ | If an invalid **<CREWPOSTITLE>**is provided in the **<RESOURCES>** section, the following error message is displayed.                                                                                                                                                                                                                                                                                                                                                                       |
| **ESTMANHOURS**                                                                               | _Either Estimated ManHours or Actual ManHours must be greater than zero_                                                                                   | Displayed when both **Estimated ManHours** and **Actual ManHours** are either missing or not greater than **zero** for the specified crew position.                                                                                                                                                                                                                                                                                                                                         |
| **ACTMANHOURS**                                                                               | _Either Estimated ManHours or Actual ManHours must be greater than zero_                                                                                   | Displayed when both **Estimated ManHours** and **Actual ManHours** are either missing or not greater than **zero** for the specified crew position.                                                                                                                                                                                                                                                                                                                                         |

# Technical Support

Should you need technical support, log into the [Customer Self-Service Portal](https://www.abswavesight.com/customer-self-service) where you can access the following helpful resources:

1. **Knowledge Center** – Discover resources and browse product information.
2. **Community** – Find solutions, ask questions, and collaborate with other users.
3. **Product Support** – Submit and check the status of your tickets.

![Support Portal](../media/NS_Work/image4.png)