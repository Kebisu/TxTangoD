<!-- docs/op/resultobject.md -->
# Result object

> Every response is derived from the result object. This provides a generic way to check on errors and warnings

## Response
- result: _ExecutionResult_
	- Errors: _array of Error_
		-  ErrorCode: _string_
		-  ErrorExplanation: _string_
		-  Field: _string_
		-  Value: _string_
	-  Warnings: _array of Warning_
		-  WarningCode: _string_
		-  WarningExplanation: _string_
		-  Field: _string_
		-  Value: _string_

## Example code
See [IsValidResult()](/samplecode/isvalidresult)

## Example xml
**Response**
```XML
<Errors>
   <Error>
      <ErrorCode>ERROR_UNAUTHORIZED</ErrorCode>
      <ErrorCodeExplanation>Unauthorized access</ErrorCodeExplanation>
      <Field>Login.Dispatcher</Field>
      <Value>INTERFACE</Value>
   </Error>
</Errors>


<Warnings>
  <Warning>
    <WarningCode>WARNING_NOT_IMPLEMENTED</WarningCode>
    <WarningCodeExplenation>This feature is not yet implemented.</WarningCodeExplenation>
    <Field>VehicleSelection.IncludeLastAlarmMessage, VehicleSelection.IncludeBlockedVehicleInfo</Field>
    <Value>False</Value>
  </Warning>
</Warnings>
```