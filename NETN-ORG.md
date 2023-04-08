
# NETN-ORG
|Version| Date| Dependencies|
|---|---|---|
|2.0|2023-04-08|NETN-MRM|

The NATO Education and Training Organization (NETN-ORG) module provides a standard way to represent organizations in the simulation scenario and their relationships and structure. The relationships include unit command structure, relationships between organizations, unit equipment, and installations.

Simulation of elements of an organization requires knowledge of the intra-organizational relationship, e.g. superior, subordinate, and iter-organizational relationships with other organizations, e.g. friendly or hostile. The NETN-ORG supports initialization and organizations' dynamic change of this information.

The specification is based on IEEE 1516 High Level Architecture (HLA) Object Model Template (OMT) and supports interoperability in a federated simulation (federation) based on HLA. In addition to the FOM Module, a file-based data storage and interchange format is defined based on SISO-STD-007-2008 Military Scenario Definition Language (MSDL). The NETN-ORG XML schema defines elements to capture units, equipment items, relationships, and initial modelling responsibilities.

Use the NETN-ORG information to: * initialize simulated entities * perform disaggregation, aggregation, divide and merge actions using NETN-MRM * change organizational relationships * capture simulated unit and equipment state as snapshots

## Overview 
 
Use the NETN-ORG FOM module to represent organizations and their internal structure, relationships, associated units, equipment, and installations. 
 
Dynamic organizational changes may include new and or rearranged unit structure or changes in the relationships with other organizations. 
 
In a simulation, not all units, equipment and installations have a corresponding simulation entity in the federation. Which elements to represent as simulated entities are determined by the current modelling responsibility described in NETN-TMR and dynamic changes in the level of aggregation described in NETN-MRM. 
 
The NETN-ORG organization elements are the basis for the initialization of simulated entities, e.g. `Platforms` or `AggregateEntity` objects. Therefore, updates of NETN-ORG objects should be considered a re-initialization of any associate simulation entity. E.g. updating the `Unit` attribute `Holdings` should be reflected in an `AggregateEntity` representing the unit.


## Object Classes

Note that inherited and dependency attributes are not included in the description of object classes.

```mermaid
graph RL
ORG_Root-->HLAobjectRoot
BaseEntity-->HLAobjectRoot
OrganizationElement-->ORG_Root
Organization-->ORG_Root
Equipment-->OrganizationElement
Unit-->OrganizationElement
Installation-->OrganizationElement
AggregateEntity-->BaseEntity
PhysicalEntity-->BaseEntity
Platform-->PhysicalEntity
```

### ORG_Root

The object class for all NETN-ORG object classes

|Attribute|Datatype|Semantics|
|---|---|---|
|Name|HLAunicodeString|Required. A unique name. Max 255 characters.|

### OrganizationElement

An object class for all NETN-ORG organizational elements

|Attribute|Datatype|Semantics|
|---|---|---|
|Organization|UUID|Required: A reference to the organization the element is affiliated with.|
|EntityType|EntityTypeStruct|Required. SISO-REF-010 code for entity type definitions. If unknown, use 0.0.0.0.0.0.0.|
|SymbolId|SymbolIdentifier|Required. A symbol identifier.|
|Location|GeodeticPoint|Required. The geographic location of the element.|

### Equipment

Equipment represents individual physical items identified in the scenario, including platforms and sensors.

|Attribute|Datatype|Semantics|
|---|---|---|
|HoldingUnit|UUID|Optional: A reference to the unit to which this equipment belongs. The default is that the equipment does not belong to a specific unit.|
|MountedOn|UUID|Optional. Reference to another equipment item on which this item is mounted or attached.|
|SymbolAmplification|EquipmentSymbolAmplificationStruct|Optional. Text amplifications for the symbol.|

### Unit

A unit represents an element at a specified level in the organization. An organizational unit can contain subunits and can belong to a superior unit. A unit consists of equipment, personnel and supplies; these holdings can belong directly to the unit or indirectly as a holding of a subunit.

|Attribute|Datatype|Semantics|
|---|---|---|
|SuperiorUnit|UUID|Optional: A reference to a superior unit within the organization. The default is that this unit does not have a superior.|
|SymbolAmplification|UnitSymbolAmplificationStruct|Optional. Text amplifications for the symbol.|
|Echelon|EchelonEnum32|Optional. Symbol modifier identifying the command level. Default NONE.|
|IsHq|HLAboolean|Optional. Indicate whether the unit has a command function, e.g. if it is an HQ or not.|
|Holdings|ArrayOfHoldings|Optional. A set of holdings of the unit. The default is an empty list.|
|EmbarkedIn|UUID|Optional. A reference to a unit or equipment carrying/transporting the unit. The default value is 00000000-0000-0000-0000-000000000000 (UUID with all zeros), indicating that the unit is not embarked in or mounted on any other unit or equipment.|
|Formation|FormationStruct|Optional. Formation of this unit.|

### Installation

Installations are facilities, e.g. harbours, airfields, or engineering objects, e.g. minefields.

|Attribute|Datatype|Semantics|
|---|---|---|
|UnitInCommand|UUID|Optional: A reference to a unit in charge of this installation. The default is that no specific unit is in charge of the installation.|
|SymbolAmplification|InstallationSymbolAmplificationStruct|Optional. Text amplifications for the symbol.|

### Organization

An organization have relationships with other organizations. Units belonging to different organizations have the same relationship as the organizations they belong to. However, the relationships between organizations can be asymmetrical, e.g. Side A can be hostile to B while B is neutral to A. Furthermore, the relation may change during a federation execution.

|Attribute|Datatype|Semantics|
|---|---|---|
|Relations|ArrayOfRelations|Optional. The relations with other organizations. The federation agreements specify default relationship.|
|ForceIdentifier|ForceIDEnum8|Required: A force identifier indicate a special relationship with an organization in the scenario designated as the default perspective of the scenario. The force identifier applies to all simulated entities representing an organizational element belonging to the organization and is a required attribute for all `PhysicalEntity` and `AggregateEntity` objects in the federation.|
|Nation|HLAunicodeString|Optional: A textual description of the nation the organization affiliates with.|

### BaseEntity

A base class of aggregate and discrete scenario domain participants. The BaseEntity class is characterized by being located at a particular location in space and independently movable, if capable of movement at all. It specifically excludes elements normally considered to be a component of another element. The BaseEntity class is intended to be a container for common attributes for entities of this type. Since it lacks sufficient class specific attributes that are required for simulation purposes, federates cannot publish objects of this class. Certain simulation management federates, e.g. viewers, may subscribe to this class. Simulation federates will normally subscribe to one of the subclasses, to gain the extra information required to properly simulate the entity.

|Attribute|Datatype|Semantics|
|---|---|---|
|Organization|UUID|Optional: The organization in the scenario this entity belongs to.|

### AggregateEntity

A group of one or more separate objects that operate together as part of an organization. These objects may be discrete, may be other aggregate objects, or may be a mixture of both.

|Attribute|Datatype|Semantics|
|---|---|---|
|Unit|UUID|Optional: Reference to an existing NETN-ORG `Unit` object that is represented by this `AggregateEntity`. Default value is all zeros.|

### Platform

A physical object under the control of armed forces upon which sensor, communication, or weapon systems may be mounted.

|Attribute|Datatype|Semantics|
|---|---|---|
|Equipment|UUID|Optional: Reference to a Equipment that is represented by this Platform. Default value is all zeros.|

## Datatypes

Note that only datatypes defined in this FOM Module are listed below. Please refer to FOM Modules on which this module depends for other referenced datatypes.

### Overview
|Name|Semantics|
|---|---|
|AirFormationTypeEnum32|Air formation|
|ArrayOfHoldings|Sequence of holdings.|
|ArrayOfRelations|Sequence of relations.|
|EquipmentSymbolAmplificationStruct|Text amplifiers for Equipment symbols.|
|ForceIDEnum8|The identification of the force that the entity belongs to.|
|FormationDataStruct|Struct for enumerated choice for the type of formation being Ground, Air, Surface or Subsurface.|
|FormationLocationTypeEnum32|Enumerated choice for the method to correlate formation to location as the centre of mass or lead element.|
|FormationStruct|The formation of this unit.|
|FormationTypeEnum32|Enumerated choice for the type of formation being Ground, Air, Surface or Subsurface.|
|GroundFormationTypeEnum32|Specifies the formations for ground units.|
|Holding|Static and dynamic data about the holding.|
|InstallationSymbolAmplificationStruct|Text amplifiers for Installation symbols.|
|Relation|The specific value that represents the perceived hostility status.|
|SubsurfaceFormationTypeEnum32|Subsurface formation|
|SurfaceFormationTypeEnum32|Surface formation|
|Text1|Text of max length 1 character.|
|Text15|Text of max length 15 characters.|
|Text2|Text of max length 2 characters.|
|Text20|Text of max length 20 characters.|
|Text21|Text of max length 21 characters.|
|Text24|Text of max length 24 characters.|
|Text3|Text of max length 3 characters.|
|Text5|Text of max length 5 characters.|
|Text8|Text of max length 8 characters.|
|Text9|Text of max length 9 characters.|
|UnitSymbolAmplificationStruct|Text amplifiers for Unit symbols.|
        
### Enumerated Datatypes
|Name|Representation|Semantics|
|---|---|---|
|AirFormationTypeEnum32|HLAinteger32BE|Air formation|
|ForceIDEnum8|RPRunsignedInteger8BE|The identification of the force that the entity belongs to.|
|FormationLocationTypeEnum32|HLAinteger32BE|Enumerated choice for the method to correlate formation to location as the centre of mass or lead element.|
|FormationTypeEnum32|HLAinteger32BE|Enumerated choice for the type of formation being Ground, Air, Surface or Subsurface.|
|GroundFormationTypeEnum32|HLAinteger32BE|Specifies the formations for ground units.|
|SubsurfaceFormationTypeEnum32|HLAinteger32BE|Subsurface formation|
|SurfaceFormationTypeEnum32|HLAinteger32BE|Surface formation|
        
### Array Datatypes
|Name|Element Datatype|Semantics|
|---|---|---|
|ArrayOfHoldings|Holding|Sequence of holdings.|
|ArrayOfRelations|Relation|Sequence of relations.|
|Text1|HLAunicodeChar|Text of max length 1 character.|
|Text15|HLAunicodeChar|Text of max length 15 characters.|
|Text2|HLAunicodeChar|Text of max length 2 characters.|
|Text20|HLAunicodeChar|Text of max length 20 characters.|
|Text21|HLAunicodeChar|Text of max length 21 characters.|
|Text24|HLAunicodeChar|Text of max length 24 characters.|
|Text3|HLAunicodeChar|Text of max length 3 characters.|
|Text5|HLAunicodeChar|Text of max length 5 characters.|
|Text8|HLAunicodeChar|Text of max length 8 characters.|
|Text9|HLAunicodeChar|Text of max length 9 characters.|
        
### Fixed Record Datatypes
|Name|Fields|Semantics|
|---|---|---|
|EquipmentSymbolAmplificationStruct|Quantity, StaffComments, AdditionalInformation, EvaluationRating, SignatureEquipment, Hostile, IFF_SIF_AIS, UniqueDesignation, EquipmentType, EngagementBarText|Text amplifiers for Equipment symbols.|
|FormationStruct|FormationLocationType, FormationSpacing, FormationOrientation, FormationData|The formation of this unit.|
|Holding|OperationalCount, OnHandQuantity, RequiredOnHandQuantity, IsEquipment, EntityType|Static and dynamic data about the holding.|
|InstallationSymbolAmplificationStruct|StaffComments, AdditionalInformation, EvaluationRating, CombatEffectiveness, IFF_SIF_AIS, UniqueDesignation, EngagementBarText|Text amplifiers for Installation symbols.|
|Relation|Affiliate, Relationship|The specific value that represents the perceived hostility status.|
|UnitSymbolAmplificationStruct|ReinforcedOrReduced, StaffComments, AdditionalInformation, EvaluationRating, CombatEffectiveness, HigherFormation, IFF_SIF_AIS, UniqueDesignation, SpecialHeadquarters, EngagementBarText|Text amplifiers for Unit symbols.|
        
### Variant Record Datatypes
|Name|Discriminant (Datatype)|Alternatives|Semantics|
|---|---|---|---|
|FormationDataStruct|Domain (FormationTypeEnum32)|Ground, Air, Surface, Subsurface|Struct for enumerated choice for the type of formation being Ground, Air, Surface or Subsurface.|
    