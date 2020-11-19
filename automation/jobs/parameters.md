---
description: Parameters for PowerShell Universal jobs.
---

# Parameters

## Parameters

Jobs support automatically generating forms with parameters based on your script's `param` block. The type of control will change based on the type you define in the block. Parameters that are mandatory will also be required by the UI. 

### Basic Parameters

Parameters can be simply defined without any type of parameter attribute and they will show up as text boxes in the UI. 

```text
param($Test)

$Test
```

![](../../.gitbook/assets/image%20%2887%29.png)

### Type Parameters

UA supports various types of parameters. You can use String, String\[\], Int, DateTime, Boolean, Switch and Enum types. 

```text
param(
    [String]$Textbox,
    [Int]$NumberPicker,
    [DateTime]$DateTime,
    [Bool]$Switch,
    [Switch]$Switch2,
    [System.DayOfWeek]$Select
)

$Textbox
$NumberPicker
$DateTime
$Switch
$Switch2
$Select
```

![](../../.gitbook/assets/image%20%2888%29.png)

### Required Parameters

You can use the Parameter attribute to define required parameters. 

```text
param(
    [Parameter(Mandatory)]
    $RequiredParameter
)

$RequiredParameter
```

![](../../.gitbook/assets/image%20%2886%29.png)

## Passing Parameters from PowerShell

You can pass parameters from PowerShell using the `Invoke-UAJob` cmdlet. This cmdlet supports dynamic parameters. If you have a `param` block on your script, these parameters will automatically be added to `Invoke-UAJob`. 

For example, I had a script named Script1.ps1 and the contents were are follows. 

```text
param($MyParameter)

$MyParameter
```

I could then invoke that script using this syntax. 

```text
Invoke-UAScript -Name 'Script.ps1' -MyParameter "Hello"
```

The result would be that Hello was output in the job log and pipeline. 

