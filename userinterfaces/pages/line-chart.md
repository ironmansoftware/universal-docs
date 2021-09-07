---
description: A line chart that can display output from scripts and APIs.
---

# Line Chart

## About <a id="about"></a>

Line charts can retrieve output from scripts and APIs to display the data in a chart.‌

### Display Data from an API <a id="display-data-from-an-api"></a>

You will need to return an array of JSON objects from your API in order to use a bar chart. An example would be returning a list of hashtables serialized to JSON.

```text
@(
    @{
        Name = "Name1"
        Value = Get-Random
    }
    @{
        Name = "Name2"
        Value = Get-Random
    }
    @{
        Name = "Name3"
        Value = Get-Random
    }
) | ConvertTo-Json
```

In this example, you would configure the data source to an API and select your API endpoint. 

![](../../.gitbook/assets/image%20%28255%29.png)

You would then specify Name as the X axis and Value as the Y axis.​​

![](../../.gitbook/assets/image%20%28261%29.png)

The resulting chart contains the data from the API. Each time the page is loaded, the API is called.​

![](../../.gitbook/assets/image%20%28266%29.png)

### Display Data from a Script <a id="display-data-from-an-api-1"></a>

You will need to return PSCustomObjects, objects or hashtables from your script in order to display a chart from a script.

```text

@(
    @{
        Name = "Name1"
        Value = Get-Random
    }
    @{
        Name = "Name2"
        Value = Get-Random
    }
    @{
        Name = "Name3"
        Value = Get-Random
    }
) 
```

You will need to set the data source to script and select the script you want to retrieve data for.​

![](../../.gitbook/assets/image%20%28263%29.png)

You will need to set the Y and X axis to the properties of the object returned from the script.​‌

The chart will appear on the page like this. Loading the page will not call the script again. It will load the result of the last time the script ran.​

![](../../.gitbook/assets/image%20%28266%29.png)

‌

## Properties <a id="properties"></a>

| Property | Description | Available Since |
| :--- | :--- | :--- |
| Id | The ID of this component | 2.2.0 |
| X Axis Field | The field to use as the X Axis for data within the chart. | 2.2.0 |
| Y Axis Field | The field to use as the Y Axis for data within the chart. | 2.2.0 |
| Data Source Type | Whether to use a script or API as a data source. | 2.2.0 |
| Data Source | The script or API to use as data for the chart. | 2.2.0 |
| Color | The bar color to use for the chart. | 2.2.0 |

