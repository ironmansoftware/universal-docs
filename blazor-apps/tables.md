---
description: Blazor app Tables
---

# Tables

Tables can be used to display data to users in a grid format.&#x20;

## Basic Table

Tables consist of a data source and a series of columns. You can use PowerShell variables are a data source. A simple script could load all the services on the machine into a variable.&#x20;

```powershell
$Variables["Services"] = Get-Service
```

The table would then display a set number of properties as columns.&#x20;

```markup
<Table DataSource="$Services">
    <PropertyColumn Property="Name"></PropertyColumn>
    <PropertyColumn Property="Status"></PropertyColumn>
</Table>
```

## Column Content

Property columns can provide custom content based on the row being rendered. Use the `$Context` variable to reference the current row.&#x20;

```markup
<Table DataSource="$Services">
    <PropertyColumn Property="Name"></PropertyColumn>
    <PropertyColumn Property="Status">
        <Alert Message="$context.Status" />
    </PropertyColumn>
</Table>
```

## Action Columns

Actions columns are not tied to a particular property and are used for display actions such as buttons.&#x20;

```markup
<Table DataSource="$Services">
    <PropertyColumn Property="Name"></PropertyColumn>
    <PropertyColumn Property="Status">
        <Alert Message="$context.Status" />
    </PropertyColumn>
    <ActionColumn>
        <Button OnClick="ShowStatus">Show Status</Button>
    </ActionColumn>
</Table>
```

To reference the current row in the button click, use the `$Context` parameter.&#x20;

```powershell
function ShowStatus {
    param($Context)
    $MessageService.Success($Context.Status.ToString())
}
```
