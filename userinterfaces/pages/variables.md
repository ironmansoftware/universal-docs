---
description: Variables available in PowerShell Universal pages.
---

# Variables

{% hint style="info" %}
This feature requires a [PowerShell Universal license](../../licensing.md).&#x20;
{% endhint %}

Variables allow you modify the functionality of a page depending on factors such as the user name or URL route. Variable-based routes allow you to create dynamic pages based on the URL the user is visiting.&#x20;

Variables that are defined with Platform \ Variables will also be available to pages.

## Viewing Variables

Variables can be viewed when editing a page. To view variables, click Edit and then Variables.&#x20;

![](<../../.gitbook/assets/image (298) (1) (1) (1) (1) (1) (1).png>)

A drawer will appear with the variables for the current page.&#x20;

![](<../../.gitbook/assets/image (301) (1) (1) (1) (1).png>)

## Using Variables

Variables can be used anywhere you can type a property value. For example, if you have an Alert, you could use the `$pagename` variable within the title property.&#x20;

![](<../../.gitbook/assets/image (293) (1) (1) (1).png>)

When the page is rendered, the variable will be replaced.&#x20;

![](<../../.gitbook/assets/image (299) (1) (1) (1) (1) (1).png>)



You can also use variables within targets and data sources. This allows you to call URLs that will change based on the variable.&#x20;

![](<../../.gitbook/assets/image (295) (1) (1) (1).png>)

You can also use variables to provide hidden input fields to APIs and scripts.&#x20;

&#x20;

![](<../../.gitbook/assets/image (296) (1) (1) (1) (1).png>)

## Page Variables

You can load additional data when the page is loading by providing a data source to in the page properties. The data source should return a single PSCustomObject or hashtable. The properties of the object will become variables within the page.&#x20;

For example, assume you have an API that returns the following hashtable.&#x20;

```
@{
    Name = "My Name"
    Title = "My Title"
}
```

Selecting this API as the data source for the page would then create the variables `$Name` and `$Title` within the page.&#x20;

You can also use Route Variables within the data source to customize which API is called based on the route visited.&#x20;

## Route Variables

Route variables need to be defined when creating the URL for the page. Each section of the URL that starts with `:` will be treated as a variable.&#x20;

For example, this page defines a single route variable.&#x20;

![](<../../.gitbook/assets/image (294) (1) (1).png>)

Within the page, the route variables will appear within the variable drawer.&#x20;

![](<../../.gitbook/assets/image (300) (1) (1) (1) (1) (1) (1) (1).png>)

