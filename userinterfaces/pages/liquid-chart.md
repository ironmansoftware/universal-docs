---
description: Liquid charts show a percentage value as returned by an API or script.
---

# Liquid Chart

## Display a chart from an API

An API that provides data to a chart needs to return a single number between 0.0 and 1.00. 

This example returns a random percentage. 

```text
(1..100 | Get-Random) / 100
```

Select an API from the list of available APIs. 

![](../../.gitbook/assets/image%20%28262%29.png)

The liquid chart will display the value. 

![](../../.gitbook/assets/image%20%28259%29.png)

## Display a chart from a Script

You can display a liquid chart with data from a script. You should return a single value between 0.0 and 1.00. 

This script we are executing in this example returns a random percentage. 

```text
(1..100 | Get-Random) / 100
```

Select the script as the data source. 

![](../../.gitbook/assets/image%20%28264%29.png)

The chart will display based on the data returned. 

![](../../.gitbook/assets/image%20%28259%29.png)

## Properties

| Properties | Description | Available Since |
| :--- | :--- | :--- |
| Id | The ID of this component | 2.2.0 |
| Data Source Type | The data source type for this chart. Accepts scripts or APIs. | 2.2.0 |
| Data Source | The data source for this chart. | 2.2.0 |
| Color | The color of the chart. | 2.2.0 |

