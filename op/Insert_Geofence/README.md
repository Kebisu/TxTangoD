<!-- docs/op/Insert_Geofence/README.md -->
# Insert_Geofence

> The creation of circular zones that can trigger different kind of alarms: alarms when entering and/or leaving, alarms when an activity takes more than x minutes in this zone or alarms when not in the zone before a certain date and time.
>
> - It is not possible to create polygone geofence via the web services, this needs to be done via TX-CONNECT.

## Version info
- Version 2 adds the option to create a geofence based on an existing POI.

## Request
\* is mandatory, \*\* Either GeoValidity date or ETADate need to be used

- [Login block](/op/loginblock.md)*
- GeofenceInsert: _InterfaceGeoFenceInsert V2_
	- Geozones: _array of IntefaceGoeZone V2_
		- Name: _string_
		- Position: _Position_
			- Longitude: _double_
			- Latitude: _double_
		- Radius: _int32_
		- DriverAlarmText: _string
		- PoiID: _int32_
	- Active*: _boolean_, set true, otherwise an inactive geofence is created
	- ETADate**: _DateTime_, generate an alarm when not in the zone by this date-time
	- GeoValidityDate**: _GeoValidityDate_, the period that the alarm is valid for
		- BeginDate*: _DateTime_, should not be in the passed
		- EndDate*: _DateTime_
	- Name*: _string_
	- DriverAlarmText: _string_, what text should be shown to driver when the alarm occurs. 
	- NotifyHomeBase: _boolean_, alarm for the backoffice (TX-CONNECT, Web service, ...)
	- NotifyDriverByBeep: _boolean_
	- NotifyOnce: _boolean_, the alarm will only be triggered once for each vehicle
	- GeoFenceDirection*: _enumGeofenceDirection_: ENTER, LEAVE, ENTER\_LEAVE, alarm upon entering or leaving or both
	- GeoZonePositive: _boolean_, true: zone colours red when vehicle is inside, otherwise green. false: vica-versa
	- RestrictedActivity: _ActivityPlace_, give an alarm when an activity takes longer than x minutes, if this is used than the GeoFenceDirection will be ignored.
		- ID: _int32_
		- Name: _string_
		- MaxTimeOfExecution: _int32_

## Response
Derived from result object, contains Errors and Warnings: See [result object](/op/resultobject.md)
- result: _InsertGeoFenceResult_
	- GeoFenceID: _int64_, unique id of the geofence, need to be stored to easily interpret alarms via [Get_AlarmMessages](/op/Get_AlarmMessages/)
	- GeoFenceName: _string_
	- GeoZones: _array of InsertGeoZoneResult_
		-  GeoZoneTNR: _int64_, unique id of the geozone, need to be stored to easily interpret alarms via [Get_AlarmMessages](/op/Get_AlarmMessages/)
		-  GeoZoneSeq: _int64_
		-  GeoZoneName: _string_

## Example xml

**Request**

```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tran="http://transics.org">
   <soapenv:Header/>
   <soapenv:Body>
      <tran:Insert_GeoFence_V2>
         <tran:Login>
            ...
         </tran:Login>
         <tran:GeoFenceInsert>
            <tran:Active>true</tran:Active>
            <tran:GeoValidityDate>
               <tran:BeginDate>2019-01-08T09:30:00</tran:BeginDate>
               <tran:EndDate>2029-01-08T00:00:00</tran:EndDate>
            </tran:GeoValidityDate>
            <tran:Name>Lisboa customer</tran:Name>
            <tran:NotifyHomeBase>true</tran:NotifyHomeBase>
            <tran:GeoFenceDirection>ENTER_LEAVE</tran:GeoFenceDirection>
            <tran:GeoZones>
               <tran:InterfaceGeoZone_V2>
                  <tran:Name>Main site</tran:Name>
                  <tran:Position>
                     <tran:Longitude>-9.179815</tran:Longitude>
                     <tran:Latitude>38.705459</tran:Latitude>
                  </tran:Position>
                  <tran:Radius>500</tran:Radius>
               </tran:InterfaceGeoZone_V2>
            </tran:GeoZones>
         </tran:GeoFenceInsert>
      </tran:Insert_GeoFence_V2>
   </soapenv:Body>
</soapenv:Envelope>
```



**Response**

```XML
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <soap:Body>
      <Insert_GeoFence_V2Response xmlns="http://transics.org">
         <Insert_GeoFence_V2Result Executiontime="0.268">
            <Errors/>
            <Warnings/>
            <GeoFenceID>6143</GeoFenceID>
            <GeoFenceName>Lisboa customer</GeoFenceName>
            <GeoZones>
               <InsertGeoZoneResult>
                  <GeoZoneTNR>7153</GeoZoneTNR>
                  <GeoZoneSeq>1</GeoZoneSeq>
                  <GeoZoneName>Main site</GeoZoneName>
               </InsertGeoZoneResult>
            </GeoZones>
         </Insert_GeoFence_V2Result>
      </Insert_GeoFence_V2Response>
   </soap:Body>
</soap:Envelope>
```