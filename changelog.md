## Changelog NETN-ORG

### v1.0 - Initial version developed by MSG-163. Release included in NETN-FOM v3.0



### v2.0 - Updated version developed by MSG-191. Release included in NETN-FOM v4.0

* Removed dependency `NETN-BASE` 
* Added dependency `NETN-MRM` 
 
 
* Replaced `ORG_Root` attribute `UniqueId` with NETN-BASE `HLAobjectRoot` attribute `UniqueId` 
* Added `ORG_Root` attribute `Name` 
 
* Added object class `OrganizationElement` 
 
* Replaced `Unit` attribute `Name` with `ORG_Root` attribute `Name` 
* Replaced `Unit` attribute `Force` with `OrganizationElement` attribute `Organization` 
* Replaced `Unit` attribute `EntityType` with `OrganizationElement` attribute `EntityType` 
* Replaced `Unit` attribute `SymbolId` with `OrganizationElement` attribute `SymbolId` 
* Replaced `Unit` attribute `Disposition` with `OrganizationElement` attribute `Location` 
* Replaced `Unit` attribute `CommunicationNetworks` with NETN-COM `Unit` attribute `CommunicationNetworks` 
* Replaced `Unit` attribute `EmbarkedIn` with `OrganizationElement` attribute `HostUnit` 
* Replaced `Unit` attribute `SymbolAmplification` with `OrganizationElement` attribute `SymbolAmplification` 
* Added `Unit` attribute `HigherHeadquarters` 
 
* Renamed object class `EquipmentItem` to `Equipment` 
* Replaced `EquipmentItem` attribute `Name` with `ORG_Root` attribute `Name` 
* Replaced `EquipmentItem` attribute `EntityType` with `OrganizationElement` attribute `EntityType` 
* Removed `EquipmentItem` attribute `NatoStockNumber` 
* Replaced `EquipmentItem` attribute `SymbolId` with `OrganizationElement` attribute `SymbolId` 
* Replaced `EquipmentItem` attribute `Disposition` with `OrganizationElement` attribute `Location` 
* Replaced `EquipmentItem` attribute `CommunicationNetworks` with NETN-COM `Equipment` attribute `CommunicationNetworks` 
* Removed `EquipmentItem` attribute `Resolution` 
* Replaced `EquipmentItem` attribute `MountedOn` with `OrganizationElement` attribute `HostUnit` 
* Replaced `EquipmentItem` attribute `SymbolAmplification` with `OrganizationElement` attribute `SymbolAmplification` 
 
* Replaced `Installation` attribute `Name` with `ORG_Root` attribute `Name` 
* Renamed `Installation` attribute `Owner` to `UnitInCommand` 
* Replaced `Installation` attribute `EntityType` with `OrganizationElement` attribute `EntityType` 
* Replaced `Installation` attribute `SymbolId` with `OrganizationElement` attribute `SymbolId` 
* Replaced `Installation` attribute `Location` with `OrganizationElement` attribute `Location` 
* Replaced `Installation` attribute `SymbolAmplification` with `OrganizationElement` attribute `SymbolAmplification` 
 
* Renamed object class `Force` to `Organization` 
* Replaced `Force` attribute `Name` with `ORG_Root` attribute `Name` 
* Added `Organization` attribute `ForceIdentifier` 
* Added `Organization` attribute `Nation` 
 
* Moved object class `FederateApplication` to NETN-TMR 
 
* Removed datatype `ArrayOfCommunicationNetworks` 
* Removed datatype `CommunicationNetworkStruct` 
* Removed datatype `CommunicationServiceTypeEnum32` 
* Removed datatype `DispositionStruct` 
* Added datatype `ForceIDEnum8` 
* Removed datatype `FormationInt32` 
* Removed datatype `FormationPositionStruct` 
* Replaced datatype `HostilityStatusCodeEnum32` with NETN-BASE datatype `HostilityStatusCodeEnum32` 
* Removed datatype `ModelResolutionTypeEnum32` 
* Removed datatype `NatoStockNumberArray13` 
* Replaced datatype `Text255` with `HLAunicodeString` 
 
* Replaced datatype `EquipmentSymbolAmplificationStruct` with NETN-BASE datatype `SymbolAmplificationVariant` 
* Replaced datatype `UnitSymbolAmplificationStruct` with NETN-BASE datatype `SymbolAmplificationVariant` 
* Replaced datatype `InstallationSymbolAmplificationStruct` with NETN-BASE datatype `SymbolAmplificationVariant` 
 
* Added `BaseEntity` attribute `Organization`


* Replaced datatype `Text5` with NETN-BASE datatype `Text5` 
* Replaced datatype `Text21` with NETN-BASE datatype `Text21` 
* Replaced datatype `Text24` with NETN-BASE datatype `Text24` 
* Replaced datatype `Text20` with NETN-BASE datatype `Text20` 
* Replaced datatype `Text9` with NETN-BASE datatype `Text9` 
* Replaced datatype `Text3` with NETN-BASE datatype `Text3` 
* Replaced datatype `Text2` with NETN-BASE datatype `Text2` 
* Replaced datatype `Text1` with NETN-BASE datatype `Text1` 
* Replaced datatype `Text15` with NETN-BASE datatype `Text15` 
* Replaced datatype `Text8` with NETN-BASE datatype `Text8` 


