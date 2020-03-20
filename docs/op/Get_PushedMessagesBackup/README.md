<!-- docs/op/Get_PushedMessagesBackup/README.md -->
# Get_PushedMessagesBackup

> Get the list of pushed messages for a certain period
> Useful to retrieve the messages that were not pushed or in exceptional cases the messages that were pushed but not procesed by your backend.

## Version info
- There is only one version

## Request
\* is mandatory

- [Login block](/detail/loginblock.md)*
- PushedMessagesSelection: _PushedMessagesSelection_
	- StartDateTime: start of the period for which you want to retrieve the pushed messages
	- EndDateTime: end of the period for which you want to check retrieve pushed messages
	- TypeOfMessages: _String_: Failure, Success or All

## Response
Derived from result object, contains Errors and Warnings: See [result object](/detail/resultobject.md)
- PushedMessages: _PushedMessages_
	- Messages: _array of Message_
		- Status: _Status_: Enum: Failure or Success
		- MessageJson: _String_: The message that was pushed
		- Response: _String_: The response we got from the server


## Example xml
**Request**
```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tran="http://transics.org">
   <soapenv:Header/>
   <soapenv:Body>
      <tran:Get_PushedMessagesBackup>
         <tran:Login>
            ...
         </tran:Login>
         <tran:pushedMessagesSelection>
            <tran:StartDateTime>2020-03-20T10:00:00</tran:StartDateTime>
            <tran:EndDateTime>2020-03-20T12:00:00</tran:EndDateTime>
            <tran:TypeOfMessages>Failed</tran:TypeOfMessages>
         </tran:pushedMessagesSelection>
      </tran:Get_PushedMessagesBackup>
   </soapenv:Body>
</soapenv:Envelope>
```

**Response**
```XML
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <soap:Body>
      <Get_PushedMessagesBackupResponse xmlns="http://transics.org">
         <Get_PushedMessagesBackupResult Executiontime="0.052">
            <Errors/>
            <Warnings/>
            <Messages>
               <Message>
                  <Status>Failure</Status>
                  <MessageJson>{"alarmId":12651770,"alarmType":"DynamicAlarm","alarmSubType":"","alarmText":"Alarm on 30 minutes","truckId":1111,"driverId":2222,"trailerId":-1,"timeStamp":"2020-03-20T09:00:00Z","position":{"latitude":16.3773,"longitude":63.0177,"address":""},"origin":{"rel":"","id":-1,"href":""},"updateDate":"2020-03-20T09:00:00.7729534Z"}</MessageJson>
               </Message>
               <Message>
                  <Status>Failure</Status>
                  <MessageJson>{"alarmId":12651809,"alarmType":"Geofencing","alarmSubType":"EnterGeoZoneAlarm","alarmText":"GeoFencing alert - Entered in testPUSH - DEMOA4 (DEMO ROMANIA).","truckId":3333,"driverId":4444,"trailerId":-1,"timeStamp":"2020-03-20T09:15:27Z","position":{"latitude":24.7992,"longitude":99.7401,"address":""},"origin":{"rel":"Geozone","id":9544,"href":""},"updateDate":"2020-03-20T09:15:28.9474435Z"}</MessageJson>
               </Message>
            </Messages>
            <NextStartDate>2020-03-20T10:30:00Z</NextStartDate>
         </Get_PushedMessagesBackupResult>
      </Get_PushedMessagesBackupResponse>
   </soap:Body>
</soap:Envelope>
```