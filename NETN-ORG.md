# NETN-ORG
Copyright (C) 2020 NATO/OTAN.
This work is licensed under a [Creative Commons Attribution-NoDerivatives 4.0 International License](LICENCE.md).

## Introduction
Modelling of an organizational unit in a distributed simulation depends on its organizational relationship with other units (e.g. superior, subordinate) and on the relationship between organizational units (e.g. friendly or hostile). This organizational information is normally provided to a simulation system as part of its initialization.

The NATO Education and Training Network Organization Module (NETN ORG) is a specification of how to represent organizations in a federated distributed simulation.

### Purpose

The NETN-ORG FOM Module provides a standard object model for the representation of organizational information, including command structure, relationships between organizational units, relationships between units and equipment items, and installations associated with a unit or a force. This representation can be used for setting the initial state of simulated entities, for capturing subsequent snapshot states, and for dynamically changing model attributes such as organizational relationships.

In addition to the FOM Module, a file-based data storage and interchange format is defined based on SISO-STD-007-2008 Military Scenario Definition Language (MSDL). The NETN-ORG XML schema defines elements to capture units, equipment items, relationships, and initial modelling responsibilities.

### Scope

- Initial allocation of modelling responsibilities
- Capture unit and equipment state for (re-)initialization and snapshots
- Dynamic changes in an organization command structure
- Dynamic changes in relationships between organizational units
- Dynamic changes in relationships between equipment items and organizational units

## Overview

Use the NETN-ORG FOM module to represent organizational units, their internal organizational structure and relationships between different organizations based on force affiliation. Specific equipment items are associated with a unit, and the initial modelling responsibility of both units and equipment can be allocated to specific federates. Represent installations associated with a unit or force.

<img src=./images/objectclasses.png>

**Figure: ORG FOM Object Classes**

|Class|Description|
|---|---|
|ORG_Root|Root object class for all NETN-ORG object classes. Includes unique identifier and unique name attributes inherited by all subclasses.|
|Unit|Representation of an organizational unit based on attributes defined in the NETN-ORG extensions of MSDL.|
|EquipmentItem|Representation of an equipment item based on attributes defined in the NETN-ORG extensions of MSDL.|
|Installation|Representation of an installation/facility based on attributes defined in the NETN-ORG extensions of MSDL.|
|Force| Representation of a specific force and its relationship with other forces. Units belonging to a force all have the same relationship with units belonging to another force. The relationships between forces can be asymmetrical, e.g. Force A can be hostile to B while B is neutral to A. The relation may change during a federation execution. |
|FederateApplication| Representation of the allocation of initial modelling responsibility of units and equipment items to a federate application. |

During a simulation, the organizational relationships between units may change. Dynamic changes in the task organization may include new and or rearranged unit structure. These changes can be represented in the NETN-ORG FOM module as updates of corresponding attributes reflected by all subscribing simulation systems.

## Units, Equipment items and Installations

Not all units and equipment items are required to have a corresponding simulation entity representation in the federation execution. The existence of simulation entities may depend on the aggregation level of the federation and participating applications. During the execution of a scenario, the level of aggregation may also change, e.g. by using NETN-MRM aggregation patterns. Units may also be divided and represented as multiple aggregate entities or as platforms. 

Units and equipment items in NETN-ORG have both an `EntityType` attribute and a `SymbolId` attribute. The `EntityType` attribute indicates the type of model to use in the simulation. The `SymbolId` is a representation of the simulated entity as a 2D symbol on a map. In some cases, the symbol selected may indicate a different type of entity compared to the simulation `EntityType`. The SISO standard SISO-REF-010 (Reference for Enumerations for Simulation Interoperability) provides a standard set of entity type enumeration values. Federation agreements and mapping of entity types to simulation models may be developed to complement and override the standard enumerations.

The NETN-ORG objects represent data used for (re-)initialization of ground truth objects such as NETN-Physical Platforms and NETN-MRM Aggregate entities. The initial value of the NETN-ORG object attributes can be used by federates to perform initial registration and update of ground-truth objects. Note that each federate will interpret these values and perform their internal initialization which might include approximations, adjustments etc. E.g. an equipment item representing a ground vehicle can be located in water or inside buildings/trees. Therefore the initial value of the corresponding ground-truth platform can be adjusted by the federate. 

Subsequent updates of NETN-ORG objects with an associated ground-truth representation in the federation execution should be considered a re-initialization of the ground-truth object. A federate with current modelling responsibility of a ground-truth object must perform the re-initialization based on the updated unit or equipment item attribute values. Federation agreements should specify any limitation as to which NETN-ORG object attributes are allowed to be updated during the federation execution.  

Snapshots of the simulation ground-truth can be made at any point during the federation execution but preferably in a paused state when there is no advancement of simulation time. The snapshot is an update of all NETN-ORG objects to reflect the current simulated ground-truth state, e.g. unit locations and relationships in NETN-ORG are updated.

The initial allocation of modelling responsibility of NETN-ORG objects (unit, equipment item, installation) in the federation is represented by Federate Application, which associates specific federates with NETN-ORG objects. As noted earlier, during the federation execution the modeling responsibility may change and another federate may be come responsible for modelling a certain unit and/or child units.


### Unit

A `Unit` is a representation of an initial or snapshot state of an organizational unit based on attributes defined in the NETN-ORG extensions of MSDL.

The `Unit` object class attributes represent model data for organizational units that can be represented in the federation as ground-truth Aggregate Entities. The initial values can be used during scenario initialization, and subsequent updates of attributes are reflected in the federation to update model attributes.

|Attribute|Description|
|---|---|
|UniqueId|***Inherited:*** **Required.** Unique Identifier.|
|Name|**Required.** A unique name of the units.|
|SuperiorUnit|**Required.** Reference to the superior unit of this unit. If this unit has no superior unit (i.e. is the top-unit) then the value of this attribute shall be 00000000-0000-0000-0000-000000000000 (UUID with all zeros).|
|EmbarkedIn|**Optional.** A reference to a host unit which carries/transports the unit. Default value is 00000000-0000-0000-0000-000000000000 (UUID with all zeros) indicating that the unit is not embarked in any other unit.|
|Force|**Required.** The UUID referencing the Force that the unit belongs to.|
|Holdings|**Optional.** A set of holdings of the unit. Default is an empty list.|
|EntityType|**Required.** The entity type to use for representation of the units as an aggregate entity. Entity types should be based on SISO-REF-010 and/or defined by federation agreements.|
|SymbolId|**Required.** A symbol identifier represented as a string. The symbol standard used is indicated using an URI notation (uri:xxxxxxxxxx). The following uri should be used for common symbology standards app6b, app6b, app6c, app6c, 2525b, 2525c, 2525d. If not provided the symbol standard used is undefined.|
|SymbolAmplification|**Optional.** Text amplifications for the unit's symbol. Static or very low update rate.|
|Disposition|**Required.** Formation location, direction and speed of unit.|
|Formation|**Optional.** Formation of this unit.|
|IsHq|**Optional.** Indicate if the unit has a command function, e.g. if it is an HQ or not.|
|Echelon|**Optional.** Symbol modifier identifying the command level. Default NONE.|
|CommunicationNetworks|**Optional.** Set of Communication Networks that unit monitors and uses to communicate during a mission.|
|IsSimulationEntity|**Optional.** Indicates if the Unit has an initial allocation of modelling responsibility and is represented as a ground-truth aggregate entity during federation execution. Default is False.|

### Equipment Item

The `EquipmentItem` object class attributes represent specific equipment associated with a unit. Equipment items can be represented in the federation as ground-truth physical entities, e.g. an Aircraft platform or RadioTransmitter.

|Attribute|Description|
|---|---|
|UniqueId|***Inherited:*** **Required.** Unique Identifier.|
|Name|**Required.** A unique name of the equipment item.|
|HoldingUnit|**Required.** Identifies the lowest level unit in the ORBAT to which this equipment item belong.|
|MountedOn|**Optional.** Reference to another equipment item on which this item is mounted or attached.|
|EntityType|**Required.** SISO-REF-010 code for entity type definitions. If unknown, use 0.0.0.0.0.0.0.|
|NatoStockNumber|**Optional.** NATO stock number code. 13 digits (0-9)|
|SymbolId|**Required.** A symbol identifier represented as a string. If not provided the symbol standard used is undefined.|
|SymbolAmplification|**Optional.** Text amplifications for the equipment's symbol. Static or very low update rate.|
|Disposition|**Required.** Formation position, location, orientation and speed.|
|CommunicationNetworks|**Optional.** Set of Communication Networks that equipment monitors and uses to communicate during a mission.|
|Resolution|**Optional.** Enumeration indicating the level of fidelity appropriate for instancing the unit or equipment in the simulation. Default value: NOT_SPECIFIED.|

### Installation

Representation of an initial or snapshot state of an installation/facility based on attributes defined in the NETN-ORG extensions of MSDL.

|Attribute|Description|
|---|---|
|UniqueId|***Inherited:*** **Required.** Unique Identifier.|
|Name|**Required.** A unique name of the installation.|
|Owner|**Required** Reference to the force, unit or equipment item owning or hosting the installation.|
|EntityType|**Required.** SISO-REF-010 code for entity type definitions. If unknown, use 0.0.0.0.0.0.0.|
|SymbolId|**Required.** A symbol identifier represented as a string. If not provided the symbol standard used is undefined.|
|SymbolAmplification|**Optional.** Text amplifications for the installation's symbol. Static or very low update rate.|
|Location|**Required.** Geographic location of the installation.|

## Force

A `Force` object represents a specific force or side and its relationship with other forces. Units belonging to a force all have the same relationship with units belonging to another force. The relation between forces can be asymmetrical, e.g. Force A can be hostile to B when B is neutral to A. The relation may change during a federation execution. Updates of the NETN-ORG Force relations attribute should be reflected and used by federates that depend on this information.

|Attribute|Description|
|---|---|
|UniqueId|***Inherited:*** **Required.** Unique Identifier.|
|ForceName|**Required** Name of the force/side.|
|Relations|**Optional:** Sequence of relations, force-relation. Default is an empty array. |

## FederateApplication

A `FederateApplication` object is used to represent the allocation of initial modelling responsibility of units, equipment items and installations.

|Attribute|Description|
|---|---|
|UniqueId|***Inherited:*** **Required.** Unique Identifier.|
|Name|**Required.** A unique name in the organization to group units and equipment items. This group name is used to determine the initial allocation of modelling responsibility of units and equipment items to a federate. The federation agreements should specify how this name is to be interpreted and how the allocation will be performed. A common agreement and practice are to use the federate name as group name, i.e. the units and equipment items are allocated to the federate with that name. Typically one application will be responsible for performing the allocation. Alternatives for the group name are for example: federate type name, a functional name.|
|Units|**Optional:**  The units for which the federate has the responsibility of simulating. Default is an empty list. |
|EquipmentItems|**Optional.**  The equipment for which the federate has the responsibility of simulating. Default is an empty list. |
|Installations|**Optional.**  The installations for which the federate has the responsibility of simulating. Default is an empty list. |

Note that each unit, equipment or installation is only allowed to be referenced in one `FederateApplication` object instance. 

## SISO MSDL Schema Derivative Work

The NETN-ORG FOM Module is associated with a set of XML Schemas developed based on the SISO MSDL Standard and adapted to capture additional aspects of ORBAT information and an initial allocation of modelling responsibilities to systems in a federated distributed simulation. The updated schemas only contain extensions, and any existing MSDL file is still valid according to the new schema. 

The main changes include:

- Introduce Holdings of equipment and consumables for Units 
- Use of NSNcode for equipment type
- Deployment information for initial allocation of modelling responsibilities for Units and EquipmentItems
- Add the possibility to extend the description of Equipment Items with additional elements
- Allow equipment items to be owned by other equipment
