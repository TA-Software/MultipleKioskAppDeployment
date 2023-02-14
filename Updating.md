# Updating Payroll
Use the following steps to update the Payroll application on a kiosk.

## Single Kiosk
1. Remove Assigned Access from the account
2. Sign in into the account
3. Install the update by running the `msixbundle` file
4. Enable assigned access for the account

## Multiple Kiosks
1. Logout from all accounts on the PC
2. Login to the PC as a local administrator
3. Download a copy of the application package and this repository
4. Replace the `Add-AppDevPackage.ps1` inside the package and replace it with a copy from this repository
5. Run `Install.ps1` from the package. 
