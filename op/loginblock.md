<!-- docs/op/loginblock.md -->
# Login block

> The login block is part of every web service operation and takes care of the authentication before executing the web service.

## Struture
4 mandatory fields
- Dispatcher: the username
- Password: the password of that user
- SystemNr: the id that identifies the customer
- Integrator: the partner that is executing the request

> - Dispatcher needs to have access to that customer and the dispatcher determines which trucks, drivers and trailers are returned in the response
> - The Integrator checks if this partner has access to that function 

Optional fields
- Language: the language that needs to be used to translate fields in the response
- ApplicationName: name by which we can identify what application is making the request
- ApplicationVersion: version of the application
- PcName: name of the server that is making the connection
- DateTime: not used
- Version: not used

## Example code
Because the login block logic is needed for every web service operation, it can be interesting to put this in a reusable function
```csharp
        private IWS.Login IWSLogin()
        {
            IWS.Login login_Block = new IWS.Login()
            {
                Dispatcher = varUser,
                Password = varPwd,
                Language = "EN",
                Integrator = varInt,
                SystemNr = Convert.ToInt32(varCustId)
            };

            return login_Block;

        }
``` 