**Task 1: Use PowerShell to create a user account for Isabel Garcia.**

1. Open the Cloud Shell by clicking the Cloud Shell icon in the top-right corner of the Azure portal.
2. If prompted, select No storage account required, select the name of your subscription, and then select Apply. This is required only the first time you launch the Cloud Shell. <img width="1430" height="771" alt="image" src="https://github.com/user-attachments/assets/eb70442b-7b30-4669-86f7-edc5cf6103f3" />
3. In the PowerShell session within the Cloud Shell pane, run the following to create a password profile object: ```$passwordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile```
4. In the PowerShell session within the Cloud Shell pane, run the following to set the value of the password within the profile object: ```$passwordProfile.Password = "Pa55w.rd1234"```
5. In the PowerShell session within the Cloud Shell pane, run the following to connect to Microsoft Entra ID: ```Connect-AzureAD```
6. In the PowerShell session within the Cloud Shell pane, run the following to identify the name of your Microsoft Entra tenant: ```$domainName = ((Get-AzureAdTenantDetail).VerifiedDomains)[0].Name```
7. In the PowerShell session within the Cloud Shell pane, run the following to create a user account for Isabel Garcia: ```New-AzureADUser -DisplayName 'Isabel Garcia' -PasswordProfile $passwordProfile -UserPrincipalName "Isabel@$domainName" -AccountEnabled $true -MailNickName 'Isabel'```
8. In the PowerShell session within the Cloud Shell pane, run the following to list Microsoft Entra ID users (the accounts of Joseph and Isabel should appear on the listed): ```Get-AzureADUser -All $true | Where-Object {$_.UserPrincipalName -like "Isabel-65001729*"} ```
<img width="1919" height="886" alt="image" src="https://github.com/user-attachments/assets/50d68c0b-11e1-4260-bf6a-068a474cd12a" />

**Task 2: Use PowerShell to create the Junior Admins group and add the user account of Isabel Garcia to the group.**

1. In the same PowerShell session within the Cloud Shell pane, run the following to create a new security group named Junior Admins: ```New-AzureADGroup -DisplayName 'Junior Admins65001729' -MailEnabled $false -SecurityEnabled $true -MailNickName JuniorAdmins```
2. In the PowerShell session within the Cloud Shell pane, run the following to list groups in your Microsoft Entra tenant (the list should include the Senior Admins65001729 and Junior Admins groups) ```Get-AzureADGroup```
3. In the PowerShell session within the Cloud Shell pane, run the following to obtain a reference to the user account of Isabel Garcia: ```$user = Get-AzureADUser -Filter "UserPrincipalName eq 'Isabel-65001729@LODSPRODMSLEARNMCA.onmicrosoft.com'"```
4. In the PowerShell session within the Cloud Shell pane, run the following to add the user account of Isabel to the Junior Admins65001729 group: ```Add-AzADGroupMember -MemberUserPrincipalName $user.userPrincipalName -TargetGroupDisplayName "Junior Admins65001729"```
5. In the PowerShell session within the Cloud Shell pane, run the following to verify that the Junior Admins65001729 group contains the user account of Isabel: ```Get-AzADGroupMember -GroupDisplayName "Junior Admins65001729"```
<img width="1919" height="886" alt="image" src="https://github.com/user-attachments/assets/7a501025-dc0a-45ea-b3d7-f7aa9635af46" />

