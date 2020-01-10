<!-- docs/op/Get_Vehicles.md -->
# Get_Vehicles

> List of vehicles with some real time infomration like driver, position, activity, ...

## Version info
- Use version 12
- As of version 10, the filter on date-time is removed, because this function should return a overview of the last information of all vehicles. 
- Planning information (current trip and last place) is in the response for V7 to V12, but default behiour is to leave this information empty for V7 to V11. As of V12 we have a specific flag *IncludePlanningInfo*

## Request
\* is mandatory

- [Login block](/op/loginblock.md)*
- VehicleSelection: _InterfaceVehicleSelection\_V5_
	- Identifiers: _array of IdentifierVehicle_
		- Id: _string_
		- IdentifierVehicleType: _enumIdentifierVehicleType_: ID, TRANSICS\_ID, CODE, LICENSE\_PLATE
	- IncludePosition: _boolean_
	- IncludeActivity: _boolean_
	- IncludeDrivers: _boolean_
	- IncludeObcInfo: _boolean_
	- IncludeETAInfo: _boolean_
	- IncludeTemperatureInfo: _boolean_
	- IncludeInfoFields: _boolean_
	- IncludeUpdateDates: _boolean_
	- IncludeInactive: _boolean_
	- IncludeLastTextMessageInboxOutbox: _boolean_
	- IncludeLastAlarmMessage: _boolean_
	- IncludeBlockedVehicleInfo: _boolean_
	- IncludeCompanyCardInfo: _boolean_
	- IncludeVehicleProfile: _boolean_
	- IncludeNextStopInfo: _boolean_
	- IncludeExtraTruckInfo: _boolean_
	- IncludeGroups: _boolean_
	- IncludeRented: _boolean_
	- IncludePlanningInfo: _boolean_
	- DiagnosticFilter: _array of DiagnosticSearchItem_
		- DiagnosticIdentifier: _string_
		- DiagnosticType: _enumDiagnosticType_: ID, NAME

## Response
Derived from result object, contains Errors and Warnings: See [result object](/op/resultobject.md)
- result: _InterfaceGetVehicleResult V12_
	- Vehicles: array of _InterfaceVehicleResult V12_
		- VehicleID: _string_
		- VehicleExternalCode: _string_
		- LicensePlate: _string_
		- VehicleTransicsID: _Int64_
		- VehicleFleetNumber: _string_
		- ShortName: _string_
		- Inactive: _boolean_

## Example code
See [IWSLogin()](/samplecode/iwslogin) & [IsValidResult()](/samplecode/isvalidresult)

```csharp
	IWS.InterfaceVehicleSelection_V2 vehSel = new IWS.InterfaceVehicleSelection_V2();
	vehSel.IncludePosition = true;
	vehSel.ExcludeInactive = true;
	vehSel.IncludeDrivers = true;

	IWS.InterfaceGetVehicleResult_V7 vehRes = _iwsService.Get_Vehicles_V7(IWSLogin(), vehSel);
	
	//Does the response congtains errors?
	if (IsValidResult(vehRes))
	{
		//Loop over all the vehicles in the response
		foreach (IWS.InterfaceVehicleResult_V7 veh in vehRes.Vehicles)
        {
			//Do some logic with the veh.
		}
	}
```

## Example xml
**Request**
```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tran="http://transics.org">
   <soapenv:Header/>
   <soapenv:Body>
      <tran:Get_Vehicles_V12>
         <tran:Login>
            <tran:Dispatcher>...</tran:Dispatcher>
            <tran:Password>...</tran:Password>
            <tran:SystemNr>...</tran:SystemNr>
            <tran:Integrator>...</tran:Integrator>
            <tran:Language>EN</tran:Language>
         </tran:Login>
         <tran:VehicleSelection>
         	<tran:Identifiers/>
            <tran:IncludePosition>false</tran:IncludePosition>
            <tran:IncludeActivity>false</tran:IncludeActivity>
            <tran:IncludeDrivers>true</tran:IncludeDrivers>
            <tran:IncludeObcInfo>false</tran:IncludeObcInfo>
            <tran:IncludeETAInfo>false</tran:IncludeETAInfo>
            <tran:IncludeTemperatureInfo>false</tran:IncludeTemperatureInfo>
            <tran:IncludeInfoFields>false</tran:IncludeInfoFields>
            <tran:IncludeUpdateDates>false</tran:IncludeUpdateDates>
            <tran:IncludeInactive>false</tran:IncludeInactive>
            <tran:IncludeLastTextMessageInboxOutbox>false</tran:IncludeLastTextMessageInboxOutbox>
            <tran:IncludeLastAlarmMessage>false</tran:IncludeLastAlarmMessage>
            <tran:IncludeBlockedVehicleInfo>false</tran:IncludeBlockedVehicleInfo>
            <tran:IncludeCompanyCardInfo>false</tran:IncludeCompanyCardInfo>
            <tran:IncludeVehicleProfile>false</tran:IncludeVehicleProfile>
            <tran:IncludeNextStopInfo>false</tran:IncludeNextStopInfo>
            <tran:IncludeExtraTruckInfo>false</tran:IncludeExtraTruckInfo>
            <tran:IncludeGroups>false</tran:IncludeGroups>
            <tran:IncludeRented>false</tran:IncludeRented>
            <tran:IncludePlanningInfo>true</tran:IncludePlanningInfo>
         </tran:VehicleSelection>
      </tran:Get_Vehicles_V12>
   </soapenv:Body>
</soapenv:Envelope>
```

**Response**
```XML
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <Get_Vehicles_V12Response xmlns="http://transics.org">
      <Get_Vehicles_V12Result Executiontime="27.458">
        <Errors />
        <Warnings/>
        <Vehicles>
          <InterfaceVehicleResult_V12>
            <VehicleFleetNumber>??</VehicleFleetNumber>
            <VehicleID>SKY_SIM</VehicleID>
            <VehicleExternalCode />
            <LicensePlate>SKY_SIM</LicensePlate>
            <Inactive>false</Inactive>
            <CanBusConnection xsi:nil="true" />
            <VehicleTransicsID>195579</VehicleTransicsID>
            <Modified>2018-10-30T10:09:50</Modified>
            <CurrentKms xsi:nil="true" />
            <FuelLevel xsi:nil="true" />
            <FuelLevelIndex xsi:nil="true" />
            <RefrigeratorIndex xsi:nil="true" />
            <Speed>0</Speed>
            <ActivityCompleted xsi:nil="true" />
            <Driver>
              <ID>VDU</ID>
              <TransicsID>244356</TransicsID>
              <Code>KCL</Code>
              <Filter />
              <LastName>Claerhout</LastName>
              <FirstName>Koen</FirstName>
              <FormattedName>Claerhout Koen</FormattedName>
            </Driver>
            <Maintenance>-1</Maintenance>
            <Remaining>0</Remaining>
            <AutoFilter />
            <FormattedName>SKY_SIM</FormattedName>
          </InterfaceVehicleResult_V12>

```