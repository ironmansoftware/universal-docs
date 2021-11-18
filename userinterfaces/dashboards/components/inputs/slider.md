---
description: Slider component for Universal Dashboard.
---

# Slider

Sliders allow users to make selections from a range of values.

Sliders reflect a range of values along a bar, from which users may select a single value. They are ideal for adjusting settings such as volume, brightness, or applying image filters.

## Slider

![](<../../../../.gitbook/assets/image (37).png>)

```powershell
New-UDSlider -Value 1
```

## Slider with minimum and maximum values

![](<../../../../.gitbook/assets/image (44).png>)

```powershell
New-UDSlider -Min 10 -Max 1000
```

## Disabled Slider

![](<../../../../.gitbook/assets/image (59).png>)

```powershell
New-UDSlider -Disabled
```

## Slider with custom step size

![](<../../../../.gitbook/assets/image (48).png>)

```powershell
New-UDSlider -Min 10 -Max 1000 -Step 100
```

## Slider with marks

![](<../../../../.gitbook/assets/image (39).png>)

```powershell
New-UDSlider -Marks
```

## Range based slider

![](<../../../../.gitbook/assets/image (65).png>)

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

* [New-UDSlider](../../../../cmdlets/New-UDSlider.txt)

****
