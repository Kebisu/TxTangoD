<!-- docs/op/Update_Vehicle_V2/README.md -->
# Update_Vehicle_V2

> Changing vehicle data, things like codes, license plate, VIN, Instruction set, ... can all be changed 
> This web service can also be used to link vehicles to devices

## Version info
- V2: 
	- Allows you to specify which identifier will not change and use that one to update your vehicle: via the VehicleToUpdate fields
	- Possibility to link a truck to a device. 
		- REMARK: This needs to be activated by service desk before it can be used
- Always try to use the latest version

## Request
\* is mandatory

- [Login block](/detail/loginblock.md)*
- All the other input parameters

## Response
Derived from result object, contains Errors and Warnings: See [result object](/detail/resultobject.md)
- result: _ResultInfo_
	- ID: _String_: the ID of the vehicle that was updated

## Example xml
Example how to link a vehicle to a device and set hte instruction set
**Request**
```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tran="http://transics.org">
   <soapenv:Header/>
   <soapenv:Body>
      <tran:Update_Vehicle_V2>
         <tran:Login>
            ...
         </tran:Login>
         <tran:VehicleUpdate>
            <!--decide which field you will use to identify the vehicle.-->
            <!--this field cannot be updated in the same request-->
            <tran:VehicleToUpdate>
               <tran:IdentifierVehicleType>LICENSE_PLATE</tran:IdentifierVehicleType>
               <tran:Id>1-TEST-100</tran:Id>
            </tran:VehicleToUpdate>
            <tran:ExtraInformation>Linking the vehicle to the device 357207054231717</tran:ExtraInformation>
            <!--Specify the type of unit, otherwise the linking process is not exectued-->
            <tran:TypeOfObc>TXSky</tran:TypeOfObc>
            <!--Number of the instruction set, can be retrieved via Get_ActivityList_Vx-->
            <tran:InstructionSetNumber>176</tran:InstructionSetNumber>
            <!--Serial number of the device-->
            <tran:DeviceSerial>357207054231717</tran:DeviceSerial>
         </tran:VehicleUpdate>
      </tran:Update_Vehicle_V2>
   </soapenv:Body>
</soapenv:Envelope>
```

**Response**
```XML

```