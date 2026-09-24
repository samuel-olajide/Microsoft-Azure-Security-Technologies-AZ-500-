# Task 1: Deploy an Azure VM and an Azure SQL database
> In this task, you will deploy an Azure VM, which will automatically install Visual Studio and SQL Server Management Studio as part of the deployment.

1. Sign-in to the [Azure portal]([url](https://portal.azure.com/))
   > Sign in to the Azure portal using an account that has the Owner or Contributor role in the Azure subscription you are using for this lab.
3. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Deploy a custom template and press the Enter key.
4. On the Custom deployment blade, click the Build your own template in the editor option.
5. On the Edit template blade, click Load file, locate the \Allfiles\Labs\10\az-500-10_baseinfra.json file and click Open.
6. On the Edit template blade, click Save.
7. On the Custom deployment blade, under Deployment Scope ensure that the following settings are configured (leave any others with their default values): <br> <img width="408" height="437" alt="image" src="https://github.com/user-attachments/assets/6f8d5d50-af3c-4665-b15e-90992baf27e4" />
  - While you can change the administrative credentials used for logging on to the Virtual Machine, you don't have to.
  - To identify Azure regions where you can provision Azure VMs, refer to https://azure.microsoft.com/en-us/regions/offers/
8. Click the Review and Create button and confirm the deployment by clicking the Create button.
> This initiates the deployment of the Azure VM and Azure SQL Database required for this lab.
> Do not wait for the ARM template deployment to be completed, but instead continue to the next exercise. The deployment might take between 20-25 minutes.

# Install the az500-10-DB.json Custom Template

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Deploy a custom template and press the Enter key.
2. On the Custom deployment blade, click the Build your own template in the editor option.
3. On the Edit template blade, click Load file, locate the **.json** file and click Open.
4. Ensure the correct Resource Group is selected.
5. Set the Admin Password to the same password you used for the previous step.
6. Click the Review and Create button and confirm the deployment by clicking the Create button.

> ⚠️ If you receive the deployment error The resource write operation failed to complete successfully with an Error details of Database 'medical' does not exist you may proceed. The Medical database will be present.
