# Textbox Length Validation

This sample demonstrates how to validate the length of text entered by a user. The button is disabled until at least 2 characters are entered. OnEnter will not reload the dynamic until the test matches the length.

```powershell
New-UDCard -Title "Search" -Style @{height = 850 } -Content {
    New-UDTextbox -Id 'UsernameBox' -Label "Initials or Name" -OnEnter {
        if ($EventData.Length -gt 2)
        {
            Sync-UDElement -Id 'SearchForUserValidationID'
        }
    } -OnChange {
        $Disabled = (Get-UDElement -Id 'UsernameBox').value.Length -lt 2
        Set-UDElement -Id 'search' -Properties @{
            disabled = $Disabled
        }
    }
    New-UDButton -OnClick {
        Sync-UDElement -Id 'SearchForUserValidationID'
    } -Text "Search" -Id 'search' -Disabled
    
    New-UDDynamic -Id 'SearchForUserValidationID' -Content {
        $UsernameBoxValue = (Get-UDElement -Id 'UsernameBox').value
        New-UDTypography $UsernameBoxValue
    } -LoadingComponent {
        New-UDProgress
        New-UDTypography -Text "Loading users..."
    }

}

```
