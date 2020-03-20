<!-- docs/op/Get_PushedMessagesBackupSummary/README.md -->
# Get_PushedMessagesBackupSummary

> A web service to see how many messages were pushed and how many failed.  
> To check if you need to use the backup retrieval method [Get_PushedMessagesBackup](/op/Get_PushedMessagesBackup/) or not

## Version info
- There is only one version

## Request
\* is mandatory

- [Login block](/detail/loginblock.md)*
- PushedMessagesSummarySelection: _PushedMessagesSummarySelection_
	- StartDateTime: _datetime_: start of the period for which you want to check the push messages
	- EndDateTime: _datetime_: end of the period for which you want to check push messages

## Response
Derived from result object, contains Errors and Warnings: See [result object](/detail/resultobject.md)
- PushMessageStatusCount: _array of PushMessageStatusCount_
	- Status: _string_: failed or succeeded
	- Count: _int32_: the number of messages that have this state


## Example xml
**Request**
```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tran="http://transics.org">
   <soapenv:Header/>
   <soapenv:Body>
      <tran:Get_PushedMessagesBackupSummary>
         <tran:Login>
            ...
         </tran:Login>
         <tran:pushedMessagesSummarySelection>
            <tran:StartDateTime>2020-03-20T12:00:00</tran:StartDateTime>
            <tran:EndDateTime>2020-03-21T12:00:00</tran:EndDateTime>
         </tran:pushedMessagesSummarySelection>
      </tran:Get_PushedMessagesBackupSummary>
   </soapenv:Body>
</soapenv:Envelope>
```

**Response**
```XML
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <soap:Body>
      <Get_PushedMessagesBackupSummaryResponse xmlns="http://transics.org">
         <Get_PushedMessagesBackupSummaryResult Executiontime="0.052">
            <Errors/>
            <Warnings/>
            <PushMessageStatusCounts>
               <PushMessageStatusCount>
                  <Status>Failure</Status>
                  <Count>16</Count>
               </PushMessageStatusCount>
            </PushMessageStatusCounts>
         </Get_PushedMessagesBackupSummaryResult>
      </Get_PushedMessagesBackupSummaryResponse>
   </soap:Body>
</soap:Envelope>
```