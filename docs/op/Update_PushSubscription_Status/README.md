<!-- docs/op/Update_PushSubscriptionStatus/README.md -->
# Update_PushSubscriptionStatus

> Deactivate of reactivate a previously created subscription

## Version info
- There's is only one version

## Request
\* is mandatory

- [Login block](/detail/loginblock.md)*
- UpdateSubscriptionSelection: _UpdateSubscriptionSelection_
	- UpdateSubscriptions: _array of UpdateSubscription_
		- Feature: _string_: the feature you would like to update
		- SubscriptionStatus: _boolean_: false = deactivate, true = reactivate

## Response
Derived from result object, contains Errors and Warnings: See [result object](/detail/resultobject.md)
- result: _ResultSuccess_
	- Success: _string_: true or false

## Example xml
**Request**
Example, how to deactivate the NewAlarm feature, to no longer receive this messages
```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tran="http://transics.org">
   <soapenv:Header/>
   <soapenv:Body>
      <tran:Update_PushSubscriptions_Status>
         <tran:Login>
            ...
         </tran:Login>
         <tran:UpdateSubscriptionSelection>
            <tran:UpdateSubscriptions>
               <tran:UpdateSubscription>
                  <tran:Feature>NewAlarm</tran:Feature>
                  <tran:SubscriptionStatus>0</tran:SubscriptionStatus>
               </tran:UpdateSubscription>
            </tran:UpdateSubscriptions>
         </tran:UpdateSubscriptionSelection>
      </tran:Update_PushSubscriptions_Status>
   </soapenv:Body>
</soapenv:Envelope>
```

**Response**
```XML
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <soap:Body>
      <Update_PushSubscriptions_StatusResponse xmlns="http://transics.org">
         <Update_PushSubscriptions_StatusResult Executiontime="0.076">
            <Errors/>
            <Warnings/>
            <Success>true</Success>
         </Update_PushSubscriptions_StatusResult>
      </Update_PushSubscriptions_StatusResponse>
   </soap:Body>
</soap:Envelope>
```