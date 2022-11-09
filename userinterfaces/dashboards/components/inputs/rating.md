---
description: Rating input component.
---

# Rating

## Basic Rating

```powershell
New-UDRating 
```

![](<../../../../.gitbook/assets/image (1).png>)

## OnChange

Take action when the rating is changed.&#x20;

```powershell
New-UDRating -OnChange {
    Show-UDToast $EventData
}
```

## Maximum

Change the maximum rating.&#x20;

![](<../../../../.gitbook/assets/image (8).png>)

```powershell
New-UDRating -Max 10
```

## Precision

Change the precision for ratings.&#x20;

![](<../../../../.gitbook/assets/image (2).png>)

```powershell
New-UDRating -Precision .5
```

## Size

Change the size of the rating icons.&#x20;

![](<../../../../.gitbook/assets/image (7).png>)

```powershell
New-UDRating -Size large
```
