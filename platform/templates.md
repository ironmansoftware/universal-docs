---
description: PowerShell Universal Templates
---

# Templates

PowerShell Universal templates allow you to share your configurations with other users internally or with the PSU community. Configuration import and export functionality is built directly into PSU. You will need at least version 2.1.0 to use this functionality.&#x20;

## Exporting a Template

To export a template, you can navigate to Settings \ Configurations and click Export Configuration as Template.&#x20;

![](<../.gitbook/assets/image (229).png>)

Once you click the button, you will be prompted for a name, description, author and version for the template.&#x20;

![](<../.gitbook/assets/image (227).png>)

When you export a configuration, any variables that you have defined will not be included. The user that imports the template will need to define the variables.&#x20;

If you have a license defined, it will not be included but the user of the template will be notified that the template requires a license.&#x20;

### Including a README.md

If you want to provide additional information about your template in the for of a README.md file, you can create one in the repository before exporting it. The template library on IronmanSoftware.com will render the README.md and display it for your template.&#x20;

See the [Docker Dashboard](https://ironmansoftware.com/powershell-universal/templates/template/Docker%20Dashboard/1.0.0) for an example.&#x20;

## Importing a Template

To import a configuration navigate to Settings \ Configuration and click Import Template. Navigate to the local `psupkg` file. Template information will be presented before importing the template.

![](<../.gitbook/assets/image (228).png>)

## Publishing a Template

You can publish a template to the Ironman Software website after logging into your account. Click PowerShell Universal \ Templates and then the Upload Template button. Upload your `psupkg` file. Metadata will be read from the template file. After uploading the file, you'll be able to add some screenshots.&#x20;

