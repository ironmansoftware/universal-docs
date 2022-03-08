---
description: Table component for PowerShell Universal pages.
---

# Table

Tables allow you to display the output of APIs and scripts in rows and columns. Each object returned by the data source will create a row within the table. You can customize the columns of the table.&#x20;

## Selecting a Data Source

Both APIs and Scripts are supported by tables. When selecting an API, the API will be executed each time the page is loaded. When selecting a script, the last job run of the script will provide the output.&#x20;

![](<../../.gitbook/assets/image (308).png>)

When columns are not defined, all the properties of the objects will be displayed.&#x20;

![](<../../.gitbook/assets/image (320).png>)

## Customizing Columns

You can customize the columns that are selected when displaying data.&#x20;

### Basic

Basic columns will select the properties defined and display the text.&#x20;

In this example, we are selecting the name and service type from a call to `Get-Service`.

![](<../../.gitbook/assets/image (385).png>)

The resulting table only has these two properties displayed.&#x20;

![](<../../.gitbook/assets/image (420).png>)

### Buttons

Buttons can be added to columns to provide functionality for each row. Clicking the button will provide the target with the row data via the `$InputObject` parameter.&#x20;

![](<../../.gitbook/assets/image (379).png>)





