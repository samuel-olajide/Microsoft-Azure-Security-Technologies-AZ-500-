# Exercise 1: Deploy an Azure virtual machine

1. Sign-in to the Azure portal https://portal.azure.com/.
2. Open the Cloud Shell by clicking the first icon in the top right of the Azure Portal. If prompted, select PowerShell.
3. Ensure PowerShell is selected in the drop-down menu in the upper-left corner of the Cloud Shell pane.
4. In the Getting started window, leave the default setting as is: Select a subscription to get started. You can optionally mount a storage account to persist files between sessions. No storage account required.
5. From the Subscription drop-down menu, select your lodsubscription.
6. Leave Use an existing private virtual network unchecked, then click Apply.
7. In the PowerShell session within the Cloud Shell pane, run the following to create a resource group that will be used in this lab: ```New-AzResourceGroup -Name AZ500LAB131415 -Location 'EastUS'```
8. In the PowerShell session within the Cloud Shell pane, run the following to enable encryption at host (EAH) ```Register-AzProviderFeature -FeatureName "EncryptionAtHost" -ProviderNamespace Microsoft.Compute ```
9. In the PowerShell session within the Cloud Shell pane, run the following to create a new Azure virtual machine. ```New-AzVm -ResourceGroupName "AZ500LAB131415" -Name "myVM" -Location 'EastUS' -VirtualNetworkName "myVnet" -SubnetName "mySubnet" -SecurityGroupName   "myNetworkSecurityGroup" -PublicIpAddressName "myPublicIpAddress" -PublicIpSku Standard -OpenPorts 80,3389 -Size Standard_D2s_v7 ```
10. When prompted for credentials: Enter username and password and wait for the deployment to complete.
11. In the PowerShell session within the Cloud Shell pane, run the following to confirm that the virtual machine named myVM was created and its ProvisioningState is Succeeded. ```Get-AzVM -Name 'myVM' -ResourceGroupName 'AZ500LAB131415' | Format-Table```
12. Close the Cloud Shell pane.

# Exercise 2: Create an Log Analytics workspace
> In this task, you will create a Log Analytics workspace.

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Log Analytics workspaces and press the Enter key.
2. On the Log Analytics workspaces blade, click + Create.
3. On the Basics tab of the Create Log Analytics workspace blade, specify the following settings (leave others with their default values): <img width="303" height="215" alt="image" src="https://github.com/user-attachments/assets/1531f8a9-ed76-4780-99b4-6d711de1976f" />
4. Select Review + create.
5. On the Review + create tab of the Create Log Analytics workspace blade, select Create.
<img width="1403" height="732" alt="image" src="https://github.com/user-attachments/assets/c97a9f00-a5fd-415a-addf-47e1925be908" />
<img width="1160" height="508" alt="image" src="https://github.com/user-attachments/assets/7fcd7f9c-6dd5-4af4-8164-b8f3e502e7da" />


# Exercise 3: Create an Azure storage account

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Storage accounts and press the Enter key.
2. On the Storage accounts blade in the Azure portal, click the + Create button to create a new storage account.
3. On the Basics tab of the Create storage account blade, specify the following settings (leave others with their default values): <img width="305" height="454" alt="image" src="https://github.com/user-attachments/assets/2bdb484e-ee5f-47fd-babd-c3f0f7d2d84a" />
4. On the Basics tab of the Create storage account blade, click Review + create. After the validation process completes, click Create.
   > Wait for the Storage account to be created. This should take about 2 minutes
<img width="1425" height="715" alt="image" src="https://github.com/user-attachments/assets/6ee1f986-f9f7-4c7d-ac4c-71efa95f37a9" />


# Exercise 4: Create a Data Collection Rule

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Monitor and press the Enter key.
2. On the Monitor Settings blade, click Data Collection Rules.
3. Click the + Create button to create a new data collection rule.
4. On the Basics tab of the Create Data Collection Rule blade, specify the following settings: <img width="303" height="336" alt="image" src="https://github.com/user-attachments/assets/63448c10-547e-4c60-81b9-5e4598bfd728" />
<img width="1435" height="773" alt="image" src="https://github.com/user-attachments/assets/fbe304f5-ad9a-4bf6-96ac-ece7627ee19e" />
5. Click on the button labeled Next: Resources > to proceed.
6. On the Resources page, select + Add resources.
7. In the Select a scope template, check the Subscription box in the Scope.
8. At the bottom of the Select a scope template, click Apply.
9. At the bottom of the Resources page, select Next: Collect and deliver >.
10. Click + Add data source, then on the Add data source page, change the Data source type drop-down menu to display Performance Counters. Leave the following default settings: <img width="290" height="210" alt="image" src="https://github.com/user-attachments/assets/67495965-4f13-4007-bcb3-4d2ee74746b4" />
<img width="1431" height="773" alt="image" src="https://github.com/user-attachments/assets/945cc493-384b-4856-85bc-3e01676628c8" />
<img width="1435" height="773" alt="image" src="https://github.com/user-attachments/assets/a69491fb-76dc-481d-9594-8b2db10db2a6" />
11. Click on the button labeled Next: Destination > to proceed.
12. Click + Add destination, change the Destination type drop-down menu to display **Log Analytics Workspace**. In the Subscription window, ensure that your Subscription is displayed, then change the Account or namespace drop-down menu to reflect your previously created Log Analytics Workspace. <br> <img width="1432" height="770" alt="image" src="https://github.com/user-attachments/assets/a10a8847-fd48-40b9-b2cb-dc1369b49e45" />
13. Click on Save button at the bottom of the page. <br> <img width="1433" height="773" alt="image" src="https://github.com/user-attachments/assets/8eda3991-f170-4ca3-a1ed-9f37225466db" />
14. Click Review + create.
15. Click Create.
<img width="1429" height="738" alt="image" src="https://github.com/user-attachments/assets/0d054d1d-3fd0-4477-9102-df2bee448688" />
<img width="1430" height="775" alt="image" src="https://github.com/user-attachments/assets/39c4be2c-305f-4e14-916a-028add50f623" />
