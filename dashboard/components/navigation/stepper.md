---
description: Stepper component for Universal Dashboard
---

# Stepper

**Steppers convey progress through numbered steps. It provides a wizard-like workflow.**

Steppers display progress through a sequence of logical and numbered steps. They may also be used for navigation. Steppers may display a transient feedback message after a step is saved.

## Stepper

![](../../../.gitbook/assets/image%20%2861%29.png)

```text
New-UDStepper -Steps {
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 1" }
        New-UDTextbox -Id 'txtStep1' 
    } -Label "Step 1"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 2" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep2' 
    } -Label "Step 2"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 3" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep3' 
    } -Label "Step 3"
} -OnFinish {
    New-UDTypography -Text 'Nice! You did it!' -Variant h3
    New-UDElement -Tag 'div' -Id 'result' -Content {$Body}
}
```



\*\*\*\*

**New-UDStepper**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| ActiveStep | Int32 | Sets the active step. This should be the index of the step. | false |
| Children | ScriptBlock | The steps for this stepper. Use New-UDStep to create new steps. | true |
| NonLinear | SwitchParameter | Allows the user to progress to steps out of order. | false |
| AlternativeLabel | SwitchParameter | Places the step label under the step number. | false |
| OnFinish | Endpoint | A script block that is executed when the stepper is finished. | true |



**New-UDStep**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| OnLoad | Endpoint | The script block that is executed when the step is loaded. The script block will receive the $Body parameter which contains JSON for the current state of the stepper. If you are using form controls, their data will be availalble in the $Body.Context property. | true |
| Label | String | A label for this step. | false |
| Optional | SwitchParameter | Whether this step is optional. | false |

