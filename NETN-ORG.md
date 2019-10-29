# NETN-ORG
Copyright (C) 2019 NATO/OTAN.
This work is licensed under a [Creative Commons Attribution-NoDerivatives 4.0 International License](LICENCE.md).

## Introduction
A military ORBAT defines the participants, simulated entities, in a federated distributed simulation.

The NATO Education and Training Network Organization Module (NETN ORG) is a specification of how to model entities (aggregate and physical), the hierarchy of these entities, the relation between entities and the  equipment at the entities.

The specification is based on IEEE 1516 High Level Architecture (HLA) Object Model Template (OMT) and primarily intended to support interoperability in a federated simulation (federation) based on HLA. A Federation Object Model (FOM) Module is used to specify how data is represented and exchanged in the federation. The NETN-ORG FOM module is available as an XML file for use in HLA based federations.

### Purpose
Publish an ORBAT in a HLA Federation Execution and support saving of an ORBAT (MSDL format) between executions of a federation and restoring of an ORBAT from saved data in a federation execution.

MSDL is a SISO standard and many applications uses MSDL for the specification of an ORBAT, these applications read and writes files with the MSDL format. With a HLA FOM can this data be published as object instances in a federation execution which implies that applications without the functionality to read MSDL files can achieve the ORBAT data. 

The simulated entities in an application is initialized with the ORBAT data, either reading the MSDL file or subscribing to the object classes in NETN-ORG FOM module.

All object classes have a UUID attribute which is a unique identifier, this identifier is static and is valid both in a federation execution and between federation executions. Applications with the ORBAT data is aware of all units in the ORBAT even if there not any aggregate or physical entities that represents the Unit in the federation execution.

### Scope

<img src=./objectclasses.png>

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

