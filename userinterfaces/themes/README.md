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
}
New-UDDashboard -Theme $Theme -Title 'Hello' -Content {
    New-UDButton -Text 'Hello' 
}
```

![](<../../.gitbook/assets/image (166).png>)

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

![](../../.gitbook/assets/3yIzYxdOaa.gif)

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

![](<../../.gitbook/assets/image (271).png>)

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

![](<../../.gitbook/assets/image (465).png>)

For a full list of options available for the theme system, you can look at the [default theme for Material UI](https://material-ui.com/customization/default-theme/).

## Component Overrides

You can override any component CSS value using the theme engine. In order to override a component's base theming, you will need to identify the CSS class name applied to that element.&#x20;

To identify a component's CSS classes, use the developer tools of your browser. Right click on the component you wish to style and click Inspect Element.&#x20;

This will highlight the HTML elements that make up that component. In the image below, you will see we have numerous CSS classes being applied such as:

* MuiButtonBase-root
* MuiButton-root
* MuiButton-label
* MuiTouchRipple-root

![](<../../.gitbook/assets/image (428).png>)

In order to override these various elements, you will need to add an `overrides` key to your theme.&#x20;

```powershell
$Theme = @{
   overrides = @{
   
   }
}
```

Next, you'll need to add keys to the overrides for each element you wish to modify. Notice that I have not included the portion of the class name after the hyphen.&#x20;

```powershell
$Theme = @{
   overrides = @{
       MuiButton = @{
       
       }
   }
}
```

Now, add the subitems you wish to modify to the class name.&#x20;

```powershell
$Theme = @{
   overrides = @{
       MuiButton = @{
           root = @{
           
           }
           label = @{
           
           }
       }
   }
}
```

The last step is to define the CSS properties you wish to apply to elements that use these classes.

```powershell
$Theme = @{
   overrides = @{
       MuiButton = @{
           root = @{
               padding = 20
           }
           label = @{
               fontSize = 40
           }
       }
   }
}
```

For more examples, look at the Onepirate and Paperbase themes below that include many component overrides.

## Example Themes

### Sand

![Sand Theme](<../../.gitbook/assets/image (468).png>)

```powershell
$Theme = @{
  palette = @{
    primary = @{
      light = '#ffe8d6'
      main = '#ddbea9'
      dark = '#cb997e'
    }
    secondary = @{
      light = '#b7b7a4'
      main = '#a5a58d'
      dark = '#6b705c'
    }
  }
}
```

### Compliment

![](<../../.gitbook/assets/image (9).png>)

```powershell
$Theme = @{
  palette = @{
    primary = @{
      light = '#e9c46a'
      main = '#2a9d8f'
      dark = '#264653'
    }
    secondary = @{
      light = '#e9c46a'
      main = '#f4a261'
      dark = '#e76f51'
    }
  }
}
```

### Pastel

![](<../../.gitbook/assets/image (562).png>)

```powershell
$Theme = @{
  palette = @{
    primary = @{
      light = '#ffcdb2'
      main = '#ffb4a2'
      dark = '#e5989b'
    }
    secondary = @{
      light = '#e5989b'
      main = '#b5838d'
      dark = '#6d6875'
    }
  }
}
```

### Onepirate

![](<../../.gitbook/assets/image (93).png>)

Based on the Material UI theme, [Onepirate](https://material-ui.com/store/previews/onepirate/).&#x20;

```powershell
$Theme = @{
  palette = @{
    primary = @{
      light = '#69696a'
      main = '#28282a'
      dark = '#1e1e1f'
    }
    secondary = @{
      light = '#fff5f8'
      main = '#ff3366'
      dark = '#e62958'
    }
    warning = @{
      main = '#ffc071'
      dark = '#ffb25e'
    }
    error = @{
        xLight = '#ffebee'
        main = '#f44336'
        dark = '#d32f2f'
    }
    success = @{
        xLight = '#e8f5e9'
        main = '#4caf50'
        dark = '#388e3c'
    }
  }
  typography = @{
    fontFamily = "'Work Sans', sans-serif"
    fontSize = 14
    fontWeightLight = 300
    fontWeightRegular = 400
    fontWeightMedium = 700
    fontFamilySecondary = "'Roboto Condensed', sans-serif"
    h1 = @{
        letterSpacing = 0
        fontSize = 60
    }
    h2 = @{
        fontSize = 48
    }
    h3 = @{
        fontSize = 42
    }
    h4 = @{
        fontSize = 36
    }
    h5 = @{
        fontSize = 20
        fontWeight = 100
    }
    h6 = @{
        fontSize = 18
    }
    subtitle1 = @{
        fontSize = 18
    }
    body = @{
        fontSize = 16
    }
    body2 = @{
        fontSize = 14
    }
  }
  overrides = @{
    MuiButton = @{
        root = @{
            borderRadius = 0
            fontWeight = 300
            fontFamily = "'Roboto Condensed', sans-serif"
            padding = 10
            fontSize = 14
            boxShadow = 'none'

        }
    }
    MuiInput = @{
        root = @{
            padding = 0
            backgroundColor = 'white'
            'label + &' = @{
                marginTop = 3
            }
        }
        input = @{
            fontSize = 16
            padding = 16
            border = '1px solid #e9ddd0'
            '&:focus' = @{
                borderColor = '#ff3366'
            }
        }
        'underline:after' = @{
            borderBottom = 'none'
        }
    }
    MuiInputLabel = @{
        root = @{
            fontSize = 18
        }
    }
    MuiFormControl = @{
        root = @{
            border = 'none'
        }
    }
    MuiCard = @{
        root = @{
            boxShadow = 'none'
        }
    }
    MuiPaper = @{
        root = @{
             backgroundColor = '#fff5f8'
        }
        rounded = @{
            borderRadius = 0
        }
    }
  }
}
```

The dashboard used to generate the above image is included below.&#x20;

```powershell
New-UDDashboard -Theme $theme -Title "Onepirate" -Content {
    New-UDTypography -Text 'Upgrade your Sundays' -Variant h2 -Align Center
    New-UDTypography -Text 'Enjoy secret offers up to -70% off the best luxury hotels every Sunday.' -Variant h5 -Align Center
    New-UDElement -Tag div -Attributes @{
        style = @{
            textAlign = 'center'
        }
    } -Content {
        New-UDButton -Text 'Register' -Color secondary
    }
            
    New-UDCard -Title 'SIGN UP' -Content {
        New-UDForm -Content {
            New-UDTextbox -Label 'EMAIL ADDRESS' 
        } -OnSubmit {

        }
    } -Elevation 0
}
```

### Paperbase

![Paperbase in Universal Dashboard](<../../.gitbook/assets/image (261).png>)

Based on the Material UI theme, [Paperbase](https://material-ui.com/store/previews/paperbase/).&#x20;

```powershell
$Theme = @{
  palette = @{
    primary = @{
      light = '#63ccff'
      main = '#009be5'
      dark = '#006db3'
    }
  }
  typography = @{
    h5 = @{
      fontWeight = 500
      fontSize = 26
      letterSpacing = 0.5
    }
  }
  shape = @{
    borderRadius = 8
  }
  mixins = @{
    toolbar = @{
      minHeight = 48
    }
  }
  overrides = @{
    MuiDrawer = @{
        paper = @{
          backgroundColor = '#081627'
        }
    }
    MuiButton = @{
        label = @{
            textTransform = 'none'
        }
        contained = @{
          boxShadow = 'none'
          '&:active' = @{
            boxShadow = 'none'
          }
        }
    }
    MuiTabs = @{
        root = @{
          marginLeft = 1
        }
        indicator = @{
          height = 3
          borderTopLeftRadius = 3
          borderTopRightRadius = 3
          backgroundColor = '#000'
        }
    }
    MuiTab = @{
        root = @{
            textTransform = 'none'
            margin = '0 16px'
            minWidth = 0
            padding = 0
        }
    }
    MuiIconButton = @{
        root = @{
          padding = 1
        }
    }
    MuiTooltip = @{
        tooltip = @{
          borderRadius = 4
        }
    }
    MuiDivider = @{
        root = @{
          backgroundColor = 'rgb(255,255,255,0.15)'
        }
    }
    MuiListItemButton = @{
        root = @{
          '&.Mui-selected' = @{
            color = '#4fc3f7'
          }
        }
    }
    MuiListItemText = @{
        primary = @{
            color = 'rgba(255, 255, 255, 0.7) '
          fontSize = 14
          fontWeight = 500
        }
    }
    MuiListItemIcon = @{
        root = @{
          color = 'rgba(255, 255, 255, 0.7) '
          minWidth = 'auto'
          marginRight = 2
          '& svg' = @{
            fontSize = 20
          }
        }
    }
    MuiAvatar = @{
        root = @{
          width = 32
          height = 32
        }
    }
  }
}

```

This the dashboard used to create the above image.&#x20;

```powershell
$Navigation = @(
    New-UDListItem -Label "Home"
    New-UDListItem -Label "Getting Started" -Children {
        New-UDListItem -Label "Installation" -Icon (New-UDIcon -Icon envelope) -OnClick { Invoke-UDRedirect '/installation' }
        New-UDListItem -Label "Usage" -Icon (New-UDIcon -Icon edit) -OnClick { Invoke-UDRedirect '/usage' }
        New-UDListItem -Label "FAQs" -Icon (New-UDIcon -Icon trash) -OnClick { Invoke-UDRedirect '/faqs' }
        New-UDListItem -Label "System Requirements" -Icon (New-UDIcon -Icon bug) -OnClick { Invoke-UDRedirect '/requirements' }
        New-UDListItem -Label "Purchasing" -OnClick { Invoke-UDRedirect '/purchasing'}
    }
)


New-UDDashboard -Theme $theme -Title "Paperbase" -Content {
    New-UDButton -Text 'Add user' -Color primary
    New-UDCard -Title 'User Info' -Content {
        "No users for this project yet."
    }
} -Navigation $Navigation -NavigationLayout Permanent
```
