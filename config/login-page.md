---
description: Documentation on how to customize the login page.
---

# Login Page

{% hint style="info" %}
This feature requires any type of [PowerShell Universal license](../get-started/licensing.md).
{% endhint %}

The login page colors, image, copyright and title can be customized by editing the `.universal/loginPage.ps1` file.

## Customizing the login page

You can host an image by using [Published Folders](../platform/published-folders.md). In this example, we have a `dbatools.png` file in our local folder.

![DBATools Logo](../.gitbook/assets/image%20%28171%29.png)

Next, we can create a `loginPage.ps1` file in the repository folder. Add the various colors, text and image URL to customize the login page. As soon as you save this file, you can refresh the login page to see the result.

```text
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

![](../.gitbook/assets/image%20%28226%29.png)

## Customizing the login page in the Admin Console

{% hint style="warning" %}
This feature will be available in PowerShell Universal 2.3. 
{% endhint %}

In addition to being able to customize the login page via PowerShell, you can also do so in the admin console. Click Settings \ Login page to adjust the settings. 

![](../.gitbook/assets/image%20%28257%29.png)

## API

### New-PSULoginPage

| Name | Description | Type | Required |
| :--- | :--- | :--- | :--- |
| Image | The URL of the image to display | string | false |
| Title | The title text to display  | string | false |
| PrimaryColor | The primary color for the login page. You can use any valid HTML color. | string | false |
| SecondaryColor | The secondary color for the login page. You can use any valid HTML color. | string | false |
| PrimaryFontColor | The primary font color for the login page.  You can use any valid HTML color. | string | false |
| SecondaryFontColor | The secondary font color for the login page.  You can use any valid HTML color. | string | false |
| HeaderColor | The header color for the login page.  You can use any valid HTML color. | string | false |
| HeaderFontColor | The header color for the login page.  You can use any valid HTML color. | string | false |
| Links | A list of links to display in the header. Use New-PSULoginPageLink to create these links. | LoginPageLink | false |
| Copyright | The copyright text to display. | string | false |

### New-PSULoginPageLink

| Name | Description | Type | Required |
| :--- | :--- | :--- | :--- |
| Text | The text of the link. | string | true |
| Url | The URL the link points to. | string | true |

