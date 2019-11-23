# NETN-ORG
Copyright (C) 2019 NATO/OTAN.
This work is licensed under a [Creative Commons Attribution-NoDerivatives 4.0 International License](LICENCE.md).

## Introduction
Modelling of an organizational unit in a distributed simulation depends on its intra-organizational relationship with other units, e.g. superior, subordinate, and the relationship between organizations, e.g. friendly or hostile. This organizational information is normally provided to simulation systems as part of initialization based on the scenario.

The NATO Education and Training Network Organization Module (NETN ORG) is a specification of how to represent organizations in a federated distributed simulation.

The specification is based on IEEE 1516 High Level Architecture (HLA) Object Model Template (OMT) and primarily intended to support interoperability in a federated simulation (federation) based on HLA. A Federation Object Model (FOM) Module is used to specify how data is represented and exchanged in the federation. The NETN-ORG FOM module is available as an XML file for use in HLA based federations.

### Purpose

The NETN-ORG FOM Module provides a common standard interface for the representation of the state of units including command structure and relationship between organizations. This representation can be used for setting the initial state of simulated entities, capturing subsequent snapshot states and for dynamic change of organizational relationships.

### Scope

- Capture unit state for (re-)initialization and snapshots
- Dynamic changes in an organization command structure
- Dynamic changes in relationships between organizations
  - Force relationships
  - Support relationships


## Fundamentals

During a simulation, the organizational relationships may change. Dynamic changes in the task organization may include new and or rearranged unit structure. The relationship between organizations may also change during the execution of a scenario. These changes can be represented in the NETN-ORG FOM module as updates of corresponding attributes reflected by all subscribing simulation systems.

In a federated distributed simulation, not all units and/or equipment in the organization are simulated, i.e. represented as ground-truth Aggregate or Platform entities. The initial allocation of modelling responsibility of specific units can be provided in NETN-ORG to indicate which units and which federate should register and model the ground truth entity.

The simulated entities in an application are initialized with the ORBAT data, either reading the MSDL file or subscribing to the object classes in NETN-ORG FOM module.

All object classes have a UUID attribute which is a unique identifier, this identifier is static and is valid both in a federation execution and between federation executions. Applications with the ORBAT data is aware of all units in the ORBAT even if there not any aggregate or physical entities that represent the Unit in the federation execution.

<img src=./images/objectclasses.png>

**Figure: ORG FOM Object Classes**

#### Unit

Specifies Unit attributes, the attributes are statically or dynamic. The Unit attribute values define the initialization data for aggregate and physical entities, dynamic attributes may be updated during the execution of the federation and may be saved as a snapshot of the current state in the federation execution.

All defined Units does not need to have a simulation entity (aggregate or physical) representation in the federation execution. The existence of simulation entities depends on the aggregation level of the federation and participated applications. E.g. in an exercise is the main interest at company level and in another exercise it may be at platform level, both levels can be supported by the same ORBAT definition (file or Unit instances in the federation execution).

Many attributes in the Unit object class has an equivalent attribute at the object classes AggregateEntity (RPR)or NETN_Aggregate, the object classes in NETN that defines the extension of RPR physical entities also has some equivalent attributes. Some of these equivalent attributes has the same name and some have the same datatype (encoding and decoding).

#### Force

Units in an ORBAT belongs to a Force. 
 
Forces have relations to each other which is specified in the attribute Relations. 
The relation between forces is defined by HostilityStatusCodeEnum32 which is derived from JC3IEDM, e.g. FR (Friendly),  HO (Hostile). 
The relation between Force A and Force B does not have to be the same as the relation between B and A. 
The relation may change during a federation execution.
The relations between forces is specified in a much more understandable way in comparison to RPR. Relation between forces in RPR is done with enumerated values, not an object class representation as in the NETN ORG FOM.

#### Federate

In the ORBAT is units assigned to a Federate which will have the modelling responsibility for these simulated entities in a federation execution. The assignment can be done by reading the ORBAT file and produce the ORBAT for the application prior to the execution of the federation or subscribe to the object classes Unit and Federate and register the assigned aggregate and physical entities.

## Capture unit state for (re-)initialization and snapshots
## Dynamic changes of organization command structure
## Dynamic changes of Force relationships
## Dynamic changes of Support relationships
