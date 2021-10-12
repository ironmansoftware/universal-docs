---
description: Table component for PowerShell Universal pages.
---

# Table

Tables allow you to display the output of APIs and scripts in rows and columns. Each object returned by the data source will create a row within the table. You can customize the columns of the table. 

## Selecting a Data Source

Both APIs and Scripts are supported by tables. When selecting an API, the API will be executed each time the page is loaded. When selecting a script, the last job run of the script will provide the output. 

![](<../../.gitbook/assets/image (295).png>)

When columns are not defined, all the properties of the objects will be displayed. 

![](<../../.gitbook/assets/image (296).png>)

## Customizing Columns

You can customize the columns that are selected when displaying data. 

### Basic

Basic columns will select the properties defined and display the text. 

In this example, we are selecting the name and service type from a call to `Get-Service`.

![](<../../.gitbook/assets/image (301).png>)

The resulting table only has these two properties displayed. 

![](<../../.gitbook/assets/image (302).png>)

### Buttons

Buttons can be added to columns to provide functionality for each row. Clicking the button will provide the target with the row data via the `$InputObject` parameter. 

![](<../../.gitbook/assets/image (300).png>)





