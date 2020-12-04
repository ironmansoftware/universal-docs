---
description: SQL examples for PowerShell Universal.
---

# SQL

## Server-side SQL Table

This example uses Universal Dashboard.

This example takes advantage of a SQL server and the `New-UDTable` cmdlet to create a table that retrieves data from a database table. The filtering, sorting and paging take place within the database.

This example assumes that we have a database called podcasts running in the local MS SQL Server. It has a table called shows that includes a column called host and a column called name. 

```text
Start-PSUServer -Port 8080 -Configuration {
    New-PSUDashboard -Name 'SQL' -BaseUrl "/" -Framework 'UniversalDashboard:Latest' -Content {
        New-UDDashboard -Title 'SQL' -Content {
            New-UDTable -Title 'Shows' -LoadData {
                $TableData = ConvertFrom-Json $Body
            
                $OrderBy = $TableData.orderBy.field
                if ($OrderBy -eq $null)
                {
                    $OrderBy = "name"
                }
            
                $OrderDirection = $TableData.OrderDirection
                if ($OrderDirection -eq $null)
                {
                    $OrderDirection = 'asc'
                }
            
                $Where = ""
                if ($TableData.Filters) 
                {
                    $Where = "WHERE "
            
                    foreach($filter in $TableData.Filters)
                    {
                        $Where += $filter.column.field + " LIKE '%" + $filter.value + "%' AND "
                    }
            
                    $Where += " 1 = 1"
                }
            
                $PageSize = $TableData.PageSize 
                # Calculate the number of rows to skip
                $Offset = $TableData.Page * $PageSize
                $Count = Invoke-DbaQuery -SqlInstance localhost\MSSQLSERVER -Database 'podcasts' -Query "SELECT COUNT(*) as count FROM shows $Where"
            
                $Data = Invoke-DbaQuery -SqlInstance localhost\MSSQLSERVER -Database 'podcasts' -Query "SELECT * FROM shows $Where ORDER BY $orderBy $orderdirection OFFSET $Offset ROWS FETCH NEXT $PageSize ROWS ONLY" | ForEach-Object {
                    @{ 
                        name = $_.name 
                        host = $_.host
                    }
                } 
                $Data | Out-UDTableData -Page $TableData.page -TotalCount $Count.Count -Properties $TableData.properties
            } -Columns @(
                New-UDTableColumn -Property 'name' -Sort $true -Filter $true
                New-UDTableColumn -Property 'host' -Sort $true -Filter $true
            ) -Sort -Filter
        }
    }
}
```

