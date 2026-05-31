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

## Step 1 - Prepare the CSV File

Create a CSV file that contains the information needed to create the 10 new user accounts.

 FirstName LastName  DisplayName        UserPrincipalName                       MailNickname   Department JobTitle     UsageLocation  Password
  Williams  Kesse    Williams Kesse  williamskesse@Williams016.onmicrosoft.com   williams.kesse  Finance    IT Support   DE            P@ssw0rd123!

