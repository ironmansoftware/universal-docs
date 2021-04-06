---
description: Slider component for Universal Dashboard.
---

# Slider

Sliders allow users to make selections from a range of values.

Sliders reflect a range of values along a bar, from which users may select a single value. They are ideal for adjusting settings such as volume, brightness, or applying image filters.

## Slider 

![](../../../.gitbook/assets/image%20%2837%29.png)

```PowerShell
New-UDSlider -Value 1
```

## Slider with minimum and maximum values

![](../../../.gitbook/assets/image%20%2844%29.png)

```PowerShell
New-UDSlider -Min 10 -Max 1000
```

## Disabled Slider

![](../../../.gitbook/assets/image%20%2859%29.png)

```PowerShell
New-UDSlider -Disabled
```

## Slider with custom step size

![](../../../.gitbook/assets/image%20%2848%29.png)

```PowerShell
New-UDSlider -Min 10 -Max 1000 -Step 100
```

## Slider with marks

![](../../../.gitbook/assets/image%20%2839%29.png)

```PowerShell
New-UDSlider -Marks
```

## Range based slider

![](../../../.gitbook/assets/image%20%2865%29.png)

```PowerShell
New-UDSlider -Value @(1, 10)
```

## OnChange event for slider

```PowerShell
New-UDSlider -OnChange {
    Show-UDToast -Message $Body 
    Set-TestData $Body
}
```



**New-UDSlider**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string |  | false |
| Value | int\[\] |  | false |
| Minimum | int |  | false |
| Maximum | int |  | false |
| Disabled | switch |  | false |
| Marks | switch |  | false |
| OnChange | Endpoint |  | false |
| Orientation | string |  | false |
| Step | int |  | false |
| ValueLabelDisplay | string |  | false |

