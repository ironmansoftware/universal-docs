---
description: Display pages are desktop windows.
---

# Pages

![Page displayed as desktop window](<../.gitbook/assets/image (136).png>)

You can use the `Show-PSUPage` cmdlet from any script to pop up a tool window for a page, dashboard or other URL. This means that you can integrate with Hotkeys, Shortcuts, Protocol handlers and more to display user interfaces that appear like regular windows.&#x20;

## Displaying a Page

For example, you could place the following in a script to display a page.&#x20;

```powershell
Show-PSUPage -Url "MyPage"
```
