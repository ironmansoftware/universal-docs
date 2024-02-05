---
description: Slider component for Universal Apps.
---

# Slider

Sliders allow users to make selections from a range of values.

Sliders reflect a range of values along a bar, from which users may select a single value. They are ideal for adjusting settings such as volume, brightness, or applying image filters.

## Slider

![](<../../../.gitbook/assets/image (379).png>)

```powershell
New-UDSlider -Value 1
```

## Slider with minimum and maximum values

![](<../../../.gitbook/assets/image (487).png>)

```powershell
New-UDSlider -Min 10 -Max 1000
```

## Disabled Slider

![](<../../../.gitbook/assets/image (197).png>)

```powershell
New-UDSlider -Disabled
```

## Slider with custom step size

![](<../../../.gitbook/assets/image (508).png>)

```powershell
New-UDSlider -Min 10 -Max 1000 -Step 100
```

## Slider with marks

![](<../../../.gitbook/assets/image (388).png>)

```powershell
New-UDSlider -Marks
```

## Range based slider

![](<../../../.gitbook/assets/image (381).png>)

```powershell
New-UDSlider -Value @(1, 10)
```

## OnChange event for slider

```powershell
New-UDSlider -OnChange {
    Show-UDToast -Message $Body 
    Set-TestData $Body
}
```

## API

* [New-UDSlider](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDSlider.txt)

