---
description: An example of a data grid that queries and updates data in SQL.
---

# SQL Data Grid

This example uses `Invoke-DbaQuery` from dbatools to query and update data in a SQL database. It implements paging, sorting and filtering via the data grid's `-LoadRows` event handler. It also renders buttons within the table that updates the database based on selections.&#x20;

Additionally, bulk actions are performed using checkbox selection.&#x20;

This example requires the following table.

```sql
CREATE TABLE [dbo].[Certificates](
	[CertificateId] [int] NULL,
	[Decision] [varchar](255) NULL,
	[UserName] [varchar](255) NULL,
	[GroupName] [varchar](255) NULL,
	[AppName] [varchar](255) NULL
) ON [PRIMARY]
```

The data grid is defined within a dynamic region with some basic properties.&#x20;

```powershell
New-UDDynamic -Id "DynamicTable" {
      New-UDDataGrid -ShowPagination -PageSize 10 -RowsPerPageOptions @(10, 25, 50, 100, 200) -CheckboxSelection -LoadRows {
```

The `-LoadRows` event handler is where the bulk of the work is done. It's broken down into the following steps.&#x20;

### Columns

The columns used in this example are basic, aside from a decision column that is used to update the SQL database.&#x20;

The basic columns to display look like this. Properties that are returned from the SQL query will be available in render methods but will not be displayed.&#x20;

```powershell
New-UDDataGridColumn -HeaderName 'User' -Field 'UserName' -Filterable -Sortable -Description 'UserName'
New-UDDataGridColumn -HeaderName 'Group' -Field 'GroupName'  -Filterable -Sortable
New-UDDataGridColumn -HeaderName 'App' -Field 'AppName' -Filterable -Sortable
```

We will implement a complex column to update the SQL database. The `$EventData` variable will include the entire row's data. We can use this data to render buttons based on its state. If the certificate is approved, we will create green buttons. If the certificate is revoked, we will create red buttons. Clicking the buttons will run an UPDATE command and then reload the dynamic region.&#x20;

```powershell
New-UDDataGridColumn -HeaderName 'Decision' -Field 'Decision' -MinWidth 300 -Render {     
    New-UDDynamic -Id $EventData.CertificateId -Content {
        function New-DecisionButton {
            param(
                $Text,
                $Icon,
                $Style,
                $CertificateId,
                $Decision
            )

            New-UDButton -Text $Text -Icon $Icon -Style $Style -OnClick {
                $Session:updateButton = $true
                $Query = @"
            UPDATE Certificates
            SET Decision = $Decision
            WHERE CertificateId = $CertificateId;
"@

                Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -Query $Query
                Sync-UDElement -Id $CertificateId
            } -ShowLoading
        }

        if ($Session:updateButton) {
            $item = Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -Query ('SELECT * FROM [dbo].[Certificates] WHERE CertificateId = {0}' -f $EventData.CertificateId)
            $EventData.Decision = $item.Decision
            $Session:updateButton = $false
        }

        if ($EventData.Decision -eq 1) {
            New-DecisionButton -Text 'Approve' -Icon $Page:IconApprove -Style $Page:BtnGreenApprove -CertificateId $EventData.CertificateId -Decision 'NULL'
            New-DecisionButton -Text 'Revoke' -Icon $Page:IconRevokeNeutral -Style $Page:BtnWhiteRevoke -CertificateId $EventData.CertificateId -Decision '0'
        }
        elseif ($EventData.Decision -eq 0) {
            New-DecisionButton -Text 'Approve' -Icon $Page:IconApproveNeutral -Style $Page:BtnWhiteApprove -CertificateId $EventData.CertificateId -Decision '1'
            New-DecisionButton -Text 'Revoke' -Icon $Page:IconRevoke -Style $Page:BtnRedRevoke -CertificateId $EventData.CertificateId -Decision 'NULL'
        }
        else {
            New-DecisionButton -Text 'Approve' -Icon $Page:IconApproveNeutral -Style $Page:BtnWhiteApprove -CertificateId $EventData.CertificateId -Decision '1'
            New-DecisionButton -Text 'Revoke' -Icon $Page:IconRevokeNeutral -Style $Page:BtnWhiteRevoke -CertificateId $EventData.CertificateId -Decision '0'
        }
    }
}
```

### Filtering

Filtering is performed by accessing the `$EventData` variable (assigned to `$Context` in this example). Filters are available as a property of the context. Filters also include the logic operator used. This will be a and or or operator. We construct a SQL where expression and populate a hashtable of parameters.&#x20;

```powershell
$SqlFilter = ""
$Parameters = @{}
if ($Context.Filter.Items.Count -gt 0) {
    $count = 1
    $ParameterName = "P$count"
    foreach ($filter in $Context.Filter.Items) {
        if ($count -gt 1) {
            $SqlFilter += " $($Context.Filter.logicOperator) "
        }
        else {
            $SqlFilter += " WHERE "
        }

        $Value = $Filter.Value

        switch ($filter.Operator) {
            "contains" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) LIKE CONCAT('%', @$ParameterName, '%') " }
            "equals" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) = @$ParameterName " }
            "startsWith" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) LIKE CONCAT(@$ParameterName, '%') " }
            "endsWith" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) LIKE CONCAT('%', @$ParameterName) " }
            "isAnyOf" {
                $Value = $Value -join ','
                $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) IN (SPLIT_STRING(@$ParameterName)) "
            }
            "isempty" { $SqlFilter += " TRIM ($(ConvertTo-ProperCase $filter.Field)) IS NULL " }
            "isnotempty" { $SqlFilter += " TRIM ($(ConvertTo-ProperCase $filter.Field)) IS NOT NULL " }
            "notequals" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) != @$ParameterName " }
            "notcontains" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) NOT LIKE CONCAT('%', @$ParameterName,'%') " }
        }

        $Parameters[$ParameterName] = $Value
        $count += 1
    }
}

```

The `ConvertTo-ProperCase` function adjusts the field name, which will be lower case, into the correct case used for the SQL server columns.&#x20;

### Paging&#x20;

Paging data is also sent via the context. We can calculate the offset and page size using the following code.&#x20;

```powershell
$PageSize = $Context.PageSize
$Offset = $Context.Page * $PageSize
$sqlPage = "OFFSET $Offset ROWS FETCH NEXT $($Context.PageSize) ROWS ONLY;"
```

### Sorting&#x20;

Columns used for sorting and their direction are also included in the context. This example uses single column sorting but the sort value is an array if multi-column sort is enabled.&#x20;

```powershell
if ($Context.Sort[0].field -ne $null) {
    $sqlSort = "ORDER BY $(ConvertTo-ProperCase $Context.Sort[0].field) $($Context.Sort[0].sort) "
}
else {
    $sqlSort = "ORDER BY (SELECT NULL)"
}
```

### Execution

Once we have constructed the SQL query portions and the parameters from the context, we can invoke our query. First, we need to get a total count of rows.&#x20;

```powershell
$Query = '{0} {1}' -f $Query, "$SqlFilter $sqlSort $sqlPage"
$Count = Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -As SingleValue -Query "SELECT COUNT(*) as count FROM dbo.Certificates $SqlFilter" -SqlParameter $Parameters
```

Once we have our count, the next step is to run the query. We return the rows as PSObjects. We need to format the return data to include the rows and the count.&#x20;

```powershell
$Data = Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -As PSObjectArray -Query $Query -SqlParameter $Parameters

@{
    rows     = [Array]$Data
    rowCount = $Count
}
```

### Bulk Actions

Using the selection feature of the data grid, we can record the row selections and then perform bulk actions using a select dropdown.&#x20;

The first step is to store the selections in session state. The `$EventData` variable of `OnSelectionChanged` is a list of the IDs of the rows. The data grid requires an ID to be defined for each row. If no ID property is found on a row, a random one is generated. Since we want deterministic selections, we use the CertificateID property as an ID in the select to allow for us to use that in queries. Below we store the selected IDs in a session variable and update a label for the select dropdown.&#x20;

```powershell
-OnSelectionChange {
    $Session:Selections = $EventData
    if ($Session:Selections.Count -le 0) {
        $Page:TickedCount = ''    
    }
    else {
        $Page:TickedCount = ' ({0})' -f $Session:Selections.Count
    }                
    Sync-UDElement -Id 'DropDownDynamic'
} 
```

The select drop down uses the selections and then issues an UPDATE command for each of this. This could be optimized to execute a single command with a list of IDs. Once the code the OnChange is run, the table is updated and the drop down is refreshed.&#x20;

```powershell
New-UDDynamic -Id "DropDownDynamic" {
    New-UDSelect -Id 'DropDown' -DefaultValue 'Bulk Decisions' -Option {
        New-UDSelectOption -Name "Bulk Decisions$Page:TickedCount" -Value "Bulk Decisions"
        New-UDSelectOption -Name 'Approve' -Value 'Approve'
        New-UDSelectOption -Name 'Revoke' -Value 'Revoke'
    } -OnChange {
        $Choice = $EventData
        $DecisionBit = if ($Choice -eq 'Approve') { 1 } else { 0 }
        $Selected = $Session:Selections
        # Show-UDToast ('{0}' -f $Session:Selections | Out-String) -Persistent
        foreach ($Row in $Selected) {
            $Query = @"
                UPDATE Certificates
                SET Decision = $DecisionBit
                WHERE CertificateId = $Row;
"@
            Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -Query $Query
        }
        Start-Sleep -Seconds 1
        $Page:TickedCount = ''
        $Session:Selection = @()
        Sync-UDElement -Id 'DropDownDynamic'
        Sync-UDElement -Id 'DynamicTable'
    }
}
```

### Demo

Below is a demo of this app.&#x20;

{% embed url="https://youtu.be/gfg_MHxKFUk" %}
Demo of SQL Data Grid
{% endembed %}

### Complete Example

The entire implementation of the app can be found below.&#x20;

```powershell
New-UDApp -Content {

    $Session:Selections = @()
    #endregion ID Verification and Database Connection
    #region Button and Chip Values and Styles
    $Session:SaveBtnClickedFromOpen = $false
    $Session:SaveBtnClickedFromReview = $false

    $Session:ChipLabelUnderOpen = ''
    $Session:ChipLabelUnderReview = ''

    # White
    $Page:BtnWhiteApprove = @{'background-color' = '#FFFFFF'; 'color' = '#717171'; Width = "90px"; Height = "28px"; 'margin-left' = '0px'; 'margin-right' = '2px' }
    $Page:BtnWhiteRevoke = @{'background-color' = '#FFFFFF'; 'color' = '#717171'; Width = "90px"; Height = "28px"; 'margin-left' = '2px'; 'margin-right' = '0px' }

    # Green
    $Page:BtnGreenApprove = @{'background-color' = '#00842b'; 'color' = '#FFFFFF'; Width = "90px"; Height = "28px"; 'margin-left' = '0px'; 'margin-right' = '2px' }

    # Red
    $Page:BtnRedRevoke = @{'background-color' = '#EB0A1E'; 'color' = '#FFFFFF'; Width = "90px"; Height = "28px"; 'margin-left' = '2px'; 'margin-right' = '0px' }

    # Modal
    $Page:BtnWhiteModal = @{'background-color' = '#FFFFFF'; 'color' = '#717171'; Width = "10px"; Height = "28px"; 'margin-left' = '5px'; 'margin-right' = '0px'; 'min-width' = '10px' }

    $Page:IconModal = New-UDIcon -Icon 'bars' -Color '#717171' -Title 'Approve' -Solid

    $Page:IconApproveNeutral = New-UDIcon -Icon 'thumbs-up' -Color '#717171' -Title 'Approve' -Solid
    $Page:IconApprove = New-UDIcon -Icon 'thumbs-up' -Color '#FFFFFF' -Title 'Approve' -Solid

    $Page:IconRevokeNeutral = New-UDIcon -Icon 'thumbs-down' -Color '#717171' -Title 'Revoke' -Solid
    $Page:IconRevoke = New-UDIcon -Icon 'thumbs-down' -Color '#FFFFFF' -Title 'Revoke' -Solid

    $Page:TextApprove = 'Approve'
    $Page:TextRevoke = 'Revoke'

    #endregion Button and Chip Values and Styles
    #region CSS Styles
    New-UDHtml -Markup '<style>
.my-custom-tabs .MuiTab-root {
    width: 100px;  /* Fixed width */
    text-align: center; /* Center text */
    height: 48px;  /* Fixed height */
    margin-top: -10px;  /* Move text upwards on the page */
}
.my-custom-tabs .MuiTab-root.Mui-selected {
    background-color: #FFFFFF;
    color: #1f2328;
    font-weight: bold;
}
.my-custom-tabs .css-7mcwe1-MuiTabs-indicator {
    background-color: #EB0A1E;
}
.css-nmu7bk-MuiTableRow-root,
.css-1gjuw6o-MuiTableRow-root {
    vertical-align: baseline !important;
}
.my-badge-container {
    position: relative;
    display: flex;
    align-items: center;
}
.my-chip-open {
    position: absolute;
    top: 119px;
    left: 75px;
    z-index: 1000;
    color: #FFFFFF;
    background-color: #666666;
    width: 52px;  /* Fixed width */
    height: 15px;
    text-align: center;  /* Center the text horizontally */
    font-size: 10px;     /* Adjusted font size */
    font-weight: bold;   /* Set font weight to bold */
}
.my-chip-review {
    position: absolute;
    top: 119px;
    left: 174px;
    z-index: 1000;
    color: #FFFFFF;
    background-color: #666666;
    width: 52px;  /* Fixed width */
    height: 15px;
    text-align: center;  /* Center the text horizontally */
    font-size: 10px;     /* Adjusted font size */
    font-weight: bold;   /* Set font weight to bold */
}
</style>'



    #endregion CSS Styles
    # Adding line breaks to push the content down
    New-UDHtml -Markup '<br><br>'
    #region Grid Container (1) Wraps all code
    New-UDGrid -Container -Content {
        New-UDPaper -Elevation 1 -Content {
            #endregion Grid Container (1) Wraps all code
            #region Grid Item (1.1) Tabs
            New-UDGrid -Item -ExtraSmallSize 12 -Content {
                #endregion Grid Item (1.1) Tabs
                New-UDHtml -Markup '<div class="my-badge-container">'  # Open container div
                #region Grid Container (2) Dropdown and Button
                New-UDGrid -Container -Content {
                    New-UDPaper -Elevation 1  -Content {
                        #endregion Grid Item (2) Dropdown and Button
                        #region Grid Item (2.1) Dropdown and Button
                        New-UDGrid -Item -ExtraSmallSize 3 -Content {
                            #endregion Grid Item (2.1) Dropdown and Button
                            #region Dropdown Select
                            New-UDDynamic -Id "DropDownDynamic" {
                                New-UDSelect -Id 'DropDown' -DefaultValue 'Bulk Decisions' -Option {
                                    New-UDSelectOption -Name "Bulk Decisions$Page:TickedCount" -Value "Bulk Decisions"
                                    New-UDSelectOption -Name 'Approve' -Value 'Approve'
                                    New-UDSelectOption -Name 'Revoke' -Value 'Revoke'
                                } -OnChange {
                                    $Choice = $EventData
                                    $DecisionBit = if ($Choice -eq 'Approve') { 1 } else { 0 }
                                    $Selected = $Session:Selections
                                    # Show-UDToast ('{0}' -f $Session:Selections | Out-String) -Persistent
                                    foreach ($Row in $Selected) {
                                        $Query = @"
                                            UPDATE Certificates
                                            SET Decision = $DecisionBit
                                            WHERE CertificateId = $Row;
"@
                                        Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -Query $Query
                                    }
                                    Start-Sleep -Seconds 1
                                    $Page:TickedCount = ''
                                    $Session:Selection = @()
                                    Sync-UDElement -Id 'DropDownDynamic'
                                    Sync-UDElement -Id 'DynamicTable'
                                }
                            }
                        }
                        #endregion Dropdown Select
                    }
                }
                #region Grid Container (3) Table
                New-UDGrid -Container -Content {
                    #endregion Grid Container (3) Table
                    #region Grid Item (3.1) Table
                    New-UDGrid -Item -ExtraSmallSize 12 -Content {
                        New-UDPaper -Elevation 1  -Content {
                            #endregion Grid Item (3.1) Table
                            #region Table + Filter and Sorts
                            New-UDDynamic -Id "DynamicTable" {
                                New-UDDataGrid -ShowPagination -PageSize 10 -RowsPerPageOptions @(10, 25, 50, 100, 200) -CheckboxSelection -LoadRows {

                                    function ConvertTo-ProperCase {
                                        param($Field)

                                        switch ($Field) {
                                            "username" { "UserName" }
                                            "groupname" { "GroupName" }
                                        }
                                    }

                                    $Context = $EventData

                                    $SqlFilter = ""
                                    if ($Context.Filter.Items.Count -gt 0) {
                                        $count = 1
                                        foreach ($filter in $Context.Filter.Items) {
                                            if ($count -gt 1) {
                                                $SqlFilter += " $($Context.Filter.logicOperator) "
                                            }
                                            else {
                                                $SqlFilter += " WHERE "
                                            }
                                            switch ($filter.Operator) {
                                                "contains" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) LIKE '%$($filter.Value)%' " }
                                                "equals" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) = '$($filter.Value)' " }
                                                "startsWith" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) LIKE '$($filter.Value)%' " }
                                                "endsWith" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) LIKE '%$($filter.Value)' " }
                                                "isAnyOf" {
                                                    $count = 1
                                                    foreach ($val in $filter.Value) {
                                                        if ($count -gt 1) {
                                                            $list += ", '$val'"
                                                        }
                                                        else {
                                                            $list += "'$val'"
                                                        }  
                                                        $count += 1
                                                    }
                                                    $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) IN ($($list)) "
                                                }
                                                "isempty" { $SqlFilter += " TRIM ($(ConvertTo-ProperCase $filter.Field)) IS NULL " }
                                                "isnotempty" { $SqlFilter += " TRIM ($(ConvertTo-ProperCase $filter.Field)) IS NOT NULL " }
                                                "notequals" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) != '$($filter.Value)' " }
                                                "notcontains" { $SqlFilter += " $(ConvertTo-ProperCase $filter.Field) NOT LIKE '%$($filter.Value)%' " }
                                            }
                                            $count += 1
                                        }
                                    }

                                    $PageSize = $Context.PageSize
                                    # Calculate the number of rows to skip
                                    $Offset = $Context.Page * $PageSize

                                    #endregion Table + Filter and Sorts
                                    #region Create Table Query Herestring
                                    $Query = @"
                                    SELECT
                                        CertificateId,
                                        CertificateId as id,
                                        Decision,
                                        GroupName,
                                        UserName,
                                        AppName
                                    FROM 
                                        dbo.Certificates
"@
                                    #endregion Create Table Query Herestring                                 
                                    #region Table Construct Database Query with `Where`, `Paging`, and `Count`

                                    if ($Context.Sort[0].field -ne $null) {
                                        $sqlSort = "ORDER BY $(ConvertTo-ProperCase $Context.Sort[0].field) $($Context.Sort[0].sort) "
                                    }
                                    else {
                                        $sqlSort = "ORDER BY (SELECT NULL)"
                                    }

                                    $sqlPage = "OFFSET $Offset ROWS FETCH NEXT $($Context.PageSize) ROWS ONLY;"

                                    $Query = '{0} {1}' -f $Query, "$SqlFilter $sqlSort $sqlPage"
                                    $Count = Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -As SingleValue -Query "SELECT COUNT(*) as count FROM dbo.Certificates $SqlFilter"

                                    Show-UDToast $Query -Persistent
                                    #endregion Table Construct Database Query with `Where's` and `Paging`
                                    #region Query the Database and Pass `$Session:Data` to Out-UDTableData
                                    $Session:Data = Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -As PSObjectArray -Query $Query

                                    @{
                                        rows     = [Array]$Session:Data
                                        rowCount = $Count
                                    }
                                    #endregion Query the Datbase and Pass `$Session:Data` to Out-UDTableData
                                    #region Table Columns
                                } -Columns @(
                                    New-UDDataGridColumn -HeaderName 'User' -Field 'UserName' -Filterable -Sortable -Description 'UserName'
                                    New-UDDataGridColumn -HeaderName 'Group' -Field 'GroupName'  -Filterable -Sortable
                                    New-UDDataGridColumn -HeaderName 'App' -Field 'AppName' -Filterable -Sortable
                                    New-UDDataGridColumn -HeaderName 'Decision' -Field 'Decision' -MinWidth 300 -Render { 
                                        New-UDDynamic -Id $EventData.CertificateId -Content {

                                            function New-DecisionButton {
                                                param(
                                                    $Text,
                                                    $Icon,
                                                    $Style,
                                                    $CertificateId,
                                                    $Decision
                                                )

                                                New-UDButton -Text $Text -Icon $Icon -Style $Style -OnClick {
                                                    $Session:updateButton = $true
                                                    $Query = @"
                                                UPDATE Certificates
                                                SET Decision = $Decision
                                                WHERE CertificateId = $CertificateId;
"@

                                                    Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -Query $Query
                                                    Sync-UDElement -Id $CertificateId
                                                } -ShowLoading
                                            }

                                            if ($Session:updateButton) {
                                                $item = Invoke-DbaQuery -SqlInstance '(localdb)\MSSQLLocalDB' -Database PSU -Query ('SELECT * FROM [dbo].[Certificates] WHERE CertificateId = {0}' -f $EventData.CertificateId)
                                                $EventData.Decision = $item.Decision
                                                $Session:updateButton = $false
                                            }

                                            if ($EventData.Decision -eq 1) {
                                                New-DecisionButton -Text 'Approve' -Icon $Page:IconApprove -Style $Page:BtnGreenApprove -CertificateId $EventData.CertificateId -Decision 'NULL'
                                                New-DecisionButton -Text 'Revoke' -Icon $Page:IconRevokeNeutral -Style $Page:BtnWhiteRevoke -CertificateId $EventData.CertificateId -Decision '0'
                                            }
                                            elseif ($EventData.Decision -eq 0) {
                                                New-DecisionButton -Text 'Approve' -Icon $Page:IconApproveNeutral -Style $Page:BtnWhiteApprove -CertificateId $EventData.CertificateId -Decision '1'
                                                New-DecisionButton -Text 'Revoke' -Icon $Page:IconRevoke -Style $Page:BtnRedRevoke -CertificateId $EventData.CertificateId -Decision 'NULL'
                                            }
                                            else {
                                                New-DecisionButton -Text 'Approve' -Icon $Page:IconApproveNeutral -Style $Page:BtnWhiteApprove -CertificateId $EventData.CertificateId -Decision '1'
                                                New-DecisionButton -Text 'Revoke' -Icon $Page:IconRevokeNeutral -Style $Page:BtnWhiteRevoke -CertificateId $EventData.CertificateId -Decision '0'
                                            }
                                        }
                                    }
                                    #region Table OnRowSelection
                                ) -OnSelectionChange {
                                    $Session:Selections = $EventData
                                    if ($Session:Selections.Count -le 0) {
                                        $Page:TickedCount = ''    
                                    }
                                    else {
                                        $Page:TickedCount = ' ({0})' -f $Session:Selections.Count
                                    }                
                                    Sync-UDElement -Id 'DropDownDynamic'
                                } 
                            }
                        }
                    }
                }
                #endregion Table OnRowSelection
            }
        }
    }

}
```
