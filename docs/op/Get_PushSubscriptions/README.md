<!-- docs/op/Get_PushSubscriptions/README.md -->
# Get_PushSubscriptions

> Retrieve the list of subsciprtions linked to that Integrator

## Version info
- There's is only one version

## Request
\* is mandatory
The request only needs a login block

- [Login block](/detail/loginblock.md)*

## Response
Derived from result object, contains Errors and Warnings: See [result object](/detail/resultobject.md)
The response only contains the subscriptions for the integrator that was used in the login block of the request
- result: _Get_PushSubscriptionsResult_
	- Features: _array of FeatureResult_
		- Status: _boolean_: true = active, false = inactive
		- Feature: _string_: name of the feature that was subscribed to
		- FeatureParameters: _string_: JSON object containing a parameters structure that applies a filter on the the feature
        - StreamingTechnologyType: _string_: The technology that is used for push. Currently always 'WebAPI'
        - StreamingTechnologyDetails: _string_: JSON object containing the URL of the WebAPI

## Example xml
**Request**
```XML
	<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tran="http://transics.org">
	   <soapenv:Header/>
	   <soapenv:Body>
	      <tran:Get_PushSubscriptions>
	         <tran:Login>
	            ...
	         </tran:Login>
	      </tran:Get_PushSubscriptions>
	   </soapenv:Body>
	</soapenv:Envelope>
```

**Response**
```XML
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <soap:Body>
      <Get_PushSubscriptionsResponse xmlns="http://transics.org">
         <Get_PushSubscriptionsResult Executiontime="0.033">
            <Errors/>
            <Warnings/>
            <Features>
               <FeatureResult>
                  <Feature>NewAlarm</Feature>
                  <FeatureParameters>{'AlarmTypes':['Geofencing','ActivityTakesTooLong'],'AlarmPOIEnrichmentRequired':1}</FeatureParameters>
                  <StreamingTechnologyType>WebAPI</StreamingTechnologyType>
                  <StreamingTechnologyDetails>{"URL":"https://en9n8ljouo5e.x.test.net"}</StreamingTechnologyDetails>
                  <Status>true</Status>
               </FeatureResult>
            </Features>
         </Get_PushSubscriptionsResult>
      </Get_PushSubscriptionsResponse>
   </soap:Body>
</soap:Envelope>
```