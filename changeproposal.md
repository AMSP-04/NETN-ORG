# Change Proposal

### Comments on RC v0.2.3

#### Federate
Is the Federate object class a more general extension/concept possibly suited for NETN-BASE? I would imagine that other attribtues should be associated with the Federate object such as a Federate´s ability to participate in different NETN design patterns. Other information might also be interesting to publish. 

The Units attribute is the published allocation of modelling responsibilities. Is the interpretation that this attribute is static (updates only once) or does it always reflect current modelling responsibility? If the attribute is updated what is meant to happen? What if the modelling responibility is shared or is is basically stating owner of privilegeToDelete attribute of an object instance?

Name of Units attribute can be a bit clearer - e.g. AlllocatedUnits or ModellingResponsibility

If moved to NETN-BASE the Federate object class should stand by its own and not be a subclass of ORG_Root which also mean that the OrbatObject class can be ellimitated.

#### Force

Units belong to an Organization (Force). 
Should the Force object class be renamed Organization to be more general. Civilian organizations are rarely considered a "Force". Similarly the "Force" attribute of Unit should be called "Organization".

Organizations have relationships regarding "hostility". Do we envision other organizational relationships? Rename "Relations" attribute to e.g. "ForceRelations".

#### Unit

It is unclear which of the Unit's attribute reflects GroundTruth and are which are considered static initialization data. Information used for initialization should be reflected as a single attribute with Fixed Record Datatype and with an unambigous name.
E.e. 
- SuperiorUnit
- Force (rename to Organization) - if updated also require update of SuperiorUnit
- 
- UnitType (FixedRecord) - probably fixed and never change 
    - EntityType
    - SymbolIdentifier
    - UniqueDesignation
    - Echelon
    - CategoryCode
    - CommandFunctionIndicatorCode
    - SizeCode
    - ArmCategoryCode
    - TypeServiceCode
    - IsSimulationEntity
    - HigherFormation (can/should this change during runtime)
    - IFF
- IntitialData (FixedRecord) - probably only updated if new init data is generated from simulation ground truth. Like a snapshot for use as initial data in the future. 
    - Holdings
    - EmbarkedIn
    - CombatEffectiveness
    - Location
    - Direction
    - Speed
    - FormationPosition
    - OwnFormation

Units may have relationship with other Units, e.g. A Logistics Unit may support another Unit for delivering supplies and transport services (possibly to a unit in a different Organization/Force). This may be reflected in the NETN-LOG module as a UnitRelation object or similar?? Or LOG_Unit subclass to Unit ???