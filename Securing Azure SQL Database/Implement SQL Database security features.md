<img width="1435" height="771" alt="image" src="https://github.com/user-attachments/assets/4b02c1e5-ce03-498c-9c47-6f6f5a4e3217" />**Task 1: Deploy an Azure SQL Database**
_In this task, you will use a template to deploy the lab infrastructure._

1. Sign-in to the Azure portal ```https://portal.azure.com/```
2. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type **Deploy a custom template** and press the Enter key.
3. On the Custom deployment blade, click the **Build your own template** in the editor option. <br> <img width="1428" height="695" alt="image" src="https://github.com/user-attachments/assets/e9746637-b5a7-49fa-86af-1d59fe500a41" />
4. On the Edit template blade, click Load file, locate the \Allfiles\Labs\11\azuredeploy.json file and click Open.
5. On the Edit template blade, click Save. <br> <img width="1428" height="775" alt="image" src="https://github.com/user-attachments/assets/b32f3bc2-c2e2-47f1-b9ac-8958aed5bbb5" />
6. On the Custom deployment blade, ensure that the following settings are configured (leave any others with their default values): <img width="316" height="223" alt="image" src="https://github.com/user-attachments/assets/9a92fe4b-0200-42c7-9dba-52ab4554d0e6" />
7. Click Review + Create and then click Create. <br> <img width="1433" height="716" alt="image" src="https://github.com/user-attachments/assets/0a2ca68e-503e-487e-b98b-677ea94f4bfd" />

**Note:** Wait for the deployment to complete.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Task 2: Configure Advanced Data Protection**

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type **Resource groups** and press the Enter key.
2. On the Resource groups blade, in the list of resource group, click the **AZ500LAB11-lod65349404** entry.
3. On the **AZ500LAB11-lod65349404** blade, click the entry representing the newly created SQL Server. <br> <img width="1433" height="769" alt="image" src="https://github.com/user-attachments/assets/e35d1bfd-bf0f-447b-9d67-41a5d6f4b694" />
4. On the SQL server blade, in the **Security** section, click **Microsoft Defender for Cloud**, select **Enable Microsoft Defender for SQL**. <br> <img width="1432" height="773" alt="image" src="https://github.com/user-attachments/assets/daa233e3-500a-469a-b932-bdd963aba0f3" />
5. On the SQL server blade, in the **Security** section, on the **Microsoft Defender for Cloud** page, in the **Microsoft Defender for SQL**: **Enabled at the subscription-level (Configure/settings)** parameter, click (**configure/settings**). <br> <img width="1437" height="739" alt="image" src="https://github.com/user-attachments/assets/655997ed-a363-41c2-86ce-e935bbcf9854" />
6. On the **Server Settings** blade, review the information about pricing and the trial period, **VULNERABILITY ASSESSMENT SETTINGS and ADVANCED THREAT PROTECTION SETTINGS**. <br> <img width="1435" height="699" alt="image" src="https://github.com/user-attachments/assets/06cb27b7-bc1a-4314-9d1e-164889b06ece" />
7. Back to Microsoft Defender for Cloud blade, review Recommendations and Security alerts.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Task 3: Configure Data Classification**
_In this task, you will discover and classify information in SQL database for GPDR and data protection compliance._

1. On the SQL server blade, in the **Settings** section, click **SQL Databases**. <br> <img width="1430" height="768" alt="image" src="https://github.com/user-attachments/assets/8ee40e10-086f-4f0a-80ff-f2aa0ca0588f" />
2. In the list of databases, select the **AZ500LabDb** entry.
3. On the A**Z500LabDb SQL database** blade, in the **Security** section, click **Data Discovery & Classification**.
4. On the **Data Discovery & Classification** blade, click the Classification tab.
_Note: The classification engine scans your database for columns containing potentially sensitive data and provides a list of recommended column classifications._
5. Click the text message We have found 15 columns with classification recommendations displayed on blue bar at the top of the blade. <br> <img width="1436" height="736" alt="image" src="https://github.com/user-attachments/assets/ccb7c01e-1b46-4f97-b80d-74e158f4b110" />
6. Review the listed columns and the recommended sensitivity label.
7. Enable the Select all checkbox and then click **Accept Selected Recommendations**.
_Note: Alternatively, you could select only certain columns and dismiss others. You have the option to change the information type and sensitivity label._
8. Once you have completed your review click Save.
_Note: This will complete the classification and persistently label the database columns with the new classification metadata._
9. Back on the **Data Discovery & Classification** blade Overview tab, note that it has been updated to account for the latest classification information.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Task 4: Configure Auditing**
_In this task, you will first configure server level auditing and then configure database level auditing._

1. In the Azure portal, navigate back to the SQL Server blade.
2. On the SQL Server blade, in the Security section, click Auditing.
_Note: This is server level auditing. The default auditing settings include all the queries and stored procedures executed against the database, as well as successful and failed logins._
3. Set the** Enable Azure SQL Auditing** switch to ON to enable auditing. <br> <img width="1428" height="769" alt="image" src="https://github.com/user-attachments/assets/2cd64199-0978-4f14-a2a8-477da136922c" />
4. Select the Storage checkbox and entry boxes for Subscription and Storage Account will display.
5. Choose your Subscription from the dropdown list.
6. Click Storage account and choose Create new. <br> <img width="1438" height="734" alt="image" src="https://github.com/user-attachments/assets/c005641a-b0f3-4c53-930f-d427e2e6999f" />
7. Click Create New and then on the Create storage account blade, in the Name box, type a globally unique name consisting of between 3 and 24 lower case letters and digits, click OK, <br> <img width="1433" height="730" alt="image" src="https://github.com/user-attachments/assets/2c86dc9f-4d58-4db5-b0f7-b492b778dbf3" />
_Note: You may need to refresh the browser before the storage account becomes available._
8. Back on the Auditing blade, under Advanced properties set Retention (days) to 5. <br> <img width="1430" height="770" alt="image" src="https://github.com/user-attachments/assets/0c81b54f-63e4-4797-a09b-84a7919b103e" />
9. On the Auditing blade, click Save to save the auditing settings.
10. On the server blade, in the Settings section, click SQL Databases.
11. In the list of databases, select the AZ500LabDb entry.
12. On the AZ500LabDb SQL database blade, in the Security section, click Auditing.
_Note: This is database level auditing. Server-level auditing is already enabled. Audits can be written to an Azure storage account, to a Log Analytics workspace, or to the Event Hub. You can configure any combination of these options. If storage-based auditing is enabled on the server, it will always apply to the database, regardless of the database settings._
13. On your SQL database Overview page in the Azure portal, select Query editor (preview) from the left menu. Try to sign in, you might fail on password, firewall rule for your IP address, everything gets audited. Try successful login as well, run query and you might find more details in audit logs. <br> <img width="1429" height="763" alt="image" src="https://github.com/user-attachments/assets/d818fdf6-c89d-4bed-84c8-1367f6fbc092" />
14. switch back to DB, Auditing and Click View Audit Logs. <br> <img width="1425" height="770" alt="image" src="https://github.com/user-attachments/assets/8e33f3fe-7d69-4c59-841a-8fb907c5553d" />
15. On the Audit records blade, note that you can switch between Server audit and Database audit. <br> <img width="1426" height="585" alt="image" src="https://github.com/user-attachments/assets/94f73a63-bc69-4d25-a1c7-ea09449af731" />

**Results:** You have created a SQL server and database, configured data classification, and auditing.
