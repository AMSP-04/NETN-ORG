# NETN-ORG
![overview](./images/overview.png)


## Introduction

Modelling of an organizational unit in a distributed simulation depend on its intra-organizational relationship with other units, e.g. superior, subordinate, and the relationship between organizations, e.g. friendly or hostile. This organizational information is normally provided to simulation systems as part of initialization based on the scenario.

The NATO Education and Training Network Organization Module (NETN ORG) is a specification of how to represent organizations in a federated distributed simulation.

The specification is based on IEEE 1516 High Level Architecture (HLA) Object Model Template (OMT) and primarily intended to support interoperability in a federated simulation (federation) based on HLA. A Federation Object Model (FOM) Module is used to specify how data is represented and exchanged in the federation. The NETN-ORG FOM module is available as an XML file for use in HLA based federations.

### Purpose

The NETN-ORG FOM Module provides a common standard interface for representation of the state of units including command structure and relationship between organizations. This representation can be used for setting the initial state of simulated entities, capturing subsequent snapshot states and for dynamic change of organizational relationships.

### Scope

- Capture unit state for (re-)initialization and snapshots
- Dynamic changes of organization command structure
- Dynamic changes of relationships between organizations
  - Force relationships
  - Support relationships

## Licence

Copyright (C) 2019 NATO/OTAN.
This work is licensed under a [Creative Commons Attribution-NoDerivatives 4.0 International License](LICENCE.md). 

The work includes the [NETN-ORG.xml](NETN-ORG.xml) FOM Module and [documentation](NETN-ORG.md).

Above licence gives you the right to use and redistribute the NETN FOM Module (XML file and Documentation) in its entirety without modification. You are also allowed to develop your own new FOM Modules (in separate XML files and separate documentation) that build-on/extends the NETN module by reference and including neccessary scaffolding classes. You are NOT allowed to modify this FOM Module or its documentation without prior permission by the NATO Modelling and Simulation Group. 

## Versions, updates and extentions

All updates and versioning of this work is coordinated by the NATO Modelling and Simulation Coordination Office (MSCO), managed by the NATO Modelling and Simulation Group (NMSG) and performed as NATO Science and Technology Organization (STO) technical activities in support of the NMSG Modelling and Simulation Standards Subgroup (MS3).

Feedback on the use of this work, suggestions for improvements and identified issues are welcome and can be provided using GitGub issue tracking. To engage in the development and update of this FOM Module please contact your national NMSG representative.

Version numbering of this FOM Module and associated documentation is based on the following principles:

* New official version number is assigned and in effect only when new release is made in the Master branch.
* Updates in the Develop branch will not change version number.
* In the FOM Module useHistory information include only information on official releases.
* Update of the major version number is made if the change constitute a major restructuring, merging, addition or redefinition of semantics that breaks backward compatibility or cover entirely new concepts.
* Update of the minor version number is made if the change constitute a minor additions to existing concepts and editorial changes that do not break backward compatibility but may require updates of software to use new concepts.
* Patches are released to fix minor issues that do not break backward compatibility.

|Version|Description|
|---|---|
|v 1.0.0 (RC1) |Initial release of NETN ORG FOM Module based on MSDL and Viking Computer Assisted eXercise (CAX).|

[Changelog](changelog.md)

## Documentation

[Full Documentation](NETN-ORG.md)
