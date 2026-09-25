# Task 1: Install Visual Studio 2026

1. Switch to your Server virtual machine if you are not already there.
2. Open Server Manager.
3. Select Local Servers.
4. Set IE Enhanced Security Configuration to Off. <br> <img width="1440" height="781" alt="image" src="https://github.com/user-attachments/assets/ec8af54a-5d46-43b4-b61f-c2786c0ab2eb" />
5. Open the Browser and bypass the warning about IE ESC being turned off.
6. Go to https://visualstudio.microsoft.com/downloads.
7. In the Visual Studio 2026 box, under Community select Free download.
8. When the download finishes, select Open File.
9. Select continue to start the install.
10. Install takes about 10 minutes
11. Choose **.Net Desktop Development** in the Workloads screen.


# Task 2: Run a data-driven application to demonstrate the use of Azure Key Vault in encrypting the Azure SQL database
> You will create a Console application using Visual Studio to load data into the encrypted columns and then access that data securely using a connection string that accesses the key in the Key Vault.

1. From the RDP session to the az500-10-vm1, launch Visual Studio 2026 from the Start menu.
2. Switch to the window displaying Visual Studio 2026 welcome message, click the Sign in button and, when prompted, provide the credentials you used to authenticate to the Azure subscription you are using in this lab.
3. On the Get started page, click Create a new project.
4. In the list of project templates, search for Console App (.NET Framework), in the list of results, click Console App (.NET Framework) for C#, and click Next.
5. On the Configure your new project page, specify the following settings (leave other settings with their default values), then click Create:
   - Project name >>	**OpsEncrypt**
   - Solution name	>> **OpsEncrypt**
   - Framework	>> **.NET Framework 4.7.2**
6. In the Visual Studio console, click the Tools menu, in the drop down menu, click NuGet Package Manager, and, in the cascading menu, click Package Manager Console.
7. In the Package Manager Console pane, run the following to install the first required NuGet package: ```Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider```
8. In the Package Manager Console pane, run the following to install the second required NuGet package: ```Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory```
9. Minimize the RDP session to your Azure virtual machine, then navigate to \Allfiles\Labs\10\program.cs, open it in Notepad, copy its content into Clipboard. File can be downloaded [here]([url](https://drive.google.com/file/d/1PcvoWQSgRpqOGJ8Duzef8OBC-_zTXoyi/view?usp=drive_link)).
10. Return to the RDP session, and in the Visual Studio console, in the Solution Explorer window, click Program.cs and replace its content with the code you copied into Clipboard.
11. In the Visual Studio window, in the Program.cs pane, in line 15, replace the (connection string noted earlier) placeholder with the Azure SQL database ADO.NET connection string you recorded earlier in the lab. In the connection string, replace the {your_password} placeholder, with the password that you specified in the deployment in Exercise 1. If you saved the string on the lab computer, you may need to leave the RDP session to copy the ADO string, then return to the Azure virtual machine to paste it in.
12. In the Visual Studio window, in the Program.cs pane, in line 16, replace the (client id noted earlier) placeholder with the value of Application (client) ID of the registered app you recorded earlier in the lab.
13. In the Visual Studio window, in the Program.cs pane, in line 17, replace the (key value noted earlier) placeholder with the the value of Key1 of the registered app you recorded earlier in the lab. <br> <img width="1406" height="834" alt="image" src="https://github.com/user-attachments/assets/a6b6a101-bcc0-430a-8e20-9b719eb8dcb2" />
14. In the Visual Studio console, click the Start button to initiate the build of the console application and start it.
15. The application will start a Command Prompt window. When prompted for password, type the password that you specified in the deployment in Exercise 1 to connect to Azure SQL Database.
16. Leave the console app running and switch to the SQL Management Studio console.
17. In the Object Explorer pane, right-click the medical database and, in the right-click menu, click New Query.
18. From the query window, run the following query to verify that the data that loaded into the database from the console app is encrypted. ```SELECT FirstName, LastName, SSN, BirthDate FROM Patients;``` <br> <img width="1442" height="834" alt="image" src="https://github.com/user-attachments/assets/89d44eef-f565-423b-abab-8d7a19eb82de" />
19. Switch back to the console application where you are prompted to enter a valid SSN. This will query the encrypted column for the data. At the Command Prompt, type the following and press the Enter key: ```999-99-0003```
    > Verify that the data returned by the query is not encrypted.
<img width="980" height="512" alt="image" src="https://github.com/user-attachments/assets/9236c6f6-88e7-43b8-a202-7d009278a363" />
20. To terminate the console app, press the Enter key
