---
description: Slider component for Universal Dashboard.
---

# Slider

Sliders allow users to make selections from a range of values.

Sliders reflect a range of values along a bar, from which users may select a single value. They are ideal for adjusting settings such as volume, brightness, or applying image filters.

## Slider 

```text
New-UDSlider -Value 1
```

## Slider with minimum and maximum values

```text
New-UDSlider -Min 10 -Max 1000
```

## Disabled Slider

```text
New-UDSlider -Disabled
```

## Slider with custom step size

```text
New-UDSlider -Min 10 -Max 1000 -Step 100
```

## Slider with marks

```text
New-UDSlider -Marks
```

## Range based slider

```text
New-UDSlider -Value @(1, 10)
```

## OnChange event for slider

```text
New-UDSlider -OnChange {
    Show-UDToast -Message $Body 
    Set-TestData $Body
}
```

