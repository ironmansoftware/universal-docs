---
description: Paper component for Universal Apps
---

# Paper

**In Material Design, the physical properties of paper are translated to the screen.**

The background of an application resembles the flat, opaque texture of a sheet of paper, and an application’s behavior mimics paper’s ability to be re-sized, shuffled, and bound together in multiple sheets.

## Paper

![](<../../../.gitbook/assets/image (327).png>)

```powershell
New-UDPaper -Elevation 0 -Content {} 
New-UDPaper -Elevation 1 -Content {} 
New-UDPaper -Elevation 3 -Content {}
```

## Square Paper

By default, paper will have rounded edges. You can reduce the rounding by using a square paper.

```powershell
New-UDPaper -Square -Content {}
```

## Colored Paper

The `-Style` parameter can be used to color paper. Any valid CSS can be included in the hashtable for a style.

The following example creates paper with a red background.

```powershell
New-UDPaper  -Content { } -Style @{ 
     backgroundColor = 'red'
}
```

## API

* [New-UDPaper](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDPaper.txt)
