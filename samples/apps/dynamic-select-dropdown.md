---
description: Create a dynamic select dropdown.
---

# Dynamic Select Dropdown

This sample creates a dynamic select drop down where the second select changes based on the first.&#x20;

<figure><img src="../../.gitbook/assets/image (572).png" alt=""><figcaption><p>Dynamic dropdown</p></figcaption></figure>

```powershell
$Session:Cities = @()

New-UDSelect -Option {
    New-UDSelectOption -Name 'Idaho' -Value 'Idaho'
    New-UDSelectOption -Name 'Michigan' -Value 'Michigan'
    New-UDSelectOption -Name 'Wisconsin' -Value 'Wisconsin'
} -Label 'State' -OnChange {
    # Create session data based on the state selected
    if ($EventData -eq 'Idaho')
    {
       $Session:Cities = @("Boise", "Hailey", "Stanley")
    }
    
    if ($EventData -eq 'Michigan')
    {
       $Session:Cities = @("Ann Arbor", "Detroit", "Ironwood")
    }
    
    if ($EventData -eq 'Wisconsin')
    {
       $Session:Cities = @("Madison", "Milwaukee", "Irma")
    }

    # Refresh the city dynamic region
    Sync-UDElement -Id 'city'
}

New-UDDynamic -Id 'city' -Content {
   # if we don't have any cities, disable the select
   $Disabled = $Session:Cities.Length -eq 0

   New-UDSelect -Option {
     $Session:Cities | Foreach-Object {
         New-UDSelectOption -Name $_ -Value $_
     }
   } -Disabled:$Disabled -Label 'City'
}

```
