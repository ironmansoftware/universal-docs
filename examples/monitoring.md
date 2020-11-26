# Monitoring

## Windows Performance Counter Charts

This example uses [PowerShell Universal Dashboard](../dashboard/about.md).

In this example, we take advantage of Universal Dashboard scheduled endpoints, the in-memory cache and the UDMonitor component. We update the counter sets to use in the cache and load each of the counters' value in the set into an array to use in the dashboard. We then create a dashboard that dynamically creates UDMonitor charts within the page. Each monitor will update every 3 seconds with new data.

```text
Start-PSUServer -Port 8080 -Configuration {
    New-PSUDashboard -Name 'Performance' -BaseUrl '/' -Framework 'UniversalDashboard:Latest' -Content {

        $Schedule = New-UDEndpointSchedule -Every 5 -Second
        New-UDEndpoint -Schedule $Schedule -Endpoint {
            if (-not $Cache:CounterSets)
            {
                $Cache:CounterSets = Get-Counter -ListSet * | Select-Object -ExpandProperty 'CounterSetName'
                $Cache:CurrentSets = @( "IPv4")
            }
            
            $Cache:Data = @()
            foreach($set in $Cache:CurrentSets)
            {
                $Data = @{
                    Set = $set
                    Counters = @()
                }

                $Counters = (Get-Counter -ListSet $set).Paths
                foreach($Counter in $Counters)
                {
                    
                    $Value = 0 
                    try {
                        $Value = (Get-Counter -Counter $Counter -ErrorAction SilentlyContinue).CounterSamples[0].CookedValue
                    } catch {}
                    
                    $Data.Counters += @{ Name = $Counter; Value = $Value }
                }

                $Cache:Data += $Data
            }
        } | Out-Null

        New-UDDashboard -Title 'Performance' -Content {
            foreach($Data in $Cache:Data)
            {
                New-UDTypography -Text $Data.Set -Variant h4
                New-UDRow -Columns {
                    foreach($Counter in $Data.Counters)
                    {
                        New-UDColumn -Size 4 -LargeSize 3 -Content {
                            New-UDTypography -Text $Counter.Name
                            New-UDChartJSMonitor -LoadData {
                                $Set = $Cache:Data | Where-Object Set -eq $Data.Set
                                $Value = ($Set.Counters | Where-Object Name -eq $Counter.Name).Value
                                if (-not $Value)
                                {
                                    $Value = 0
                                }
                                $Value | Out-UDChartJSMonitorData
                            } -Labels "Value" -ChartBackgroundColor "#297741" -RefreshInterval 3 -DataPointHistory 10
                        } 
                    }
                }
            }
        }
    } -Component @("UniversalDashboard.Charts:1.3.0")
} 
```

![](../.gitbook/assets/image%20%28204%29.png)

