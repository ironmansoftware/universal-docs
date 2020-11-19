---
description: Code editor component for Universal Dashboard.
---

# Code Editor

{% hint style="info" %}
To use a code editor within your dashboard, you will need to add the UniversalDashboard.CodeEditor component. 

[Learn more about adding custom component libraries](../../dashboards/#adding-custom-component-libraries)
{% endhint %}

The code editor component allows you to host the [Microsoft Monaco ](https://microsoft.github.io/monaco-editor/)editor within your dashboards. 

## Creating a Code Editor

You can create a new code editor with the `New-UDCodeEditor` cmdlet. Specifying the `-Language` parameter will enable syntax highlighting for that language. You will need to specify a height in pixels. 

```text
New-UDCodeEditor -Height '500' -Language 'powershell'
```

![](../../../.gitbook/assets/image%20%28181%29.png)

## Populating Code

Use the `-Code` parameter to specify code that will be populated within the code editor when it loads. 

```text
New-UDCodeEditor -Height '500' -Language 'powershell' -Code '#Hello, world!'
```

## Retrieving code from another component

You can retrieve code from another component using the `Get-UDElement` cmdlet and accessing the code property of the hashtable that is returned. 

```text
New-UDCodeEditor -Height '500' -Language 'powershell' -Code '#Hello, world!' -Id 'editor'

New-UDButton -Text 'Get Code' -OnClick {
    Show-UDToast -Message (Get-UDElement -id 'editor').Code
} 
```

## Setting code from another component

You can set code from another component using the `Set-UDElement` cmdlet. Specify the code value in a hashtable passed to the `-Properties` parameter. 

```text
New-UDCodeEditor -Height '500' -Language 'powershell' -Code '#Hello, world!' -Id 'editor'

New-UDButton -Text 'Get Code' -OnClick {
    Set-UDElement -Id 'editor' -Properties @{
        code = "# Hello!"
    }
} 
```

