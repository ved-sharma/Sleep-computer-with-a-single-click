Following method worked on a Windows 7 computer

### Step 1: Script
Following is the powershell script ([original source](https://superuser.com/questions/39584/what-is-the-command-to-use-to-put-your-computer-to-sleep-not-hibernate)) for making computer to sleep
<code>Add-Type -Assembly System.Windows.Forms
[System.Windows.Forms.Application]::SetSuspendState("Suspend", $false, $true)
</code>

Open notepad and copy the above text and save it as Sleep.ps1 somewhere on your computer.

Note: If you write click on the file and choose "Run with PowerShell", it will put your computer to sleep

### Install PS2EXE Module  
Run PowerShell as administrator  
Run the Install-Module command to download and install the module from the PowerShell Gallery
<code>Install-Module ps2exe</code>  

### Step 3: Comvert Powershell script to EXE file 
[original source](https://www.youtube.com/watch?v=PtFFtY1zxPE)  
Download a graphical user interface utility called **Win-PS2EXE.exe** file from the MScholtes/PS2EXE GitHub [page](https://github.com/MScholtes/PS2EXE/blob/master/Module/Win-PS2EXE.exe)  
Download an appropriate "Sleeping" icon .ico file from iconarchive website  
Run the Win-PS2EXE.exe GUI. Select the Sleep.ps1 file from step 1 as source, select desktop as the target and select the icon file.  
Check options for "suppress output" and "suppress error output" and it will generate a Sleep.exe file on the Desktop.  
Dock it to your taskbar by dragging it over. Click on it to put your computer to sleep Zzzz...  



### Notes
Many errors were encountered on the way and here are the ways I fixed them:  
1. Needed to upgrade my PowerShell, which was version 2, to version 5.1 by following the instructions at:

2. Opened Powershell as administrator  

3. To execute PS scripts, changed the Execution policy using PowerShell
<code>Get-ExecutionPolicy</code>
showed Restricted, which means all scripts are blocked from running. Changed this to RemoteSigned by running:
<code>Set-ExecutionPolicy RemoteSigned</code>

4. In step 2, when trying "Install-Module ps2exe" on PS, it was asking for NuGet provider and throwing and wrro that it was unable to download from URI...  
It has something to do with the security protocol. I checked it using:  
<code>[Net.ServicePointManager]::SecurityProtocol</code>, which showed Ssl3, Tls  
We need Tls12. To do this, run in PS 
<code>[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12</code>  
Run the above previous command and you should see Tls12 instaed of Ssl3, Tls  
