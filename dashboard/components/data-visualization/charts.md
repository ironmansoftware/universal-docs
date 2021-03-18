---
description: Charting components for Universal Dashboard.
---

# Charts

Universal Dashboard provides several built-in charting solutions to help visualize your data retrieved from PowerShell.

{% hint style="info" %}
To use charts within your dashboard, you will need to add the UniversalDashboard.Charts component. 

[Learn more about adding custom component libraries](../../dashboards/#adding-custom-component-libraries)
{% endhint %}

## ChartJS

Universal Dashboard integrates with [ChartJS](https://www.chartjs.org/). 

### Creating a Chart

To create a chart, use `New-UDChartJS` and `New-UDChartJSData`. The below chart shows the top ten CPU using processes.

![](../../../.gitbook/assets/image%20%28157%29%20%281%29.png)

```PowerShell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'bar' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

### Types

#### Bar

![](../../../.gitbook/assets/image%20%28157%29%20%281%29%20%281%29.png)

```PowerShell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'bar' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

#### Horizontal Bar

![](../../../.gitbook/assets/image%20%28155%29.png)

```PowerShell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'horizontalBar' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

#### Line

![](../../../.gitbook/assets/image%20%28152%29.png)

```PowerShell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'line' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

#### Doughnut

![](../../../.gitbook/assets/image%20%28153%29.png)

```PowerShell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'doughnut' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

#### Pie

![](../../../.gitbook/assets/image%20%28154%29.png)

```PowerShell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'pie' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

#### Radar

![](../../../.gitbook/assets/image%20%28158%29.png)

```PowerShell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'radar' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

### Colors

Colors can be defined using the various color parameters of `New-UDChartJS`.

![](../../../.gitbook/assets/image%20%28151%29.png)

```PowerShell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 
 $Options = @{
   Type = 'bar'
   Data = $Data
   BackgroundColor = 'Red'
   BorderColor = '#c61d4a'
   HoverBackgroundColor = 'Blue'
   HoverBorderColor = '#451dc6'
   DataProperty = 'CPU'
   LabelProperty = 'ProcessName'
 }
 
 New-UDChartJS @Options
```

### Data Sets

By default, you do not need to define data sets manually. A single data set is created automatically when you use the `-DataProperty` and `-LabelProperty` parameters. If you want to define multiple data sets for a single chart, you can use the `-Dataset` property in conjunction with `New-UDChartJSDataset`. 

![](../../../.gitbook/assets/image%20%28156%29.png)

```PowerShell
$Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 
 $CPUDataset = New-UDChartJSDataset -DataProperty CPU -Label CPU -BackgroundColor '#126f8c'
 $MemoryDataset = New-UDChartJSDataset -DataProperty HandleCount -Label 'Handle Count' -BackgroundColor '#8da322'
 
 $Options = @{
   Type = 'bar'
   Data = $Data
   Dataset = @($CPUDataset, $MemoryDataset)
   LabelProperty = "ProcessName"
 }
 
 New-UDChartJS @Options
```

### Click Events

You can take action when a user clicks the chart. This example shows a toast with the contents of the `$Body`  variable. The `$Body` variable contains a JSON string with information about the elements that were clicked. 

![](../../../.gitbook/assets/z4axjkkvyu.gif)

```PowerShell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 
  $Options = @{
   Type = 'bar'
   Data = $Data
   DataProperty = 'CPU'
   LabelProperty = "ProcessName"
   OnClick = { 
      Show-UDToast -Message $Body
   }
 }
 
 
 New-UDChartJS @Options
```

### Auto refreshing charts

You can use `New-UDDynamic` to create charts that refresh on an interval.

![](../../../.gitbook/assets/cxez8afan4.gif)

```PowerShell
New-UDDynamic -Content {
    $Data = 1..10 | % { 
        [PSCustomObject]@{ Name = $_; value = get-random }
    }
    New-UDChartJS -Type 'bar' -Data $Data -DataProperty Value -Id 'test' -LabelProperty Name -BackgroundColor Blue
} -AutoRefresh -AutoRefreshInterval 1 
```

### Monitors

Monitors are a special kind of chart that tracks data over time. Monitors are good for displaying data such as server performance stats that change frequently. You return a single value from a monitor and it is graphed automatically over time. 

```PowerShell
New-UDChartJSMonitor -LoadData {
    Get-Random -Max 100 | Out-UDChartJSMonitorData
} -Labels "Random" -ChartBackgroundColor "#297741" -RefreshInterval 1
```

![](../../../.gitbook/assets/monitor.gif)

## Nivo Charts

Universal Dashboard integrates with [Nivo Charts](https://nivo.rocks/components). Below you will find examples and documentation for using these charts. 

### Creating a Chart

All the Nivo charts can be created with `New-UDNivoChart`. You will specify a switch parameter for the different types of charts. Each chart type will take a well defined data format via the `-Data` parameter. 

![](../../../.gitbook/assets/image%20%2893%29.png)

```PowerShell
$Data = 1..10 | ForEach-Object { 
    $item = Get-Random -Max 1000 
    [PSCustomObject]@{
        Name = "Test$item"
        Value = $item
    }
}
New-UDNivoChart -Id 'autoRefreshingNivoBar' -Bar -Keys "value" -IndexBy 'name' -Data $Data -Height 500 -Width 1000
```

### Patterns

Nivo provides the ability to specify patterns to display over data sets. You can configure these patterns with `New-UDNivoPattern` and `New-UDNivoFill` .

![](../../../.gitbook/assets/image%20%2892%29.png)

```PowerShell
$Data = @(
    @{
        country = 'USA'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
    @{
        country = 'Germany'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
    @{
        country = 'Japan'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
)

$Pattern = New-UDNivoPattern -Dots -Id 'dots' -Background "inherit" -Color "#38bcb2" -Size 4 -Padding 1 -Stagger
$Fill = New-UDNivoFill -ElementId "fries" -PatternId 'dots'

New-UDNivoChart -Definitions $Pattern -Fill $Fill -Bar -Data $Data -Height 400 -Width 900 -Keys @('burgers', 'fries', 'sandwich')  -IndexBy 'country'
```

### Responsive Widths

Nivo charts provide responsive widths so they will resize automatically when placed on a page or the browser is resized. A height is required when using responsive widths. 

![](../../../.gitbook/assets/responsive.gif)

### Auto Refreshing Charts

Like many components in Universal Dashboard v3, Nivo charts do not define auto-refresh properties themselves. Instead, you can take advantage of `New-UDDynamic` to refresh the chart on an interval. 

![](../../../.gitbook/assets/autorefresh.gif)

```PowerShell
New-UDDynamic -Content {
    $Data = 1..10 | ForEach-Object { 
        $item = Get-Random -Max 1000 
        [PSCustomObject]@{
            Name = "Test$item"
            Value = $item
        }
    }
    New-UDNivoChart -Id 'autoRefreshingNivoBar' -Bar -Keys "Value" -IndexBy 'name' -Data $Data -Height 500 -Width 1000
} -AutoRefresh
```

### OnClick

Nivo charts support OnClick event handlers. You will be provided with information about the data set that was clicked as JSON. 

![](../../../.gitbook/assets/onclick.gif)

```PowerShell
$Data = @(
    @{
        country = 'USA'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
    @{
        country = 'Germany'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
    @{
        country = 'Japan'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
)
New-UDNivoChart -Bar -Data $Data -Height 400 -Width 900 -Keys @('burgers', 'fries', 'sandwich')  -IndexBy 'country' -OnClick {
    Show-UDToast -Message $EventData -Position topLeft
}
```

### Types of Charts

#### Bar

```PowerShell
New-Example -Title 'Bar' -Description '' -Example {
    $Data = 1..10 | ForEach-Object { 
        $item = Get-Random -Max 1000 
        [PSCustomObject]@{
            Name = "Test$item"
            Value = $item
        }
    }
    New-UDNivoChart -Bar -Keys "Value" -IndexBy 'name' -Data $Data -Height 500 -Width 1000
}
```

#### Bubble

![](../../../.gitbook/assets/image%20%28102%29.png)

```PowerShell
$TreeData = @{
    Name     = "root"
    children = @(
        @{
            Name  = "first"
            children = @(
                @{
                    Name = "first-first"
                    Count = 7
                }
                @{
                    Name = "first-second"
                    Count = 8
                }
            )
        },
        @{
            Name  = "second"
            Count = 21
        }
    )
}

New-UDNivoChart -Bubble -Data $TreeData -Value "count" -Identity "name" -Height 500 -Width 800
```

#### Calendar

![](../../../.gitbook/assets/image%20%2898%29.png)

```PowerShell
$Data = @()
for($i = 365; $i -gt 0; $i--) {
    $Data += @{
        day = (Get-Date).AddDays($i * -1).ToString("yyyy-MM-dd")
        value = Get-Random
    }
}

$From = (Get-Date).AddDays(-365)
$To = Get-Date

New-UDNivoChart -Calendar -Data $Data -From $From -To $To -Height 500 -Width 1000 -MarginTop 50 -MarginRight 130 -MarginBottom 50 -MarginLeft 60
```

#### Heatmap

![](../../../.gitbook/assets/image%20%2895%29.png)

```PowerShell
$Data = @(
    @{
        state = "idaho"
        cats = 72307
        dogs = 23429
        moose = 23423
        bears = 784
    }
    @{
        state = "wisconsin"
        cats = 2343342
        dogs = 3453623
        moose = 1
        bears = 23423
    }
    @{
        state = "montana"
        cats = 9234
        dogs = 3973457
        moose = 23472
        bears = 347303
    }
    @{
        state = "colorado"
        cats = 345973789
        dogs = 0237234
        moose = 2302
        bears = 2349772
    }
)
New-UDNivoChart -Heatmap -Data $Data -IndexBy 'state' -keys @('cats', 'dogs', 'moose', 'bears')  -Height 500 -Width 1000 -MarginTop 50 -MarginRight 130 -MarginBottom 50 -MarginLeft 60
```

#### Line

```PowerShell
$Data = 1..10 | ForEach-Object { 
    @{
        id = "Line$_"
        data = @(
            $item = Get-Random -Max 1000 
            [PSCustomObject]@{
                x = "Test$item"
                y = $item
            }
        )
    }
}

New-UDNivoChart -Line -Data $Data -Height 500 -Width 1000 -LineWidth 1
```

#### Stream

![](../../../.gitbook/assets/image%20%2897%29.png)

```PowerShell
$Data = 1..10 | ForEach-Object { 
    @{
        "Adam" = Get-Random 
        "Alon" = Get-Random 
        "Lee" = Get-Random 
        "Frank" = Get-Random 
        "Bill" = Get-Random 
    }
}

New-UDNivoChart -Stream -Data $Data -Height 500 -Width 1000 -Keys @("adam", "alon", "lee", "frank", "bill")
```

#### Treemap

![](../../../.gitbook/assets/image%20%2891%29.png)

```PowerShell
$TreeData = @{
    Name     = "root"
    children = @(
        @{
            Name  = "first"
            children = @(
                @{
                    Name = "first-first"
                    Count = 7
                }
                @{
                    Name = "first-second"
                    Count = 8
                }
            )
        },
        @{
            Name  = "second"
            Count = 21
        }
    )
}

New-UDNivoChart -Treemap -Data $TreeData -Value "count" -Identity "name" -Height 500 -Width 800
```



