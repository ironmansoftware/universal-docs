---
description: Documentation on how to customize the login page.
---

# Login Page

{% hint style="info" %}
Login page customization requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

The login page colors, image, copyright and title can be customized by editing the `.universal/loginPage.ps1` file.

## Customizing the login page

You can host an image by using [Published Folders](../platform/published-folders.md). In this example, we have a `dbatools.png` file in our local folder.

![DBATools Logo](<../.gitbook/assets/image (401).png>)

Next, we can create a `loginPage.ps1` file in the repository folder. Add the various colors, text and image URL to customize the login page. As soon as you save this file, you can refresh the login page to see the result.

```powershell
$LoginPage = @{
 PrimaryColor = '#5c2751' 
 Title = 'DBATools Web Portal'
 Copyright = 'DBATools 2020' 
 HeaderFontColor = 'white'
 HeaderColor = '#4bc0d9' 
 SecondaryColor = '#6457a6'
 SecondaryFontColor = 'white'
 Image = 'http://localhost:5000/images/dbatools.png'
 Links = @(
    New-PSULoginPageLink -Text 'Google' -Url 'http://www.google.com'
    New-PSULoginPageLink -Text 'Microsoft' -Url 'http://www.microsoft.com'
 )
}

New-PSULoginPage @LoginPage
```

This login page looks like this.

![](<../.gitbook/assets/image (71).png>)

## Customizing the login page in the Admin Console

{% hint style="warning" %}
This feature will be available in PowerShell Universal 2.3.
{% endhint %}

In addition to being able to customize the login page via PowerShell, you can also do so in the admin console. Click Settings \ Login page to adjust the settings.

![](<../.gitbook/assets/image (515).png>)

## Customizing the login page with an App

You can override the login page with an app by setting an app's base URL to `/login`. You need to ensure that the app does not require authentication.

```powershell
New-PSUApp -Name 'App' -Path 'app.ps1' -BaseUrl '/login'
```

You will then need to implement the login features manually.

### Implementing an app-based login page

This is an example of implementing an app-based login page using email addresses and passcodes. The user would enter their email address, the app would send a passcode to the account and cache it locally. Once the user redirects back to the app, they will be logged in.

The app used for login has two different modes. The first is when no query string parameters are specified. The second is when the user is redirected back to the app with the passcode.

```powershell
New-UDApp -Content {
    if ($Query["passcode"]) {
        New-UDDynamic -Content {
            $JavaScript = "fetch('http://localhost:5000/api/v1/signin', {
            method: 'POST',
            body: JSON.stringify({
                username: '$($Query['email'])',
                password: '$($Query['passcode'])'
            }),
            credentials: 'include',
            headers: {
                'Content-type': 'application/json; charset=UTF-8'
            }
        })
        .then((response) => response.json()).
        then(() => {
            window.location.href = 'http://localhost:5000/app2'
        });"
            Invoke-UDJavaScript -JavaScript $JavaScript
        }
    }
    else {
        New-UDForm -Content {
            New-UDTextbox -Placeholder "Email" -Id 'email' -Type email
        } -OnSubmit {
            $Password = (New-Guid).ToString()
            # Send Email Here with a link like: http://localhost:5000/app?email=email&passcode=$Password

            # For Testing 
            Set-UDClipboard -Data "http://localhost:5000/app/Home?email=$($EventData.email)&passcode=$Password" -ToastOnSuccess

            # Set cache with email + passcode. User has 5 minutes to click link in email before it expires
            Set-PSUCache -Key $EventData.email -Value $Password -AbsoluteExpirationFromNow ([TimeSpan]::FromMinutes(5))
            New-UDAlert -Text "Please check your email!"

        } -SubmitText "Send Login Email"
    }
}
```

The resulting app will look like this when loaded.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

After submitting the form, the following will be shown. Additionally, the passcode is cached into the server cache with `Set-PSUCache`.

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

A URL will be generated and, in this example, copied to the clipboard.

Within the admin console, navigate to the forms authentication method and add the following logic. This logic checks the cache to see if the passcode and email address combination is valid. When the user logs in, the JavaScript on the app will run and force a login. Once complete, the user will be redirected to another page.

```powershell
param(
        [PSCredential]$Credential
    )


    # Check the cache to see if this email + passcode combination is valid
    $Passcode = Get-PSUCache -Key $Credential.UserName
    if ($Passcode -eq $Credential.GetNetworkCredential().Password) {
        New-PSUAuthenticationResult -Claims {
            New-PSUAuthorizationClaim -Type ([System.Security.Claims.ClaimTypes]::Role) -Value 'Administrator'
        } -UserName $Credential.UserName -Success
    }

    # Do standard form login here
    New-PSUAuthenticationResult -ErrorMessage 'Bad username or password'
```

## API

* [New-PSULoginPage](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSULoginPage.txt)
* [New-PSULoginPageLink](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSULoginPageLink.txt)

###
