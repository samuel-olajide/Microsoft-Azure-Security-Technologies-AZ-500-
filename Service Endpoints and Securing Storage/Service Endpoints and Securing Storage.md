# **Task 1: Create a virtual network**
>_In this task, you will create a virtual network._

1. Sign-in to the [Azure portal]([url](https://portal.azure.com/))
2. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Virtual networks and press the Enter key.
3. On the Virtual Networks blade, click + Create.
4. On the Basics tab of the Create virtual network blade, specify the following settings (leave others with their default values) and click Next: IP Addresses: <br> <img width="295" height="217" alt="image" src="https://github.com/user-attachments/assets/eb932f9f-4a4f-4ddf-a173-e1ad0f2ec2a4" />
5. On the IP addresses tab of the Create virtual network blade, set the IPv4 address space to 10.0.0.0/16, in the Subnet name column, click default and, on the Edit subnet blade, specify the following settings and click Save:
   - Subnet name	> ```Public```
   - Subnet address range	> ```10.0.0.0/24```
<img width="1435" height="771" alt="image" src="https://github.com/user-attachments/assets/8ed1f00b-2c04-47ba-b7de-25c91c03c0fa" />
6. Back on the IP addresses tab of the Create virtual network blade, click Review + create.
7. On the Review + create tab of the Create virtual network blade, click Create. <br>
<img width="1431" height="729" alt="image" src="https://github.com/user-attachments/assets/55915445-b25c-4732-b185-9a363c387555" />
<br>
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<br>

# **Task 2: Add a subnet to the virtual network and configure a storage endpoint**
>_In this task, you will create another subnet and enable a service endpoint on that subnet. Service endpoints are enabled per service, per subnet._

1. In the Azure portal, navigate back to the Virtual Networks blade.
2. On the Virtual networks blade, click the myVirtualNetwork entry.
3. On the myVirtualNetwork blade, in the Settings section, click Subnets.
4. On the myVirtualNetwork | Subnets blade, click + Subnet. <br> <img width="1436" height="766" alt="image" src="https://github.com/user-attachments/assets/af6a2278-dbaa-4c3a-9af9-e3b633ec43ad" />
5. On the Add subnet blade, specify the following settings (leave others with their default values):
   - Subnet name > **Private**
   - Subnet address range	> **10.0.1.0/24**
   - Service endpoints	Leave the default of > **None**
7. On the Add subnet blade, click Add.
>**The virtual network now has two subnets: Public and Private.**
<img width="856" height="732" alt="image" src="https://github.com/user-attachments/assets/4748c5d1-70f0-4ea1-b8bc-a19bf9990e03" />

<br>
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<br>

# **Task 3: Configure a network security group to restrict access to the subnet**
>_In this task, you will create a network security group with two outbound security rules (Storage and internet) and one inbound security rule (RDP). You will also associate the network security group with the Private subnet. This will restrict outbound traffic from Azure VMs connected to that subnet._

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Network security groups and press the Enter key.
2. On the Network security groups blade, click + Create.
3. On the Basics tab of the Create network security group blade, specify the following settings: <br> <img width="312" height="217" alt="image" src="https://github.com/user-attachments/assets/733aaa8a-34c2-4f4d-bb53-c5d23eaf8ed2" />
4. Click Review + create and then click Create. <br> <img width="1427" height="605" alt="image" src="https://github.com/user-attachments/assets/e295cc5a-1e99-4336-885c-1165e4ac5f3c" />
>**In the next steps, you will create an outbound security rule that allows communication to the Azure Storage service.**
5. In the Azure portal, navigate back to the Network security groups blade and click the myNsgPrivate entry.
6. On the myNsgPrivate blade, in the Settings section, click Outbound security rules.
7. On the myNsgPrivate | Outbound security rules blade, click + Add.
8. On the Add outbound security rule blade, specify the following settings to explicitly allow outbound traffic to Azure Storage (leave all other values with their default settings): <br> <img width="311" height="436" alt="image" src="https://github.com/user-attachments/assets/0ec82a39-8b22-482e-9e05-0ff5643f4fb8" />
9. On the Add outbound security rule blade, click Add to create the new outbound rule.
10. On the myNsgPrivate blade, in the Settings section, click Outbound security rules, and then click + Add.
11. On the Add outbound security rule blade, specify the following settings to explicitly deny outbound traffic to Internet (leave all other values with their default settings): <br> <img width="324" height="440" alt="image" src="https://github.com/user-attachments/assets/d8ec03bf-b5da-4a7b-baa7-409e5794066b" />
<img width="1433" height="670" alt="image" src="https://github.com/user-attachments/assets/bf92ed40-1900-4f7c-b77b-94d4656c416f" />
> This rule overrides a default rule in all network security groups that allows outbound internet communication.
> In the next steps, you will create an inbound security rule that allows Remote Desktop Protocol (RDP) traffic to the subnet. The rule overrides a default security rule that denies all inbound traffic from the internet. Remote Desktop connections are allowed to the subnet so that connectivity can be tested in a later step.
12. On the myNsgPrivate blade, in the Settings section, click Inbound security rules and then click + Add.
13. On the Add inbound security rule blade, specify the following settings (leave all other values with their default values): <br> <img width="314" height="401" alt="image" src="https://github.com/user-attachments/assets/8be0bdd9-f947-4ed4-a548-22bf3e505a56" />
14. On the Add inbound security rule blade, click Add to create the new inbound rule.
<img width="1439" height="731" alt="image" src="https://github.com/user-attachments/assets/a0179dc5-9510-4232-b2a4-eef3cece4ff7" />
> Now you will associate the network security group with the Private subnet. You will need to click Subnets in MyNSGPrivate and then click +Associate. .
15. On the Subnets blade, select + Associate and specify the following settings in the Associate subnet section and then click OK:
  - Virtual network >	**myVirtualNetwork**
  - Subnet	> **Private**
<img width="1433" height="768" alt="image" src="https://github.com/user-attachments/assets/2fe864b7-3e11-4cb6-91d1-d8820bc3f33b" />

<br>
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<br>

# **Task 4: Configure a network security group to allow rdp on the public subnet**
> _In this task, you will create a network security group with one inbound security rule (RDP). You will also associate the network security group with the Public subnet. This will allow RDP access to the Public VM._

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Network security groups and press the Enter key.
2. On the Network security groups blade, click + Create.
3. On the Basics tab of the Create network security group blade, specify the following settings: <br> <img width="307" height="220" alt="image" src="https://github.com/user-attachments/assets/af5cecee-7fda-4894-be99-6d44ce1b0846" />
4. Click Review + create and then click Create.
   > **In the next steps, you will create an outbound security rule that allows communication to the Azure Storage service.**
5. In the Azure portal, navigate back to the Network security groups blade and click the myNsgPublic entry.
6. On the myNsgPublic blade, in the Settings section, click Inbound security rules and then click + Add.
7. On the Add inbound security rule blade, specify the following settings (leave all other values with their default values): <br> <img width="305" height="391" alt="image" src="https://github.com/user-attachments/assets/599b5462-ff92-4721-81fb-6c8eebea4be9" />
8. On the Add inbound security rule blade, click Add to create the new inbound rule. <br> <img width="1435" height="692" alt="image" src="https://github.com/user-attachments/assets/d55f7147-ed1a-4082-9f87-65bb2ddb02ef" />
   > **Now you will associate the network security group with the Public subnet.**
10. On the Subnets blade, select + Associate and specify the following settings in the Associate subnet section and then click OK:
<img width="1430" height="733" alt="image" src="https://github.com/user-attachments/assets/88054c59-42ae-4419-8c33-3b9cb7c267aa" />

<br>
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<br>

# **Task 5: Create a storage account with a file share**
> In this task, you will create a storage account with a file share and obtain the storage account key.

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Storage accounts and press the Enter key.
2. On the Storage accounts blade, click + Create.
3. On the Basics tab of the Create storage account blade, specify the following settings (leave others with their default values): <br> <img width="322" height="380" alt="image" src="https://github.com/user-attachments/assets/3a6a0023-b400-4a2f-b158-167232b887c0" />
<img width="1439" height="678" alt="image" src="https://github.com/user-attachments/assets/c0f84e95-82e4-4d0f-b08e-bb9a9b431f5a" />
4. On the Basics tab of the Create storage account blade, click Review, wait for the validation process to complete, and click Create.
5. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Resource groups and press the Enter key.
6. On the Resource groups blade, in the list of resource group, click the AZ500LAB12 entry.
7. On the AZ500LAB12 resource group blade, in the list of resources, click the entry representing the newly created storage account. <br> <img width="1430" height="768" alt="image" src="https://github.com/user-attachments/assets/318a605c-093c-4834-94e5-18376b96ac61" />
8. On the storage account Overview blade, click File Shares under the Data storage tab, and then click + File Share. <br> <img width="1430" height="698" alt="image" src="https://github.com/user-attachments/assets/047257b3-c57e-43f7-8618-b3b2aefd7858" />
9. On the New file share blade, untick the Enable backup option in the backup tab. <br> <img width="1442" height="773" alt="image" src="https://github.com/user-attachments/assets/c806133d-e64f-473b-8464-226c7368b6c7" />
10. On the New file share blade, specify the following settings:
    - Name	> **my-file-share**
<img width="1437" height="733" alt="image" src="https://github.com/user-attachments/assets/97e5a6d5-e81d-470e-8e32-84456199ea1e" />
11. On the New file share blade, click Create.
    > **Now, retrieve and record the PowerShell script that creates a drive mapping to the Azure file share.**
12. On the storage account blade, in the list of file shares, click my-file-share. <br> <img width="1432" height="728" alt="image" src="https://github.com/user-attachments/assets/f75ece13-f293-4bec-a9ef-ca64baeceed9" />
13. On the my-file-share blade, click Connect.
14. On the Connect blade, on the Windows tab, copy the PowerShell script that creates a Z drive mapping to the file share. <br> <img width="1431" height="727" alt="image" src="https://github.com/user-attachments/assets/5775c276-45fd-4c3c-9bbf-1b22335a925a" />
    > Record this script. You will need this in a later in this lab in order to map the file share from the Azure virtual machine on the Private subnet.
15. Navigate back to the storage account blade, then in the Security + networking section, click Networking.
16. Under Public network access select Manage and as Default action select Enable from selected networks. <br> <img width="1428" height="771" alt="image" src="https://github.com/user-attachments/assets/a48df4f8-8580-4f5d-8b95-8a1f7dfd77c7" />
17. From the Enabled From selected Network in **step 17**, select the **Enabled from selected networks**
18. Under **Virtual network**, click the **+ Add a virtual network** > **Add existing virtual network**.
19. On the Add networks blade, specify the following settings:
    - Subscription	> **the name of the Azure subscription you are using in this lab**
    - Virtual networks >	**myVirtualNetwork**
    - Subnets >	**Private**
20.  On the Add networks blade, click Add. <br> <img width="1434" height="771" alt="image" src="https://github.com/user-attachments/assets/790b7148-6344-4e04-9679-1a4991b52a53" />
21.  Back on the storage account blade, click Save. <br> <img width="1441" height="772" alt="image" src="https://github.com/user-attachments/assets/a70b697e-13b5-4bcf-a031-4b76937cbbb3" />
> At this point in the lab you have configured a virtual network, a network security group, and a storage account with a file share.

<br>
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<br>

# Task 6: Deploy virtual machines into the designated subnets
> In this task, you will create two virtual machines one in the Private subnet and one in the Public subnet. <br>
> The first virtual machine will be connected to the Private subnet.

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Virtual machines and press the Enter key.
2. On the Virtual machines blade, click + Create and, in the dropdown list, click Virtual machine
3. On the Basics tab of the Create a virtual machine blade, specify the following settings (leave others with their default values): <br> <img width="338" height="563" alt="image" src="https://github.com/user-attachments/assets/055c5af3-c9a0-487f-bb8e-849807b9db77" />
   > For public inbound ports, we will rely on the precreated NSG.
4. Click Next: Disks > and, on the Disks tab of the Create a virtual machine blade, set the OS disk type to Standard HDD and click Next: Networking >.
5. Click Next: Networking >, on the Networking tab of the Create a virtual machine blade, specify the following settings (leave others with their default values): <br> <img width="311" height="239" alt="image" src="https://github.com/user-attachments/assets/386ca008-34b8-41d4-9023-bf56e46293a0" />
6. Click Next: Management >, on the Management tab of the Create a virtual machine blade, accept the default settings and click Review + create.
7. On the Review + create blade, ensure that validation was successful and click Create.
  > The second virtual machine will be connected to the Public subnet.
8. On the Virtual machines blade, click + Add and, in the dropdown list, click Virtual machine.
9. On the Basics tab of the Create a virtual machine blade, specify the following settings (leave others with their default values): <br> <img width="332" height="547" alt="image" src="https://github.com/user-attachments/assets/447d9c58-a11e-4418-9610-0fbdeeb9f573" />
    > For public inbound ports, we will rely on the precreated NSG.
10. Click Next: Disks > and, on the Disks tab of the Create a virtual machine blade, set the OS disk type to Standard HDD and click Next: Networking >.
11. Click Next: Networking >, on the Networking tab of the Create a virtual machine blade, specify the following settings (leave others with their default values): <br> <img width="324" height="217" alt="image" src="https://github.com/user-attachments/assets/a57531e9-befc-4f63-8d5b-04bd3a09d816" />
12. Click Next: Management >, on the Management tab of the Create a virtual machine blade, accept the default settings and click Review + create.
13. On the Review + create blade, ensure that validation was successful and click Create.


<br>
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<br>

# Task 7: Test the storage connection from the private subnet to confirm that access is allowed
> In this task, you will connect to the myVMPrivate virtual machine via Remote Desktop and map a drive to the file share.

1. Navigate back to the Virtual machines blade.
2. On the Virtual machines blade, click the myVMPrivate entry.
3. On the myVMPrivate blade, click Connect and, in the drop down menu, click Connect.
4. Download the RDP file and use it to connect to the myVMPrivate Azure VM via Remote Desktop. When prompted to authenticate, provide the following credentials:
5. Within the Remote Desktop session to myVMPrivate, click Start and then click Windows PowerShell ISE.
6. Within the Windows PowerShell ISE window, open the Script pane, then paste and run the PowerShell script that you recorded earlier in this lab. The script has the following format: <br> <img width="1273" height="806" alt="image" src="https://github.com/user-attachments/assets/be2157a9-291f-4f0a-9267-70c034c061b9" />
7. Start File Explorer and verify that the Z: drive mapping has been successfully created.
8. Next, from the console pane of the Windows PowerShell ISE console, run the following to verify that the virtual machine has no outbound connectivity to the internet: ```Test-NetConnection -ComputerName www.bing.com -Port 80``` <br> <img width="1209" height="814" alt="image" src="https://github.com/user-attachments/assets/d09d7cee-09d4-4558-bc5c-f00fcd5868dd" />
9. Terminate the Remote Desktop session to the myVMPrivate Azure VM.
    > At this point, you have confirmed that the virtual machine in the Private subnet can access the storage account.

<br>
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
<br>

# Task 8: Test the storage connection from the public subnet to confirm that access is denied

1. Navigate back to the Virtual machines blade.
2. On the Virtual machines blade, click the myVMPublic entry.
3. On the myVMPublic blade, click Connect and, in the drop down menu, click Connect.
4. Click Connect via RDP and use it to connect to the myVMPublic Azure VM via Remote Desktop. When prompted to authenticate, enter your credential.
5. Within the Remote Desktop session to myVMPublic, click Start and then click Windows PowerShell ISE.
6. Within the Windows PowerShell ISE window, open the Script pane, then paste and run the same PowerShell script that you ran within the Remote Desktop session to the myVMPrivate Azure VM.
    > This time, you will receive the New-PSDrive : Access is denied error.
    > Access is denied because the myVmPublic virtual machine is deployed in the Public subnet. The Public subnet does not have a service endpoint enabled for the Azure Storage. The storage account only allows network access from the Private subnet.
7. Next, from the console pane of the Windows PowerShell ISE console, run the following to verify that the virtual machine has outbound connectivity to the internet: ```Test-NetConnection -ComputerName www.bing.com -Port 80```
   > The test will succeed because there is no outbound security rule to deny internet on the Public subnet.
8. Terminate the Remote Desktop session to the myVMPublic Azure VM.
   > At this point, you have confirmed that the virtual machine in the Public subnet cannot access the storage account, but has access to the internet.

# Clean up resources
> Remember to remove any newly created Azure resources that you no longer use. Removing unused resources ensures you will not incur unexpected costs.
