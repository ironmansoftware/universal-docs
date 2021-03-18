---
description: Hyper-V examples for PowerShell Universal.
---

# Hyper-V

## Virtual Machine Creator

This example uses [PowerShell Universal Dashboard](../dashboard/about.md). 

This example can be used to create virtual machines on a Hyper-V host. This dashboard assumes it's being run on the host in question. You could adjust the dashboard script to run on a remote host. 

```PowerShell
Start-PSUServer -Port 8080 -Configuration {
    New-PSUDashboard -Name 'Hyper-V' -BaseUrl '/' -Framework 'UniversalDashboard:Latest' -Content {
  
        $HostRam = Get-WMIObject -class Win32_PhysicalMemory | Measure-Object -Property capacity -Sum | % {[Math]::Round(($_.sum / 1GB *0.97),0)-1}
        $HostName=hostname
        $SwitchList = @()
        Get-VMSwitch | Select-Object -ExpandProperty name | ForEach-Object {
            $SwitchList += $_
        }
        
        function Run-Checks
        {
            $VMHostInfo= Get-VMHost
        
            $BootISOTextBoxText = (Get-UDElement -Id 'VMBootISO')['value']
            $VHDRootTextBoxText = (Get-UDElement -Id 'VMVHDRoot')['value']
            $VMNameTextBoxText = (Get-UDElement -Id 'VMName')['value']
            $Generation = (Get-UDElement -Id 'VMGeneration')['value']
            $SwitchNameComboBoxText = (Get-UDElement -Id 'VMSwitch')['value']
            $RAMinGBTextBoxText = (Get-UDElement -Id 'VMRam')['value']
            $CPUCountTextBoxText = (Get-UDElement -Id 'VMCPU')['value']
            [int64]$VLANIDTextBoxText = (Get-UDElement -Id 'VMVLan')['value']
        
            #Paths and Gen Sets    
            if ($BootISOTextBoxText -and $BootISOTextBoxText -ne "") {$ISOFilePathValid = test-path $BootISOTextBoxText}
            if ($VHDRootTextBoxText -and $VHDRootTextBoxText -ne "") {$VHDBootPathValid = test-path $VHDRootTextBoxText}
            if ($Generation -eq 'Gen1') { $VMGeneration = 1 } else { $VMGeneration = 2 } 
        
            if ($VMNameTextBoxText.Length -ne 0) { $VMExists = Get-VM -name $VMNameTextBoxText -ErrorAction SilentlyContinue }
        
            if (-not (Test-Path $VMHostInfo.VirtualMachinePath) ) {Show-UDToast -Message  "Default Virtual Machine path is not valid in HyperV Host Settings"}
            elseif (-not (Test-Path $VMHostInfo.VirtualHardDiskPath) ) {Show-UDToast -Message  "Default Virtual Harddisk path is not valid in HyperV Host Settings"}
            elseif ($VMExists) {Show-UDToast -Message  "VM with that name already exists"}
            elseif ($VMNameTextBoxText.Length -eq 0) {Show-UDToast -Message  "Please Enter VM Name"}
            elseif ($SwitchNameComboBoxText -eq "Switch Name") {Show-UDToast -Message  "Please Select a Switch Name"}
            elseif ($ISOFilePathValid -eq $False) {Show-UDToast -Message  "ISO File path in invaild"}
            elseif ($VHDRootTextBoxText -eq "") {Show-UDToast -Message  "VHD Root path is blank.  Please enter a valid path"}
            elseif ($VHDBootPathValid -eq $False) {Show-UDToast -Message  "VHD Root path in invaild"}
            elseif ($RAMinGBTextBoxText.Length -eq 0) {Show-UDToast -Message  "Please Enter Ram Amount in GB"}
            elseif ([int64]$RAMinGBTextBoxText -lt 1) {Show-UDToast -Message  "Please Enter Ram Amount of at least 1GB"}
            elseif ([int64]$RAMinGBTextBoxText -gt $HostRam) {Show-UDToast -Message  "Please Enter Ram Amount of "+ $HostRam + "GB or bellow"}
            elseif ($CPUCountTextBoxText.Length -eq 0) {Show-UDToast -Message  "Please Enter a CPU Count"}
            elseif ([int64]$CPUCountTextBoxText.Length -eq 0) {Show-UDToast -Message  "Please Enter a CPU Count"}
            elseif ([int64]$CPUCountTextBoxText -lt 1) {Show-UDToast -Message  "Please Enter a CPU Count of at least 1"}
            elseif ([int64]$CPUCountTextBoxText -gt 64) {Show-UDToast -Message  "Please Enter a CPU Count of 64 or below"}
            elseif ([int64]$VLANIDTextBoxText -gt 999 -or [int64]$VLANIDTextBoxText -lt 1) {Show-UDToast -Message  "Please Enter VLAN ID between 1 and 999."}
            else 
            {
                (65..90) | ForEach-Object { 
                    $DriveLetter = [char]$_  
        
                    [int64]$value = (Get-UDElement -Id "Drive$DriveLetter")['value']
        
                    if ($value -gt 65536)
                    {
                        Show-UDToast -Message  "For $DriveLetter Drive please Enter a Disk Size of 65536 GB or below"
                        return $false
                    }
                } 
        
                Show-UDToast -Message  "Looking Good Man ;)"
        
                return $true
            }
        
            return $false
        }
        
        function Create-VMs
        {
            Run-Checks
        
            $BootISOTextBoxText = (Get-UDElement -Id 'VMBootISO')['value']
            $VHDRootTextBoxText = (Get-UDElement -Id 'VMVHDRoot')['value']
            $VMNameTextBoxText = (Get-UDElement -Id 'VMName')['value']
            $Generation = (Get-UDElement -Id 'VMGeneration')['value']
            [int]$SwitchNameComboBoxIndex = (Get-UDElement -Id 'VMSwitch')['value']
            $SwitchNameComboBoxText = $SwitchList[$SwitchNameComboBoxIndex]
            Show-UDToast -message ((Get-UDElement -Id 'VMSwitch') | ConvertTo-Json)
            $RAMinGBTextBoxText = (Get-UDElement -Id 'VMRam')['value']
            $CPUCountTextBoxText = (Get-UDElement -Id 'VMCPU')['value']
            $VLANIDTextBoxText = (Get-UDElement -Id 'VMVLan')['value']
        
            if ($Generation -eq 'Gen1') { $VMGeneration = 1 } else { $VMGeneration = 2 } 
        
            #Create VM
        
            try
            {
                New-VM -Name $VMNameTextBoxText -MemoryStartupBytes ([int]$RAMinGBTextBoxText*1073741824) -SwitchName $SwitchNameComboBoxText -Generation $VMGeneration -ErrorAction Stop
            }
            catch
            {
                $VMCrateFailed=$True
                Show-UDToast -Message ("VM " + $VMNameTextBoxText + " Failed to Create :( $($_.Exception.Message)")
            }
        
        
            if (-Not($VMCrateFailed -eq $True))
            {
                (65..90) | ForEach-Object { 
                    $DriveLetter = [char]$_  
                    [int64]$value = (Get-UDElement -Id "Drive$DriveLetter")['value']
                    if ($value -gt 0)
                    {
                        $Path = $VHDRootTextBoxText+"\"+$VMNameTextBoxText+"\"+$VMNameTextBoxText+"-"+$value+".vhdx"
                        if (-not (test-path $Path)) 
                        {
                            New-VHD -Path $Path -SizeBytes (Invoke-Expression ("$($Value)GB")) -Dynamic
                        } 
                        else 
                        {
                            $VHDPathExisted = $true
                        }
                    }
                } 
        
            Get-VM $VMNameTextBoxText | Set-VMProcessor -Count $CPUCountTextBoxText
            Get-VM $VMNameTextBoxText | set-VMNetworkAdapterVlan -Access -vlanId $VLANIDTextBoxText
        
            (65..90) | ForEach-Object { 
                $DriveLetter = [char]$_  
                [int64]$value = (Get-UDElement -Id "Drive$DriveLetter")['value']
                $Path = $VHDRootTextBoxText+"\"+$VMNameTextBoxText+"\"+$VMNameTextBoxText+"-"+$value+".vhdx"
        
                if (Test-Path $Path)
                {
                    Add-VMHardDiskDrive -VMName $VMNameTextBoxText -Path $Path -ControllerType SCSI -ControllerNumber 0
                }
            } 
        
            # 
            #  REMOVING NETWORK FROM THE BOOT ORDER
        
            #Set New Boot order
            if ($VMGeneration -eq "2")
                {
                    $old_boot_order = Get-VMFirmware -VMName $VMNameTextBoxText -ComputerName $HostName | Select-Object -ExpandProperty BootOrder
                    $new_boot_order = $old_boot_order | Where-Object { $_.BootType -ne "Network" }
                    Set-VMFirmware -VMName $VMNameTextBoxText -ComputerName $HostName -BootOrder $new_boot_order
                }
        
        
            #  ADD DVD Drive with ISO Attached
            if ($BootISOTextBoxText -ne "")
            {
                Get-VM $VMNameTextBoxText | Add-VMDvdDrive -Path $BootISOTextBoxText
            }
        
            if ($VHDPathExisted) {
                Show-UDToast -Message ("VM " + $VMNameTextBoxText + " Created OK, but at least one VHD already existed and was just reattached")
            }
            else 
            {
                Show-UDToast -Message ("VM " + $VMNameTextBoxText + " Created OK")}
            }
        }
        
        
        New-UDDashboard -Title "Hyper-V VM Creator" -Content {
            New-UDContainer -Children {
                New-UDTypography -Text "Hyper-V VM Creator" -Variant h3 
        
                New-UDRow -Columns {
                    New-UDColumn -LargeSize 6 -Content {
                        New-UDRow -Columns {
                            New-UDTextbox -Label 'VM Name' -Id 'VMName'
                        }
                        New-UDRow -Columns {
                            New-UDTextbox -Id 'VMRam' -Label 'RAM in GB' -Value $HostRam
                        }
                        New-UDRow -Columns {
                            New-UDTextbox -Id 'VMCPU' -Label 'CPU Count' -Value 2
                        }
                    
                        New-UDRadioGroup -Label 'Generation' -Id 'VMGeneration' -Children {
                            New-UDRadio -Label 'Gen 1' -Value 'Gen1'
                            New-UDRadio -Label 'Gen 2' -Value 'Gen2'
                        } -Value 'Gen1'
                    }
                    New-UDColumn -LargeSize 6 -Content {
                        New-UDRow -Columns {
                            New-UDSelect -Id 'VMSwitch' -Label 'Switch Name' -Option {
                                $i = 0
                                $SwitchList | ForEach-Object {
                                    New-UDSelectOption -Value $i -Name $_
                                    $i++
                                }
                            }
                        }
                    
                        New-UDTextbox -Id 'VMVLan' -Label 'VLAN ID'
                    }
                }
        
                New-UDRow -Columns {
                    New-UDColumn -LargeSize 12 -Content {
                        New-UDTextbox -Id 'VMBootISO' -Label 'Boot ISO'
                    }
                }
        
                New-UDRow -Columns {
                    New-UDColumn -LargeSize 12 -Content {
                        New-UDTextbox -Id 'VMVHDRoot' -Label 'VHD Root'
                    }
                }
        
                New-UDTypography -Text 'Drives' -Variant h4
        
                New-UDRow -Columns {
                    New-UDColumn -LargeSize 6 -Content {
                        New-UDRow -Columns {
                            # Loop through each letter of the alphabet
                            (65..90) | ForEach-Object { 
                                New-UDColumn -LargeSize 6 -Content {
                                    $DriveLetter = [char]$_  
                                    New-UDTextbox -Id "Drive$DriveLetter" -Placeholder $DriveLetter
                                }
                            } 
                        }
                    }
                    New-UDColumn -LargeSize 6 -Content {
                        New-UDButton -Text 'Do Some Checks' -OnClick { Run-Checks }
                        New-UDButton -Text 'Im feeling lucky Create Vm' -OnClick { Create-VMs }
                    }
                }
            }
        }
    }

}
```

![](../.gitbook/assets/image%20%28203%29.png)

