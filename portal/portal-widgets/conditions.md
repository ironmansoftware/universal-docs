---
description: Conditions within portal widgets.
---

# Conditions

You can use the `<Condition />` component within widgets to optionally display sections of the widget.

## Script Block

Using the `ScriptBlock` attribute to define a Script Block to determine the value of the condition. The script block needs to return true or false.&#x20;

```xml
<Condition ScriptBlock="$Errors -eq $null">
</Condition>
```

## Child Content

The `ChildContent` section will be displayed if the condition is true.&#x20;

```markup
<Condition ScriptBlock="$Errors -eq $null">
   <ChildContent>
      <Alert Message="Success!" />
   </ChildContent>
</Condition>
```

## Else

The `Else` section will be displayed if the condition is false.&#x20;

```markup
<Condition ScriptBlock="$Errors -eq $null">
   <ChildContent>
      <Alert Message="Success!" />
   </ChildContent>
   <Else>
      <Alert Message="Failure!" Type="error" ShowIcon="true" />
   </Else>
</Condition>
```
