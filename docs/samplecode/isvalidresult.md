<!-- docs/samplecode/iwslogin.md -->
# Sample code for checking the response

## Purpose
Because every response object is derived from the same parent class, we can process this in a standard way. This allows us to capture all errors or warnings that might occur.

All responses are derived from the ExecutionResult object.
The ExecutionResult contains a list of errors, a list of warnings and the execution time (the time it took for our servers to process the request)

## Example code
```csharp

    private bool IsValidResult(IWS.ExecutionResult response)
    {
        bool isValid = true;
        //check if there are errors
        if (response.Errors.Length > 0)
        {
            //if one or more errors then set the result to false
            isValid = false;
            //loop over all the errors and log them
            foreach (IWS.Error err in response.Errors)
            {
                Log(err.ErrorCode + ": " + err.ErrorCodeExplanation + " (" + err.Field + " - " + err.Value + ")", true);
            }
        }
        return isValid;
    }
    
```