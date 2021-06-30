---
description: PowerShell Universal Templates
---

# Templates



{% hint style="warning" %}
This documentation is for a future version of PSU. 
{% endhint %}

PowerShell Universal templates allow you to share your configurations with other users internally or with the PSU community. Configuration import and export functionality is built directly into PSU. You will need at least version 2.1.0 to use this functionality. 

## Exporting a Template

To export a template, you can navigate to Settings \ Configurations and click Export Configuration as Template. 

![](../.gitbook/assets/image%20%28229%29.png)

Once you click the button, you will be prompted for a name, description, author and version for the template. 

![](../.gitbook/assets/image%20%28227%29.png)

When you export a configuration, any variables that you have defined will not be included. The user that imports the template will need to define the variables. 

If you have a license defined, it will not be included but the user of the template will be notified that the template requires a license. 

## Importing a Template

To import a configuration navigate to Settings \ Configuration and click Import Template. Navigate to the local `psupkg` file. Template information will be presented before importing the template.

![](../.gitbook/assets/image%20%28228%29.png)

## Publishing a Template

You can publish a template to the Ironman Software website after logging into your account. Click PowerShell Universal \ Templates and then the Upload Template button. Upload your `psupkg` file. Metadata will be read from the template file. After uploading the file, you'll be able to add some screenshots. 



