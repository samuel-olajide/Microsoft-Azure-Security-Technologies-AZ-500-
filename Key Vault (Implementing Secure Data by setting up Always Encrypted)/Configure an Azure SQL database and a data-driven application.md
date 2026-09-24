# Task 1: Enable a client application to access the Azure SQL Database service.
> In this task, you will enable a client application to access the Azure SQL Database service. This will be done by setting up the required authentication and acquiring the Application ID and Secret that you will need to authenticate your application.

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type App Registrations and press the Enter key.
2. On the App Registrations blade, click + New registration.
3. On the Register an application blade, specify the following settings (leave all others with their default values):
   - Name	>> sqlApp
   - Redirect URI (optional)	>> Web and https://sqlapp
4. On the Register an application blade, click Register.
   > 🗒️Once the registration is completed, the browser will automatically redirect you to sqlApp blade.
5. On the sqlApp blade, identify the value of Application (client) ID.
   > 🗒️Record this value. You will need it in the next task.
<img width="1277" height="811" alt="image" src="https://github.com/user-attachments/assets/07a9dacd-f69e-4c0b-8161-e1049833da8b" />
6. On the sqlApp blade, in the Manage section, click Certificates & secrets.
7. On the sqlApp | Certificates & secrets blade / Client Secrets section, click + New client secret
8. In the Add a client secret pane, specify the following settings:
   - Description	>> Key1
   - Expires	>> 12 months
9. Click Add to update the application credentials.
10. On the sqlApp | Certificates & secrets blade, identify the value of Key1.
<img width="1267" height="748" alt="image" src="https://github.com/user-attachments/assets/331275ca-1ca4-4cbd-8a53-02134290b391" />
> 🗒️Record this value. You will need it in the next task.
> Make sure to copy the value before you navigate away from the blade. Once you do, it is no longer possible to retrieve its clear text value.

# Task 2: Create a policy allowing the application access to the Key Vault.
> In this task, you will grant the newly registered app permissions to access secrets stored in the Key Vault.

1. In the Azure portal, open a PowerShell session in the Cloud Shell pane.
2. Ensure PowerShell is selected in the upper-left drop-down menu of the Cloud Shell pane.
3. In the PowerShell session within the Cloud Shell pane, run the following to create a variable storing the Application (client) ID you recorded in the previous task (replace the (Azure_AD_Application_ID) placeholder with the value of the Application (client) ID): ```$applicationId = '<Azure_AD_Application_ID>'```
4. In the PowerShell session within the Cloud Shell pane, run the following to create a variable storing the Key Vault name.
  - ```$kvName = (Get-AzKeyVault -ResourceGroupName 'AZ500Lab10-lod65493277').VaultName```
  - ```$kvName```
5. In the PowerShell session within the Cloud Shell pane, run the following to grant permissions on the Key Vault to the application you registered in the previous task: ```Set-AZKeyVaultAccessPolicy -VaultName $kvName -ResourceGroupName AZ500Lab10-lod65493277 -ServicePrincipalName $applicationId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list```
6. Close the Cloud Shell pane.
<img width="1274" height="257" alt="image" src="https://github.com/user-attachments/assets/52888c5f-9c35-4e68-8c71-1cf0821f2bd4" />


# Task 3: Retrieve SQL Azure database ADO.NET Connection String
> The ARM-template deployment in Exercise 1 provisioned an Azure SQL Server instance and an Azure SQL database named medical . You will update the empty database resource with a new table structure and select data columns for encryption

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type SQL databases and press the Enter key.
2. In the list of SQL databases, click the medical() entry.
 <img width="1283" height="646" alt="image" src="https://github.com/user-attachments/assets/8c84344a-9367-4bf7-a58a-367f375ce18e" />
  > If the database cannot be found, this likely means the deployment you initiated in Exercise 1 has not completed yet. You can validate this by browsing to the Azure Resource Group "AZ500Lab10-lod65493277" (or the name you chose), and selecting Deployments from the Settings pane.
3. On the SQL database blade, in the Settings section, click Connection strings.
  > The interface includes connection strings for ADO.NET, JDBC, ODBC, PHP, and Go.
4. Record the ADO.NET (SQL authentication) connection string. You will need it later.
 <img width="1276" height="804" alt="image" src="https://github.com/user-attachments/assets/5387c35b-c127-412a-a9b5-264f022c0c08" />
  > When you use the connection string, make sure to replace the ```{your_password}``` placeholder with the password that you configured with the deployment in Exercise 1.

# Task 4: Log on to the Azure VM running Visual Studio 2019 and SQL Management Studio 19
> In this task, you log on to the Azure VM, which deployment you initiated in Exercise 1. This Azure VM hosts Visual Studio 2019 and SQL Server Management Studio 19.
  > 🗒️efore you proceed with this task, ensure that the deployment you initiated in the first exercise has completed successfully. You can validate this by navigating to the blade of the Azure resource group "AZ500Lab10-lod65493277" (or other name you chose) and selecting Deployments from the Settings pane.

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type virtual machines and press the Enter key.
2. In the list of Virtual Machines shown, select the az500-10-vm1 entry. On the az500-10-vm1 blade, on the Essentials pane, take note of the Public IP address. You will use this later.

# Task 5: Create a table in the SQL Database and select data columns for encryption
> In this task, you will connect to the SQL Database with SQL Server Management Studio and create a table. You will then encrypt two data columns using an autogenerated key from the Azure Key Vault.

1. In the Azure portal, navigate to the blade of the medical SQL database, in the Essentials section, identify the Server name (copy to clipboard), and then, in the toolbar, click Set server firewall.
    > Record the server name. You will need the server name later in this task.
2. On the Firewall settings blade, scroll down to Rule Name, click + Add a firewall rule, and specify the following settings: <br> <img width="1284" height="771" alt="image" src="https://github.com/user-attachments/assets/a8007afc-d70b-46b4-9bfe-af08aa5982f4" />
   - Rule Name	>> Allow Mgmt VM
   - Start IP >>	the Public IP Address of the az500-10-vm1
   - End IP	>> the Public IP Address of the az500-10-vm1
3. Click Save to save the change and close the confirmation pane.
    > This modifies the server firewall settings, allowing connections to the medical database from the Azure VM's public IP address you deployed in this lab.
4. Navigate back to the az500-10-vm1 blade, click Overview, next click Connect and, in the drop down menu, click Connect.
5. Download the RDP file and use it to connect to the az500-10-vm1 Azure VM via Remote Desktop. When prompted to authenticate, provide the following credentials:
   - Username	>> Student
   - Password	>> ```Please use your personal password created in Lab 02 > Exercise 1 > Task 1 > Step 9.```
    > Wait for the Remote Desktop session and Server Manager to load. Close Server Manager.
    > The remaining steps in this lab are performed within the Remote Desktop session to the az500-10-vm1 Azure VM.
6. Install ```https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017``` on az500-10-vm1. Azure VM.
7. Open SQL Server Management Studio.
8. In the Connect to Server dialog box, specify the following settings:
   - Server Type	>> Database Engine
   - Server Name	>> the server name you identified earlier in this task
   - Authentication >>	SQL Server Authentication
   - Username	>> Student
   - Password	>> ```Please use your personal password created in Lab 02 > Exercise 2 > Task 1 > Step 3.```
9. In the Connect to Server dialog box, click Connect.
10. Within the SQL Server Management Studio console, in the Object Explorer pane, expand the Databases folder.
11. In the Object Explorer pane, right-click the medical database and click New Query. > The medical database can be found in the menu.
12. Paste the following code into the query window and click Execute. This will create a Patients table.
    >CREATE TABLE [dbo].[Patients](
    >[PatientId] [int] IDENTITY(1,1),
    >[SSN] [char](11) NOT NULL,
    >[FirstName] [nvarchar](50) NULL,
    >[LastName] [nvarchar](50) NULL,
    >[MiddleName] [nvarchar](50) NULL,
    >[StreetAddress] [nvarchar](50) NULL,
    >[City] [nvarchar](50) NULL,
    >[ZipCode] [char](5) NULL,
    >[State] [char](2) NULL,
    >[BirthDate] [date] NOT NULL
    >PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
13. After the table is created successfully, in the Object Explorer pane, expand the medical database node, the tables node, right-click the dbo.Patients node, and click Always Encrypted wizard….
      > This will initiate the Always Encrypted wizard.
14. On the Introduction page, click Next.
15. On the Column Selection page, select the SSN and Birthdate columns, set the Encryption Type of the SSN column to Deterministic and of the Birthdate column to Randomized, and click Next.
      > While performing the encryption if any error thrown like Exception has been thrown by the target of an invocation related to Rotary(Microsoft.SQLServer.Management.ServiceManagement) then make sure the Key Permission's values of Rotation Policy Operations are unchecked, if not in the Azure portal navigate to the Key Vault >> Access Policies >> Key Permissions >> Uncheck all the values under the Rotation Policy Operations >> Under Privileged Key Operations >> Uncheck Release.
16. On the Master Key Configuration page, select Azure Key Vault, click Sign in. Make sure to only allow this App to sign in. When prompted, authenticate by using the same user account you used to provision the Azure Key Vault instance earlier in this lab, ensure that that Key Vault appears in the Select an Azure Key Vault drop down list, and click Next.
17. On the Run Settings page, click Next.
18. On the Summary page, click Finish to proceed with the encryption. When prompted, sign in again by using the same user account you used to provision the Azure Key Vault instance earlier in this lab.
19. Once the encryption process is complete, on the Results page, click Close.
20. In the SQL Server Management Studio console, in the Object Explorer pane, under the medical node, expand the Security and Always Encrypted Keys subnodes.
    > The Always Encrypted Keys subnode contains the Column Master Keys and Column Encryption Keys subfolders.
