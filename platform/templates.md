---
description: PowerShell Universal Templates
---

# Templates

PowerShell Universal templates allow you to share your configurations with other users internally or with the PSU community. Configuration import and export functionality is built directly into PSU. You will need at least version 2.1.0 to use this functionality.&#x20;

## Exporting a Template

To export a template, you can navigate to Platform \ Templates and click Export Configuration as Template.&#x20;

![Templates](<../.gitbook/assets/image (316).png>)

Once you click the button, you will be prompted for a name, description, author and version for the template. The Readme value can contain markdown and is rendered on IronmanSoftware.com.

![](<../.gitbook/assets/image (314).png>)

When you export a configuration, any variables that you have defined will not be included. The user that imports the template will need to define the variables.&#x20;

If you have a license defined, it will not be included.

## Importing a Template

To import a configuration, navigate to Platform \ Templates and click the template to Import.&#x20;

![Templates](<../.gitbook/assets/image (315).png>)

You will be prompted to before applying the template.

![Import Template](<../.gitbook/assets/image (298).png>)

## Import a PSUPKG

Templates are stored as `psupkg` files. To import a template from a file, click Platform \ Templates and then Import Template. Navigate to the local `psupkg` file. Template information will be presented before importing the template.

## Publishing a Template

You can publish a template to the Ironman Software website after logging into your account. Click PowerShell Universal \ Templates and then the Upload Template button. Upload your `psupkg` file. Metadata will be read from the template file. After uploading the file, you'll be able to add some screenshots.&#x20;

