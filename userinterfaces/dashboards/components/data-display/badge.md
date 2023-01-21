# Badge

## Basic Badge

Examples of badges containing text, using primary and secondary colors. The badge is applied to its children.

![](<../../../../.gitbook/assets/image (317) (1).png>)

```powershell
  New-UDBadge -BadgeContent { 4 } -Children {
      New-UDIcon -Icon Envelope -Size 2x
  } -Color primary
```

## Color&#x20;

![](<../../../../.gitbook/assets/image (347) (1).png>)

```powershell
New-UDBadge -BadgeContent { 4 } -Children {
    New-UDIcon -Icon Envelope -Size 2x
} -Color secondary
New-UDBadge -BadgeContent { 4 } -Children {
    New-UDIcon -Icon Envelope -Size 2x
} -Color success
```

## API&#x20;

* [New-UDBadge](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDBadge.txt)
