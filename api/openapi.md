---
description: Standardized documentation for your endpoints.
---

# OpenAPI

## About

API documentation can be produced for your endpoints by creating a new OpenAPI definition and assigning endpoints to it. OpenAPI is a standard format and can be consumed by tools, such as the [OpenAPI Generator](https://openapi-generator.tech/) or [Swagger Codegen](https://swagger.io/tools/swagger-codegen/), to create clients.  The Swagger dashboard is also integrated into PowerShell Universal to provide interactive documentation.

## Management API Documentation

You can view the Managment API documentation by visiting the built in Swagger dashboard.&#x20;

```
http://localhost:5000/swagger/index.html
```

## Create an OpenAPI Document

To create an OpenAPI definition, click APIs \ Documentation and then Create new Endpoint Documentation. You can set the name, URL, description and authentication details for the documentation.

<figure><img src="../.gitbook/assets/image (233).png" alt=""><figcaption><p>Endpoint Documentation</p></figcaption></figure>

Once created, you can assign endpoints to the documentation by editing the endpoint.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption><p>Edit Endpoint</p></figcaption></figure>

The documentation for your endpoint will appear within the Swagger dashboard. Select the definition with the Select a definition dropdown.

<figure><img src="../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>

All your custom endpoints will be listed.

![Swagger Documentation for APIs](<../.gitbook/assets/image (22).png>)

## Help Text

You can specify help text for your APIs using comment-based help. Including a synopsis, description and parameter descriptions will result in each of those pieces being documented in the OpenAPI documentation and Swagger age.

For example, with a simple `/get/:id` endpoint, we could have comment-based help such as this.

```powershell
<# 
.SYNOPSIS
This is an endpoint

.DESCRIPTION
This is a description

.PARAMETER ID
This is an ID.

#>
param($ID)
    
$Id
```

The resulting Swagger page will show each of these descriptions.

## Input and Output Types

Types can be defined within an endpoint documentation ScriptBlock. Click the Edit Details button on the API documentation record.

<figure><img src="../.gitbook/assets/image (231).png" alt=""><figcaption><p>Edit Details for API Documentation</p></figcaption></figure>

APIs can also be documented using input and output types by creating a PowerShell class and referencing it within your comment-based help. PowerShell Universal takes advantage of the `.INPUTS` and `.OUTPUTS` sections to specify accepted formats and define status code return values.

Within the `.INPUTS` and `.OUTPUTS` , you will define a YAML block to provide this information. To create types, use the Endpoint Documentation editor. This file is loaded when reading OpenAPI documents. This information is stored in `endpointsDocumentation.ps1`.

```powershell
[Documentation()]
class MyReturnType {
    [string]$Value
}
```

### Inputs

Input types are defined in the `.INPUTS` section. This section is a YAML block that defines if the input is required, provides a description and specifies the content type. This is a content type followed by the PowerShell class you defined in the endpoint documentation.&#x20;

```powershell
<#
  .INPUTS
  Required: false
  Description: This is an input value.
  Content:
      application/json: MyReturnType 
#>
param()
```

### &#x20;Outputs

Output types are similar to input but are specified on return codes as well as their content type and PowerShell class. The below example returns an ADAccountType class when a HTTP OK (200) is returned from the API. A 400 (Bad Request) does not return data but does provide a description that will be displayed in the API documentation.&#x20;

```powershell
<#
.OUTPUTS
200:
  Description: This is an output value. 
  Content:
      application/json: ADAccountType

400:
  Description: Invalid input
#>
param()
```
