# Security

## Forms Authentication

By default, the forms authentication script is configured to accept the user Admin and any password. You can configure this authentication policy to interact with whatever system you like. The script will receive a `PSCredential` object that contains the user name and password entered by the user at the login page. 

## Authorization 

User authorization can be achieved in two different ways: Role Assignment or Policy Assignment. 

### Policy Assignment

By default, roles are assigned by policies. Policies are run when the user logs in. You can change the policy scripts by visiting the Security / Roles tab. Click the Edit Policy button to configure the Policy script. 

![](../.gitbook/assets/image%20%285%29.png)

Policy scripts will receive a `ClaimsPrincipal` object as a parameter and need to return true or false. Policies that throw errors will be assumed to be false. The `ClaimsPrincipal` object contains the user's identity and the claims that the user has received. These may include group assignments or other features of a user's account. 

You can expect an object with this structure. 

```text
public class ClaimsPrincipal
{
    public List<Claim> Claims { get; set; } = new List<Claim>();
    public Identity Identity { get; set; } = new Identity();
}

public class Identity 
{
    public string Name { get ;set; }
}

public class Claim 
{
    public string Type { get; set; }  
    public string Value { get; set; }
    public string ValueType { get; set; } 
    public string Issuer { get; set; }
    public Dictionary<string, string> Properties { get; set; } = new Dictionary<string, string>();
}
```

### Role Assignment 

To assign a role to a user, you can create their identity within Universal and then select the role in the drop down on the Identities page. By default, identities receive a role through policy. 

![](../.gitbook/assets/image%20%2811%29.png)

## App Tokens

App Tokens can be assigned to services that cannot login interactively. You can grant a new app token to your account by clicking the Grant App Token button within the Security / App Tokens tab. 

The token will have a expiration of one year and have the valid roles for your account. To copy the App Token to your account, click the Copy action. To revoke an App Token, click the Revoke action. 

You can use App Tokens with the Universal cmdlets or by using web requests directly using Bearer authorization. 

![](../.gitbook/assets/image%20%283%29.png)

