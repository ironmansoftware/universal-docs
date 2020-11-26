---
description: Documentation on how to customize the login page.
---

# Login Page

{% hint style="info" %}
This feature requires any type of [PowerShell Universal license](../get-started/licensing.md). 
{% endhint %}

The login page colors, image, copyright and title can be customized by editing the `.universal/loginPage.ps1` file. 

## Customizing the login page

You can host an image by using [Published Folders](../dashboard/published-folders.md). In this example, we have a `dbatools.png` file in our local folder.

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
}

New-PSULoginPage @LoginPage
```

This login page looks like this. 

![DBATools Web Portal Example](../.gitbook/assets/image%20%28170%29.png)

