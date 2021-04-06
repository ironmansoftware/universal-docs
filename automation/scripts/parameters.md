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

#### String

You can define string parameters by specifying the `[String]` type of by not specifying a type at all. Strings will generate a textbox.

```text
param(
    [String]$Textbox,
    $Textbox2
)
```

![](../../.gitbook/assets/image%20%28189%29.png)

#### String Arrays

You can specify string arrays by using the `[String[]]` type specifier. String arrays will generate a multi-tag select box.

```text
param([String[]]$Array)
```

![](../../.gitbook/assets/image%20%28190%29.png)

#### Date and Time

You can use the `[DateTime]` type specifier to create a date and time selector.

```text
param([DateTime]$DateTime)
```

![](../../.gitbook/assets/image%20%28193%29.png)

#### Boolean

You can use a `[Bool]` type selector to create a switch.

```text
param([Bool]$Switch)
```

![](../../.gitbook/assets/image%20%28186%29.png)

#### Integer

You can define a number selector by using the `[Int]` type specifier.

```text
param([Int]$Number)
```

![](../../.gitbook/assets/image%20%28194%29.png)

#### Switch Parameter

You can define a switch parameter using the `[Switch]` type specifier to create a switch.

```text
param([Switch]$Switch)
```

![](../../.gitbook/assets/image%20%28187%29.png)

#### Enumerations

You can use System.Enum values to create select boxes. For example, you could use the `System.DayOrWeek` to create a day of the week selection box.

```text
param([System.DayOfWeek]$DayOfWeek)
```

![](../../.gitbook/assets/image%20%28192%29.png)

### Help Messages

You can define help messages for your parameters by using the `HelpMessage` property of the `Parameter` attribute.

```text
param(
    [Parameter(HelpMessage = "Class you want to enroll in")]
    [string]$Class
)
```

![](../../.gitbook/assets/image%20%28185%29.png)

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

