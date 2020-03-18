<!-- docs/op/Assign_GeoFence/README.md -->
# Assign_GeoFence

> Assign one or more geofences from one or more vehicles

## Version info
- There's is only one version

## Request
\* is mandatory

- [Login block](/detail/loginblock.md)*
- SubscriptionSelection* _SubscriptionSelection_
	- Features*: _array of FeatureInfo_: an array of features that you want to subscibe to, with the endpoint where they need to be pushed
		- Feature: FeatureInfo_
			- Feature: _string_: name of the feature that you would like to subscribe to
			- FeatureParameters: _string_: JSON object containing a parameters structure that matches the feature you are subscribing to
         - StreamingTechnologyType: _string_: Currently always 'WebAPI'
         - StreamingTechnologyDetails: _string_: JSON object containing the URL of the WebAPI

## Response
Derived from result object, contains Errors and Warnings: See [result object](/detail/resultobject.md)
- result: _Add_PushSubscriptionsResult_
	- Success: _string_: true or false

## Example xml
**Request**
```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tran="http://transics.org">
   <soapenv:Header/>
   <soapenv:Body>
      <tran:Add_PushSubscriptions>
         <tran:Login>
            ...
         </tran:Login>
         <tran:SubscriptionSelection>
            <tran:Features>
               <tran:FeatureInfo>
                  <tran:Feature>NewAlarm</tran:Feature>
                  <tran:FeatureParameters>{'AlarmTypes':['Geofencing','ActivityTakesTooLong','DeadlineReadConfirmation','PlanningActivityTakesTooLong','ExternalDevice','CorridorAlarm','LowBattery','Pto','SpeedThresHold','RpmThresHold','EndQuestionPathNotCompletedAlarm','NextStop','Sos','DrivingTimes','Temperature','FuelDecreaseAlarm','HarshBrakeAlarm','DrivingWithoutIsoCableAlarm','RollOverStabilitySupportAlarm','EbsStateAlarm','TyrePressureAlarm','DoorlockAlarm','SensorAlarm','DynamicAlarm','RemoteDiagnosticsAlarm','NoCommunicationAlarm','UnknownDriverForObc','HarshAccelerationAlarm','MaxIdlingAlarm','FuelIncreaseAlarm','SufficientBrakeLiningAlarm','AntiLockBrakingSystemAlarm'],'AlarmPOIEnrichmentRequired':1}</tran:FeatureParameters>
                  <tran:StreamingTechnologyType>WebAPI</tran:StreamingTechnologyType>
                  <tran:StreamingTechnologyDetails>{"URL":"https://webhook.site/...."}</tran:StreamingTechnologyDetails>
               </tran:FeatureInfo>
            </tran:Features>
         </tran:SubscriptionSelection>
      </tran:Add_PushSubscriptions>
   </soapenv:Body>
</soapenv:Envelope>
```

**Response**
```XML
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <soap:Body>
      <Add_PushSubscriptionsResponse xmlns="http://transics.org">
         <Add_PushSubscriptionsResult Executiontime="0.116">
            <Errors/>
            <Warnings/>
            <Success>true</Success>
         </Add_PushSubscriptionsResult>
      </Add_PushSubscriptionsResponse>
   </soap:Body>
</soap:Envelope>
```