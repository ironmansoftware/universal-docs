---
description: Parameters for PowerShell Universal jobs.
---

# Parameters

## Parameters

Jobs support automatically generating forms with parameters based on your script's `param` block. The type of control will change based on the type you define in the block. Parameters that are mandatory will also be required by the UI.

### Basic Parameters

Parameters can be simply defined without any type of parameter attribute and they will show up as text boxes in the UI.

```powershell
param($Test)

$Test
```

![](<../../.gitbook/assets/image (82).png>)

### Type Parameters

UA supports various types of parameters. You can use String, String\[], Int, DateTime, Boolean, Switch and Enum types.

#### String

You can define string parameters by specifying the `[String]` type of by not specifying a type at all. Strings will generate a textbox.

```powershell
param(
    [String]$Textbox,
    $Textbox2
)
```

![](<../../.gitbook/assets/image (180).png>)

#### String Arrays

You can specify string arrays by using the `[String[]]` type specifier. String arrays will generate a multi-tag select box.

```powershell
param([String[]]$Array)
```

![](<../../.gitbook/assets/image (181).png>)

#### Date and Time

You can use the `[DateTime]` type specifier to create a date and time selector.

```powershell
param([DateTime]$DateTime)
```

![](<../../.gitbook/assets/image (182).png>)

#### Boolean

You can use a `[Bool]` type selector to create a switch.

```powershell
param([Bool]$Switch)
```

![](<../../.gitbook/assets/image (183).png>)

#### Integer

You can define a number selector by using the `[Int]` type specifier.

```powershell
param([Int]$Number)
```

![](<../../.gitbook/assets/image (187).png>)

#### Switch Parameter

You can define a switch parameter using the `[Switch]` type specifier to create a switch.

```powershell
param([Switch]$Switch)
```

![](<../../.gitbook/assets/image (184).png>)

#### Enumerations

You can use System.Enum values to create select boxes. For example, you could use the `System.DayOrWeek` to create a day of the week selection box.

```powershell
param([System.DayOfWeek]$DayOfWeek)
```

![](<../../.gitbook/assets/image (185).png>)

#### PSCredential

When you specify a `PSCredential` , the user will be presented with a drop down of credentials available as [variables](../../platform/variables.md#creating-a-secret-variable).&#x20;

```powershell
param(
    [PSCredential]$Credential
)
```

![](<../../.gitbook/assets/image (331).png>)

### Display Name

You can use the `DisplayNameAtrribute` to set a display name for the script parameter.&#x20;

```powershell
param(
    [ComponentModel.DisplayName("My Script")]
    $MyScript
)
```

![](<../../.gitbook/assets/image (367).png>)

### Help Messages

You can define help messages for your parameters by using the `HelpMessage` property of the `Parameter` attribute.

```powershell
param(
    [Parameter(HelpMessage = "Class you want to enroll in")]
    [string]$Class
)
```

![](<../../.gitbook/assets/image (186).png>)

### Required Parameters

You can use the Parameter attribute to define required parameters.

```powershell
param(
    [Parameter(Mandatory)]
    $RequiredParameter
)

$RequiredParameter
```

![](<../../.gitbook/assets/image (84).png>)

## Passing Parameters from PowerShell

You can pass parameters from PowerShell using the `Invoke-UAJob` cmdlet. This cmdlet supports dynamic parameters. If you have a `param` block on your script, these parameters will automatically be added to `Invoke-UAJob`.

For example, I had a script named Script1.ps1 and the contents were are follows.

```powershell
param($MyParameter)

$MyParameter
```

I could then invoke that script using this syntax.

```powershell
Invoke-PSUScript -Name 'Script.ps1' -MyParameter "Hello"
```

The result would be that Hello was output in the job log and pipeline.

## Parameter Sets

PowerShell Universal supports parameter sets. When a parameter set is defined, a drop down is provided that allows for switching between the sets.&#x20;

```powershell
param(
    [Parameter(ParameterSetName = 'Set1')]
    $Parameter1,
    [Parameter(ParameterSetName = 'Set2')]
    $Parameter2
)
```

![Parameter Sets](<../../.gitbook/assets/image (415).png>)
