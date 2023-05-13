Following method worked on a Windows 7 computer

### Step 1: PowerShell Script
Following is the powershell script ([original source](https://superuser.com/questions/39584/what-is-the-command-to-use-to-put-your-computer-to-sleep-not-hibernate)) for making computer to sleep:  
<code>Add-Type -Assembly System.Windows.Forms
[System.Windows.Forms.Application]::SetSuspendState("Suspend", $false, $true)
</code>

Open notepad and copy the above text. Save it as _Sleep.ps1_ somewhere on your Desktop.  

**Note:** If you right click on the file and choose "Run with PowerShell", it will put your computer to sleep. But that's two clicks and we want a single-click solution!  

### Step 2: Install PS2EXE Module  
Run PowerShell as administrator.  
Run the following command to download and install it from the PowerShell Gallery:  
<code>Install-Module ps2exe</code>  

**Note:** when trying the above command, it asked for NuGet provider and threw an error that it was unable to download from URI...  
This error had something to do with the security protocol ([original source](https://stackoverflow.com/questions/51406685/powershell-how-do-i-install-the-nuget-provider-for-powershell-on-a-unconnected)).  
Check current security protocol:  
<code>[Net.ServicePointManager]::SecurityProtocol</code>, which showed _Ssl3, Tls_  
We need _Tls12_. To do this, run in PS  
<code>[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12</code>  
Run the previous command and you should see _Tls12_ instead of _Ssl3, Tls_  
Run the <code>Install-Module ps2exe</code> command and it should work.  

### Step 3: Convert Powershell script to EXE file 
[original source](https://www.youtube.com/watch?v=PtFFtY1zxPE)  
- Download a graphical user interface utility called **Win-PS2EXE.exe** file from the MScholtes/PS2EXE GitHub [page](https://github.com/MScholtes/PS2EXE/blob/master/Module/Win-PS2EXE.exe).  
- Download an appropriate "Sleeping" icon file (.ico) from the iconarchive website.  
- Run the Win-PS2EXE.exe GUI. Select the Sleep.ps1 file from step 1 as source, select Desktop as the target and select the icon file.  
Check options for "suppress output" and "suppress error output" and it will generate a Sleep.exe file on the Desktop.  
- Dock it to your Taskbar by dragging it over. Click on it to put your computer to sleep with a single click Zzzz...  

### Notes
Many errors were encountered on the way. Here is how I fixed them:  

1. To execute PS scripts, changed the Execution policy using PowerShell
<code>Get-ExecutionPolicy</code>
showed Restricted, which means all scripts are blocked from running. Changed this to RemoteSigned by running:
<code>Set-ExecutionPolicy RemoteSigned</code>

2. Before running step 2, I needed to upgrade my PowerShell, which was version 2, to version 5.1 (Instructions [here](https://giritharan.com/install-the-latest-powershell-on-windows-7/)).  
First, check the current PS version with <code>$PSVersionTable</code> or <code>$PSVersionTable.PSVersion</code> or <code>Get-Host | Select-Object Version</code>  
Download the latest Windows Management Framework from the Microsoft site - Win7AndW2K8R2-KB3191566-x64.zip, which is for a 64 bit computer. Unzip it and you will see the following two files:  
![image](https://github.com/ved-sharma/Sleep-computer-with-a-single-click/assets/39934015/0643df15-d6d6-43bc-b6da-6749b24befbd)  
Run the powershell script _Install-WMF5.1.ps1_ file on PS prompt.  

