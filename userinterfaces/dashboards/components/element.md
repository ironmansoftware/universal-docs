---
description: Information about UDElements.
---

# Element

The `New-UDElement` cmdlet allows you to create custom React elements within your dashboard. Similar to `New-UDHtml`, you can define HTML elements using `New-UDElement`. Unlike, `New-UDHtml`, you can update elements, set auto refresh and take advantage of the React component system.

## Create an Element

You need to specify the `-Tag` and `-Content` when creating an element. The below example creates a div tag.

```powershell
New-UDElement -Tag 'div' -Content { 'Hello' }
```

You can nest components within each other to create HTML structures. For example, you could create an unordered list with the following example.

```powershell
New-UDElement -Tag 'ul' -Content {
    New-UDElement -Tag 'li' -Content { 'First' }
    New-UDElement -Tag 'li' -Content { 'Second' }
    New-UDElement -Tag 'li' -Content { 'Third' }
}
```

## Setting Attributes

You can select attributes of an element (like HTML attributes) by using the `-Attributes` parameter. This parameter accepts a hashtable of attribute name and values. The below example creates red text.

```powershell
New-UDElement -Tag 'div' -Content { 'Hello' } -Attributes @{
    style = @{
        color = 'red'
    }
}
```

You can wrap any component with New-UDElement and add an event handler.

```powershell
New-UDElement -Tag div -Content {
    New-UDIcon -Icon "user"
} -Attributes @{
    onClick = {
        Show-UDToast "Nice!"
    }
}
```


## Auto Refreshing Elements

You can define the `-AutoRefresh`, `-RefreshInterval` and `-Endpoint` parameters to create an element the refreshes on a certain interval. The below example creates an element that refreshes every second and displays the current time.

```powershell
New-UDElement -Tag 'div' -Endpoint {
    Get-Date
} -AutoRefresh -RefreshInterval 1
```

## Setting Element Properties Dynamically

You can use the `Set-UDElement` cmdlet to set element properties and content dynamically. The following example sets the content of the element to the current time.

```powershell
New-UDElement -Tag 'div' -Id 'myElement' -Content { }

New-UDButton -Text 'Click Me' -OnClick {
    Set-UDElement -Id 'myElement' -Content { Get-Date }
}
```

You can also set attributes by using the `-Properties` parameter of `Set-UDElement`. The following example sets the current time and changes the color to red.

```powershell
    New-UDElement -Tag 'div' -Id 'myElement' -Content { }

    New-UDButton -Text 'Click Me' -OnClick {
        Set-UDElement -Id 'myElement' -Content { Get-Date } -Properties @{ Attributes = @{ style = @{ color = "red" } } }
    }
```

## Adding Child Elements

You can add child elements using `Add-UDElement`. The following example adds child list items to an unordered list.

```powershell
New-UDElement -Tag 'ul' -Content {

} -Id 'myList'

New-UDButton -Text 'Click Me' -OnClick {
    Add-UDElement -ParentId 'myList' -Content {
        New-UDElement -Tag 'li' -Content { Get-Date }
    }
}
```

## Clearing Child Elements

You can clear the child elements of an element by using `Clear-UDElement`. The following example clears all the list items from an unordered list.

```powershell
New-UDElement -Tag 'ul' -Content {
    New-UDElement -Tag 'li' -Content { 'First' }
    New-UDElement -Tag 'li' -Content { 'Second' }
    New-UDElement -Tag 'li' -Content { 'Third' }
}  -Id 'myList'

New-UDButton -Text 'Click Me' -OnClick {
    Clear-UDElement -Id 'myList'
}
```

## Forcing an Element to Reload

You can force an element to reload using `Sync-UDElement`. The following example causes the div to reload with the current date.

```powershell
New-UDElement -Tag 'div' -Endpoint {
    Get-Date
} -Id 'myDiv'

New-UDButton -Text 'Click Me' -OnClick {
    Sync-UDElement -Id 'myDiv'
}
```

## Removing an Element

You can remove an element by using `Remove-UDElement`.

```powershell
New-UDElement -Tag 'div' -Endpoint {
    Get-Date
} -Id 'myDiv'

New-UDButton -Text 'Click Me' -OnClick {
    Remove-UDElement -Id 'myDiv'
}
```

## API

* [**Get-UDElement**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Get-UDElement.txt)****
* ****[**Set-UDElement**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-UDElement.txt)****
* ****[**Remove-UDElement**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Remove-UDElement.txt)****
* ****[**Add-UDElement**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Add-UDElement.txt)****
* ****[**Clear-UDElement**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Clear-UDElement.txt)****
* ****[**Sync-UDElement**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Sync-UDElement.txt)****
* ****[**Select-UDElement**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Select-UDElement.txt)

****
