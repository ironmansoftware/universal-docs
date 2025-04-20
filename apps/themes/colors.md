---
description: About the color parameter on components.
---

# Colors

Many components accept a color parameter. Some color parameters allow you to select from a preset style like success and error. Other color parameters accept a `DashboardColor` object that can define a specific color using a name, hex value or RGB value.&#x20;

Below is an example of each type of configuration. A list of [known colors can be found here](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.knowncolor?view=net-9.0).&#x20;

```powershell
# Hex color 
New-UDIcon -Icon User -Color '#2596be'

# RGB values
New-UDIcon -Icon User -Color 'rgb(37, 150, 190)'

# Anything Color.FromName knows
New-UDIcon -Icon User -Color 'gray'
```
