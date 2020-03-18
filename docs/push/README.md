<!-- docs/op/push/README.md -->
# PUSH Technology

> We are adding the option to get data pushed to your server.
> Data that can currently be pushed: Alarms
> The only push technology that we are currently supporting is WebAPI.

## Technology
### WebAPI
- A WebAPI, means that we push data via a HTTP POST to an endpoint at your side or in the cloud.
- The data is a JSON message in the body of the POST

### Subscriptions
- In order to receive the data on your endpoint you need to subscribe and provide us the URL.
- The subscription consists of two parts: The feature and the technology.
**Feature**
- With the feature you choose the data and the filter on that data
- Currently the only feature is _NewAlarm_ and you can filter on the type of alarms.
**Technology**
- The technology is how and where we need to push data
- Currently the only technology we support is WebAPI and the detail we need is the URL
- Details are sent as JSON in the subscription web service
	```json
		{
			"URL": "https://ar.azure-api.net/tran......"
		}
	```
**TX-TANGO**
- The subscriptions are managed via TX-TANGO: Add_Subscriptions, Update_PushSubscriptionsStatus, Get_Subscriptions
- See each TX-TANGO web service for more details

## Data
### Alarms
- Feature name: _NewAlarm_
- Feature parameters is a json with the following structure
	- Array of AlarmTypes: 'Geofencing','ActivityTakesTooLong','DeadlineReadConfirmation','PlanningActivityTakesTooLong','ExternalDevice','CorridorAlarm','LowBattery','Pto','SpeedThresHold','RpmThresHold','EndQuestionPathNotCompletedAlarm','NextStop','Sos','DrivingTimes','Temperature','FuelDecreaseAlarm','HarshBrakeAlarm','DrivingWithoutIsoCableAlarm','RollOverStabilitySupportAlarm','EbsStateAlarm','TyrePressureAlarm','DoorlockAlarm','SensorAlarm','DynamicAlarm','RemoteDiagnosticsAlarm','NoCommunicationAlarm','UnknownDriverForObc','HarshAccelerationAlarm','MaxIdlingAlarm','FuelIncreaseAlarm','SufficientBrakeLiningAlarm','AntiLockBrakingSystemAlarm'
	- AlarmPOIEnrichment flag: 0 or 1, to indicate if the POI has to be resolved and added to the pushed message. We suggest to keep this a 0.
- Feature parameters are sent as JSON in the subscription web service
	```json
		{
		'AlarmTypes': ['Geofencing', 'ActivityTakesTooLong'],
		'AlarmPOIEnrichmentRequired': 1
		}
	```
**Example of a pushed alarm message**
```json
{
    "alarmId": 12647781,
    "alarmType": "Geofencing",
    "alarmSubType": "EnterGeoZoneAlarm",
    "alarmText": "GeoFencing alert - Entered in testPUSH - DEMOA4 (DEMO ROMANIA).",
    "truckId": 53926,
    "driverId": 144673,
    "trailerId": -1,
    "timeStamp": "2020-03-18T16:20:22Z",
    "position": {
        "latitude": 46.7992,
        "longitude": 23.74,
        "address": ""
    },
    "origin": {
        "rel": "Geozone",
        "id": 9544,
        "href": ""
    },
    "updateDate": "2020-03-18T16:20:22.1386076Z"
}
```

## Test & Valdate
- Checking what the messages look like without setting up a server can be done easily via https://webhook.site or https://requestbin.com
- These sites generate an endpoint that you can use in the subscription web service
- If something is pushed it will be visualized in the browser and you can inspect the message.
