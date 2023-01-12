# Deploying Kiosk application

## Deploying for one kiosk in one PC
1. Download a copy of this repository
2. Copy the file to the target PC
3. Run `Install.ps1` file on the target PC
4. Setup the application to run on startup by setting up Assigned Access https://learn.microsoft.com/en-us/windows/configuration/kiosk-single-app#local

## Deploying for multiple kiosks in one PC
1. Upgrade the PC to Enterprise or Education edition. This is required to use the ShellLauncherV2
2. Turn on the Shell Launcher optional component
3. Download the scripts and files in this folder to your PC
4. Download SysInternals tools, run "psexec.exe -i -s powershell.exe" from elevated command prompt
5. Open the `PayrollShellLauncherConfiguration.xml` file
6. For each user accounts that is going to be used to host the kiosk application, there should be one Profile and Config element in the XML file.
    1. Copy and paste the existing `Profile` element that has Payroll as its Shell, and make sure that each `Profile` has a unique Id attribute.
    2. For each  `Config` element, the `Account Name` attribute should be the name of the user account, and the `Profile Id` attribute should map to the Ids that is used on the `Profiles` element.
7. In the powershell launched by psexec.exe, first import the scripts, notice the . command when importing the ps1 file
```
PS C:\Users\test> . .\ShellLauncherBridgeWmiHelpers.ps1
```
8. After importing, run the command Set-ShellLauncherBridgeWMI with FilePath pointing to a shell launcher config xml
```
PS C:\Users\test> Set-ShellLauncherBridgeWmi -FilePath .\PayrollShellLauncherConfiguration.xml
```
9. To remove the kiosk configuration from the PC, run the other command Clear-ShellLauncherBridgeWMI

```
PS C:\Users\test> Clear-ShellLauncherBridgeWmi
```
10. On the kiosk app installation package, replace the `Add-AppDevPackage.ps1` file with the one in this folder. This will make sure that the kiosk app is installed for all users.
11. Run `Install.ps1` file on the target PC

## Extra reading
1. Assigned Access: https://docs.microsoft.com/en-us/windows/configuration/kiosk-single-app#local
2. ShellLauncher: https://learn.microsoft.com/en-us/windows-hardware/customize/enterprise/shell-launcher
3. ShellLauncher v2: https://learn.microsoft.com/en-us/windows/configuration/kiosk-shelllauncher
4. ShellLauncher v2 Script and configuration: https://github.com/microsoft/Windows-iotcore-samples/tree/develop/Samples/ShellLauncherV2
