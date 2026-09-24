# Task 1: Create and configure a Key Vault
> In this task, you will create an Azure Key Vault resource. You will also configure the Azure Key Vault permissions.

1. Open the Cloud Shell by clicking the first icon (next to the search bar) at the top right of the Azure portal. If prompted, select PowerShell and Create storage.
2. Ensure PowerShell is selected in the drop-down menu in the upper-left corner of the Cloud Shell pane.
3. In the PowerShell session within the Cloud Shell pane, run the following to create an Azure Key Vault in the resource group AZ500Lab10-lod65493277. (If you chose another name for this lab's Resource Group out of Task 1, use that name for this task as well). The Key Vault name must be unique. Remember the name you have chosen. You will need it throughout this lab.
   > $kvName = 'az500kv' + $(Get-Random)
   > $location = (Get-AzResourceGroup -ResourceGroupName 'AZ500Lab10-lod65493277').Location
   > New-AzKeyVault -VaultName $kvName -ResourceGroupName 'AZ500Lab10-lod65493277' -Location $location -DisableRbacAuthorization
**🗒️The output of the last command will display the vault name and the vault URI. The vault URI is in the format https://(vault_name).vault.azure.net/**
<img width="1255" height="737" alt="image" src="https://github.com/user-attachments/assets/91b88810-7af4-4ca9-9095-13f73a32a002" />
4. Close the Cloud Shell pane.
5. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Resource groups and press the Enter key.
6. On the Resource groups blade, in the list of resource group, click the AZ500Lab10-lod65493277 (or other name you chose earlier for the resource group) entry.
7. On the Resource Group blade, click the entry representing the newly created Key Vault.
8. On the Key Vault blade, in the Overview section, click Access Policies and then click + Create.
9. On the Create an access policy blade, specify the following settings (leave all others with their default values):
    - Setting	Value
    - Configure from template (optional) >> **Key, Secret, & Certificate Management**
    - Key permissions	>> **click Select all resulting in total of 9 selected permissions**
    - Key permissions/Cryptographic Operations	>> **click Sign resulting in total of 1 selected permissions**
    - Secret permissions	>> **click Select all resulting in total of 7 selected permissions**
    - Certification permissions	>> **click Select all resulting in total of 15 selected permissions**
    - Select principal	>> **On the Principal blade, select your user account, and click Next**
    - Application (optional)	>> click **Next**
    - Review + create	>> click **Create**
> 🗒️ The previous Review + create operation returns to the Access policies page that lists Application, Email, Key Permissions, Secret Permissions, and Certificate Permissions.
<img width="1265" height="804" alt="image" src="https://github.com/user-attachments/assets/05ea20d4-cf1a-46aa-acd6-7aac80a30aa9" />
<img width="1275" height="801" alt="image" src="https://github.com/user-attachments/assets/2d03a1ac-7a4a-40d2-99a7-873d0d3714ef" />

# Task 2: Add a key to Key Vault
> In this task, you will add a key to the Key Vault and view information about the key.

1. In the Azure portal, open a PowerShell session in the Cloud Shell pane.
2. Ensure PowerShell is selected in the upper-left drop-down menu of the Cloud Shell pane.
3. In the PowerShell session within the Cloud Shell pane, run the following to add a software-protected key to the Key Vault:
   - ```$kv = Get-AzKeyVault -ResourceGroupName 'AZ500Lab10-lod65493277'```
   - ```$key = Add-AZKeyVaultKey -VaultName $kv.VaultName -Name 'MyLabKey' -Destination 'Software'```
> 🗒️The name of the key is **MyLabKey**
4. In the PowerShell session within the Cloud Shell pane, run the following to verify the key was created: ```Get-AZKeyVaultKey -VaultName $kv.VaultName``` <br> <img width="1284" height="651" alt="image" src="https://github.com/user-attachments/assets/20365783-9d74-4302-980f-49eb15c80ce4" />
5. In the PowerShell session within the Cloud Shell pane, run the following to display the key identifier: ```$key.key.kid```
6. Minimize the Cloud Shell pane.
7. Back in the Azure portal, on the Key Vault blade, in the Objects section, click Keys.
8. In the list of keys, click the MyLabKey entry and then, on the MyLabKey blade, click the entry representing the current version of the key. <br> <img width="1272" height="813" alt="image" src="https://github.com/user-attachments/assets/1b89aa98-f158-4b00-8a84-48a25eae537e" />
> Examine the information about the key you created.
> You can reference any key by using the key identifier. To get the most current version, reference https://(key_vault_name).vault.azure.net/keys/MyLabKey or get the specific version with: https://.vault.azure.net/keys/MyLabKey/(key_version)

# Task 3: Add a Secret to Key Vault

1. Switch back to the Cloud Shell pane.
2. In the PowerShell session within the Cloud Shell pane, run the following to create a variable with a secure string value: ```$secretvalue = ConvertTo-SecureString 'Pa55w.rd1234' -AsPlainText -Force```
3. In the PowerShell session within the Cloud Shell pane, run the following to add the secret to the vault: ```$secret = Set-AZKeyVaultSecret -VaultName $kv.VaultName -Name 'SQLPassword' -SecretValue $secretvalue```
   > 🗒️ The name of the secret is **SQLPassword**.
<img width="1279" height="155" alt="image" src="https://github.com/user-attachments/assets/a73138ff-69d0-4f1f-930d-8277c8921630" />
4. In the PowerShell session within the Cloud Shell pane, run the following to verify the secret was created. ```Get-AZKeyVaultSecret -VaultName $kv.VaultName``` <br> <img width="1280" height="636" alt="image" src="https://github.com/user-attachments/assets/f36a28ff-4f5f-4266-823d-8eec83964d1c" />
5. Minimize the Cloud Shell pane.
6. In the Azure portal, navigate back to the Key Vault blade, in the Objects section, click Secrets. <br> <img width="1278" height="731" alt="image" src="https://github.com/user-attachments/assets/8117dc45-24ed-4b36-a98a-675656c475d1" />
7. In the list of secrets, click the SQLPassword entry and then, on the SQLPassword blade, click the entry representing the current version of the secret.
<img width="1271" height="807" alt="image" src="https://github.com/user-attachments/assets/41b46ed7-d7bd-4b1e-97b0-c4c5ca91c540" />
> 🗒️ Examine the information about the secret you created.
> To get the most current version of a secret, reference **https://<key_vault_name>.vault.azure.net/secrets/<secret_name>** or get a specific version, reference **https://<key_vault_name>.vault.azure.net/secrets/<secret_name>/<secret_version>**

