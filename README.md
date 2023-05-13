Following method was tested on a Windows 7 computer with 

### Step 1: script for 
Following is the powershell script ([original source](https://superuser.com/questions/39584/what-is-the-command-to-use-to-put-your-computer-to-sleep-not-hibernate)) for making computer to sleep
<code>Add-Type -Assembly System.Windows.Forms
[System.Windows.Forms.Application]::SetSuspendState("Suspend", $false, $true)
</code>

Open notepad and copy the above text and save it as Sleep.ps1 somewhere on your computer.

Note: If you write click on the file and choose "Run with PowerShell", it will put your computer to sleep

### Comvert Powershell script to EXE file for single click 

### Notes
Needed to upgrade my PowerShell, which was version 2, to version 5.1 by following the instructions at:
Opened Powershell as administrattor  
To execute PS scripts, changed the Execution policy using PowerShell
<code>Get-ExecutionPolicy</code>
showed Restricted, which means all scripts are blocked from running. Changed this to RemoteSigned by running:
<code>Set-ExecutionPolicy RemoteSigned</code>

