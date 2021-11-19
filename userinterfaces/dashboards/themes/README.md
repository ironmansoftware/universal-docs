# Themes

Universal Dashboard v3 is built on Material UI. Material UI provides a [built-in theme system ](https://material-ui.com/customization/theming/)that UD now takes advantage of. You can utilize this theme system by providing a hashtable of options to the `New-UDDashboard` 's `-Theme` parameter.

Here's an example of changing the theme's main color.

```powershell
$Theme = @{
    palette = @{
        primary = @{
            main = '#111111'
        }
    }
}
New-UDDashboard -Theme $Theme -Title 'Hello' -Content {
    New-UDButton -Text "Test " -OnClick {
        Show-UDToast -Message 'HEllo'
    }
}
```

{% hint style="info" %}
Note that when specifying keys that require a number, ensure that the key is specified as a string.&#x20;

```
grey = @{
    '50'              = '#fafafa'
    '100'             = '#f5f5f5'
    '200'             = '#eeeeee'
    '300'             = '#e0e0e0'
    '400'             = '#bdbdbd'
    '500'             = '#9e9e9e'
    '600'             = '#757575'
    '700'             = '#616161'
    '800'             = '#424242'
    '900'             = '#212121'
    A100              = '#d5d5d5'
    A200              = '#aaaaaa'
    A400              = '#303030'
    A700              = '#616161'
    contrastThreshold = '3'
    getContrastText   = 'f E()'
    augmentColor      = 'f B()'
    tonalOffset       = '0.2'
}
```
{% endhint %}

## Setting the default theme

You can set the default theme to either Light or Dark using the `-DefaultTheme` parameter.

```powershell
New-UDDashboard -Title 'Hello' -Content {
    New-UDButton -Text "Test " -OnClick {
        Show-UDToast -Message 'HEllo'
    }
} -DefaultTheme dark
```

## Changing the background color

You can change the page background color by setting the background default color. To adjust the header background color, set the primary main color.

```powershell
$Theme = @{
    palette = @{
        primary = @{
            main = '#876a38'
        }
        background = @{
            default = '#876a38'
        }
    }
#    typography = @{
#        fontSize = 20
#    }
}
New-UDDashboard -Theme $Theme -Title 'Hello' -Content {
    New-UDButton -Text 'Hello' 
}
```

![](<../../../.gitbook/assets/image (145).png>)

## Supporting dark and light palettes

To support dark and light palettes, you can define a dark and light sections in your hashtable. They have the same properties as a theme.

```powershell
$Theme = @{
    light = @{
        palette = @{
            primary = @{
                main = "#fff"
            }
        }
    }
    dark = @{
        palette = @{
            primary = @{
                main = "#333"
            }
        }
    }
}
New-UDDashboard -Theme $Theme -Title 'Hello' -Content {
    New-UDButton -Text 'Hello' 
}
```

![](../../../.gitbook/assets/3yizyxdoaa.gif)

## Changing the font size

To change the font size, set the typography fontSize property.

```powershell
$Theme = @{
    typography = @{
        fontSize = 20
    }
}
New-UDDashboard -Theme $Theme -Title 'Hello' -Content {
    New-UDButton -Text 'Hello' 
}
```

![](<../../../.gitbook/assets/image (146).png>)

## Changing default button colors

```powershell
$Theme = @{
    palette = @{
        grey = @{
            '300' = '#000'
        }
    }
}
New-UDDashboard -Theme $Theme -Title 'Hello' -Content {
    New-UDButton -Text 'Small Button'
}
```

![](<../../../.gitbook/assets/image (144).png>)

For a full list of options available for the theme system, you can look at the [default theme for Material UI](https://material-ui.com/customization/default-theme/).
