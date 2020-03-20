<!-- docs/samplecode/iwslogin.md -->
# Sample code for centralizeing login block

## Purpose
As we need to pass our login information to every TX-TANGO SOAP web serice call, it is good practice to centralize this logic.

## Example code
```csharp
    private IWS.Login IWSLogin()
    {
        //create a login block and return it
        IWS.Login login_Block = new IWS.Login()
        {
            Dispatcher = Properties.Settings.Default.Dispatcher,
            Password = Properties.Settings.Default.Password,
            Language = "EN",
            Integrator = Properties.Settings.Default.DispatcherIntegrator,
            SystemNr = Convert.ToInt32(Properties.Settings.Default.CustomerId)
        };

        return login_Block;
    }
```