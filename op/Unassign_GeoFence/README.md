<!-- docs/op/Unassign_GeoFence/README.md -->
# Unassign_GeoFence

> Unassign (remove) one or more geofences from one or more vehicles

## Version info
- There's is only one version

## Request
\* is mandatory

- [Login block](/op/loginblock.md)*
- GeoFenceSelection* _UnAssignGeoFenceSelection_
	- VehicleListStrategySelection*: _VehicleListStrategySelection_, the strategy needs to be initialized with a VehicleStrategyList or a TrailerStrategyList to filter either on vehicles or trailers
		- IdentifierVehicle: _array of IdentifierVehicle_
			- Id: _string_
			- IdentifierVehicleType: _enumIdentifierVehicleType_: ID, TRANSICS\_ID, CODE, LICENSE\_PLATE
	- GeoFences*: _array of GeoFence_V2_, list of geofence objects that need to be passed via Transics ID or Name
		- GeoFence: _ArrayOfIdentifierGeoFence_
			- IdentifierGeoFence: _IdentifierGeoFence_
			- IdentifierType: _enumGeofenceIdentifierType_: TRANSICS\_ID, NAME
			- ID: _string_

## Response
Derived from result object, contains Errors and Warnings: See [result object](/op/resultobject.md)
- result: _UnAssignGeoFenceResult_
	- GeoFences: _array of IdentifierGeofenceResult_
		- TransicsID: _int64_
		- Name: _string_
	- Vehicles: _array of IdentifierVehicleResult_
		- LicensePlate: _string_
		- ID: _string_
		- TransicsID: _int64_
		- Code: _string_
		- Filter: _string_


## Example xml
**Request**
```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xmlns:tran="http://transics.org">
   <soapenv:Header/>
   <soapenv:Body>
      <tran:Unassign_GeoFence>
         <tran:Login>
            ...
         </tran:Login>
         <tran:UnAssignGeoFenceSelection>
            <tran:VehicleListStrategySelection xsi:type="tran:VehicleStrategyList">
               <tran:IdentifierVehicle>
                  <tran:IdentifierVehicle>
                     <tran:IdentifierVehicleType>ID</tran:IdentifierVehicleType>
                     <tran:Id>ABC123</tran:Id>
                  </tran:IdentifierVehicle>
               </tran:IdentifierVehicle>
            </tran:VehicleListStrategySelection>
            <tran:GeoFences>
               <tran:GeoFence>
                  <tran:IdentifierGeoFence>
                     <tran:IdentifierType>TRANSICS_ID</tran:IdentifierType>
                     <tran:ID>45357</tran:ID>
                  </tran:IdentifierGeoFence>
               </tran:GeoFence>
            </tran:GeoFences>
         </tran:UnAssingGeoFenceSelection>
      </tran:Unassign_GeoFence>
   </soapenv:Body>
</soapenv:Envelope>
```

**Response**
```XML
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <soap:Body>
      <UnAssign_GeoFenceResponse xmlns="http://transics.org">
         <UnAssign_GeoFenceResult Executiontime="0.13">
            <Errors/>
            <Warnings/>
            <GeoFences>
               <IdentifierGeofenceResult>
                  <TransicsID>45357</TransicsID>
                  <Name>TestGeoSmart</Name>
               </IdentifierGeofenceResult>
            </GeoFences>
            <Vehicles>
               <IdentifierVehicleResult>
                  <ID>ABC123</ID>
                  <TransicsID>2688</TransicsID>
                  <Code>Ext_ABC123</Code>
                  <LicensePlate>LIC-NEW</LicensePlate>
               </IdentifierVehicleResult>
            </Vehicles>
         </UnAssign_GeoFenceResult>
      </UnAssign_GeoFenceResponse>
   </soap:Body>
</soap:Envelope>
```