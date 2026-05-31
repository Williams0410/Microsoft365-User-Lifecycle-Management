# Microsoft365-User-Lifecycle-Management
Automating Microsoft 365 user onboarding and Self-Service Password Reset using Microsoft Graph PowerShell and Microsoft Entra ID.

# Microsoft 365 User Lifecycle Management & SSPR Deployment
## Overview

This project demonstrates how Microsoft 365 user onboarding was automated using Microsoft Graph PowerShell and how Self-Service Password Reset (SSPR) was deployed through Microsoft Entra ID.

## Business Scenario
The organization was onboarding 10 new employees and experiencing a high volume of password reset requests.
Manual account creation and password recovery were consuming significant IT resources and delaying user productivity.

## Objectives
- Automate user account creation
- Reduce onboarding time
- Assign users to department groups
- Configure shared mailboxes
- Deploy Self-Service Password Reset (SSPR)

 ## Technologies Used

- Microsoft 365
- Microsoft Entra ID
- Microsoft Graph PowerShell
- Exchange Online PowerShell
- PowerShell
- CSV Import

  ## Prerequisites

- Microsoft 365 Global Administrator account
- Microsoft Graph PowerShell SDK
- Exchange Online Management Module
- Microsoft Entra ID P1 License

  ## Solution Architecture / Workflow
  CSV File
    ↓
Microsoft Graph
    ↓
Create Users
    ↓
Assign Groups
    ↓
Assign Licenses
    ↓
Exchange Online
    ↓
Create Shared Mailboxes
    ↓
Microsoft Entra ID
    ↓
Configure SSPR

## Implementation Steps
## Step 1 - Connect to Microsoft Graph

Connect-MgGraph `
 -Scopes "User.ReadWrite.All","Group.ReadWrite.All"
 $users = Import-Csv "users.csv"

foreach ($user in $users) {
    New-MgUser ...
}


## Step 2 - Create Users 

  $users = Import- Csv "E:\DOCUMENT\PERSONAL COURSE\ITSA\users.csv" foreach ($user in $users)  
  {Check if user already exists  $existingUser = Get-MgUser -Filter "userPrincipalName eq '$($user. UserPrincipalName)'" 
  if (-not $existingUser) } { $PasswordProfile = @{ Password = $user. Password ForceChangePasswordNextSignIn = $true} try { 
  New-MgUser ` 
                -DisplayName "$($user. FirstName) $($user. LastName)" ` 

                -GivenName $user. FirstName ` 

                -Surname $user. LastName ` 

                -UserPrincipalName $user. UserPrincipalName ` 

                -MailNickname (($user. FirstName + $user. LastName). ToLower()) ` 

                -AccountEnabled:$true ` 

                -PasswordProfile $PasswordProfile 

            Write-Host "Created user:" $user. UserPrincipalName} 

        catch { 

            Write-Host "Failed to create:" $user. UserPrincipalName   }} 

    else {Write-Host "User already exists:" $user. UserPrincipalName}} 



## Step 3 - Create And Assign Groups and Licenses
    
 #Finance Group 
New-MgGroup -DisplayName "Finance" -MailEnabled:$false -MailNickname "Finance" -SecurityEnabled:$true 
 #Business Intelligence Group 

New-MgGroup -DisplayName "Business Intelligence" -MailEnabled:$false -MailNickname "BusinessIntelligence" -SecurityEnabled:$true
Get-MgGroup | Select DisplayName 
if ($user.Department -eq "Finance") {
    $ExistingMember = Get-MgGroupMember -GroupId $FinanceGroup.Id |
        Where-Object Id -eq $MgUser.Id

    if (-not $ExistingMember) {
        New-MgGroupMember -GroupId $FinanceGroup.Id -DirectoryObjectId $MgUser.Id
        Write-Host "$($user.UserPrincipalName) added to Finance"}
    else {
        Write-Host "$($user.UserPrincipalName) already in Finance"}}
elseif ($user.Department -eq "Business Intelligence") {
    $ExistingMember = Get-MgGroupMember -GroupId $BIGroup.Id |
        Where-Object Id -eq $MgUser.Id
        
  if (-not $ExistingMember) {
        New-MgGroupMember -GroupId $BIGroup.Id -DirectoryObjectId $MgUser.Id
        Write-Host "$($user.UserPrincipalName) added to Business Intelligence"}
    else {Write-Host "$($user.UserPrincipalName) already in Business Intelligence"}
    }

 ## Configure Shared Mailboxes
Connect-ExchangeOnline 

# Finance
New-Mailbox ` 
-Shared ` 
-Name "Finance Shared Mailbox" ` 
-DisplayName "Finance Shared Mailbox" ` 
-PrimarySmtpAddress finance@Williams016.onmicrosoft.com

# Business Intelligence
New-Mailbox ` 
-Shared ` 
-Name "BI Shared Mailbox" ` 
-DisplayName "Business Intelligence Shared Mailbox" ` 
-PrimarySmtpAddress bi@Williams016.onmicrosoft.com , 
Get-Mailbox -RecipientTypeDetails SharedMailbox 
