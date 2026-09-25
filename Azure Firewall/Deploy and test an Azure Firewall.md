# Task 1: Use a template to deploy the lab environment.
> In this task, you will review and deploy the lab environment.
> In this task, you will create a virtual machine by using an ARM template. This virtual machine will be used in the last exercise for this lab.

1. Sign-in to the Azure portal **https://portal.azure.com/.**
2. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Deploy a custom template and press the Enter key.
3. On the Custom deployment blade, click the Build your own template in the editor option.
4. On the Edit template blade, click Load file, locate the \Allfiles\Labs\08\template.json file and click Open. 
    > Review the content of the template and note that it deploys an Azure VM hosting Windows Server 2016 Datacenter.
5. On the Edit template blade, click Save.
6. On the Custom deployment blade, ensure that the following settings are configured (leave any others with their default values):
   - Setting >>	Value
   - Subscription >>	the name of the Azure subscription you will be using in this lab
   - Resource group >>	Use existing Resource Group AZ500LAB08
   - Location >>	(US) East US
   - adminPassword	>> A secure password of your own choosing for the virtual machines. Remember the password. You will need it later to connect to the VMs.
     > To identify Azure regions where you can provision Azure VMs, refer to https://azure.microsoft.com/en-us/regions/offers/
7. Click Review + create, and then click Create.
<img width="1434" height="771" alt="image" src="https://github.com/user-attachments/assets/563292e5-b1b9-4744-bede-caa94da879ef" />


# Task 2: Deploy the Azure firewall
> ⚠️ If the firewall deployment fails with an error message stating, 'internalservererror,' delete all deployed resources in the Azure portal via the All Resources blade, and then edit the template.json file from task 1 to replace all mentions of 'eastus' with a different region such as 'centralus.' After making the update, re-deploy the template and Azure firewall using the newly specified region for all deployments. Please note: When deploying the template, the Azure portal will still show eastus as the region. This can be ignored as long as all mentions of eastus in the template.json file have been replaced with the new region.
> In this task you will deploy the Azure firewall into the virtual network.

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Firewalls and press the Enter key.
2. On the Firewalls blade, click + Create.
3. On the Basics tab of the Create a firewall blade, specify the following settings: <br> <img width="329" height="508" alt="image" src="https://github.com/user-attachments/assets/fde38c69-3fb4-49be-bd6a-c5e6c8d5c10e" />
4. Click Review + create and then click Create. <br> <img width="1432" height="759" alt="image" src="https://github.com/user-attachments/assets/2d59d146-4522-499b-97df-f92912393533" />
5. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Resource groups and press the Enter key.
6. On the Resource groups blade, in the list of resource group, click the AZ500LAB08 entry.
    > On the AZ500LAB08 resource group blade, review the list of resources. You can sort by Type.
7. In the list of resources, click the entry representing the Test-FW01 firewall.
8. On the Test-FW01 blade, identify the Private IP address that was assigned to the firewall.
   > You will need this information in the next task.


# Task 3: Create a default route
> In this task, you will create a default route for the Workload-SN subnet. This route will configure outbound traffic through the firewall.

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Route tables and press the Enter key.
2. On the Route tables blade, click + Create.
3. On the Create route table blade, specify the following settings:
   - Resource group >>	AZ500LAB08
   - Region	>> East US
   - Name	>> Firewall-route
4. Click Review + create, then click Create, and wait for the provisioning to complete. <br> <img width="1436" height="748" alt="image" src="https://github.com/user-attachments/assets/ec0fb724-ba35-42f1-844c-d443a75d38ec" />
5. On the Route tables blade, click Refresh, and, in the list of route tables, click the Firewall-route entry.
6. On the Firewall-route blade, in the Settings section, click Subnets and then, on the Firewall-route | Subnets blade, click + Associate.
7. On the Associate subnet blade, specify the following settings:
   - Virtual network	>> Test-FW-VN
   - Subnet	>> Workload-SN
    > Ensure the Workload-SN subnet is selected for this route, otherwise the firewall won't work correctly.
8. Click OK to associate the firewall to the virtual network subnet. <br> <img width="1433" height="770" alt="image" src="https://github.com/user-attachments/assets/63185eed-d132-4b40-9499-69e788b375bd" />
9. Back on the Firewall-route blade, in the Settings section, click Routes and then click + Add.
10. On the Add route blade, specify the following settings:
    - Route name	>> FW-DG
    - Destination Type	>> IP Address
    - Destination IP addresses/CIDR ranges	>> 0.0.0.0/0
    - Next hop type	>> Virtual appliance
    - Next hop address	>> the private IP address of the firewall that you identified in the previous task
     > Azure Firewall is actually a managed service, but virtual appliance works in this situation.
11. Click Add to add the route.
<img width="1425" height="776" alt="image" src="https://github.com/user-attachments/assets/13a6e76f-bebf-46e2-9821-59d8c9310763" />


# Task 4: Configure an application rule
> In this task you will create an application rule that allows outbound access to www.bing.com.

1. In the Azure portal, navigate back to the Test-FW01 firewall.
2. On the Test-FW01 blade, in the Settings section, click Rules (classic).
3. On the Test-FW01 | Rules (classic) blade, click the Application rule collection tab, and then click + Add application rule collection.
4. On the Add application rule collection blade, specify the following settings (leave others with their default values):
   - Name	>> App-Coll01
   - Priority	>> 200
   - Action	>> Allow
5. On the Add application rule collection blade, create a new entry in the Target FQDNs section with the following settings (leave others with their default values):
   - name	>> AllowGH
   - Source type	>> IP Address
   - Source	>> 10.0.2.0/24
   - Protocol port	>> http:80, https:443
   - Target FQDNS	>> www.bing.com
6. Click Add to add the Target FQDNs-based application rule.
   > Azure Firewall includes a built-in rule collection for infrastructure FQDNs that are allowed by default. These FQDNs are specific for the platform and can't be used for other purposes.
<img width="1431" height="748" alt="image" src="https://github.com/user-attachments/assets/9e101438-8756-4821-bde4-ee257ef363f0" />
<img width="1439" height="717" alt="image" src="https://github.com/user-attachments/assets/5493cb34-83ad-46bf-a252-31f9bf06d185" />


# Task 5: Configure a network rule
> In this task, you will create a network rule that allows outbound access to two IP addresses on port 53 (DNS).

1. In the Azure portal, navigate back to the Test-FW01 | Rules (classic) blade.
2. On the Test-FW01 | Rules (classic) blade, click the Network rule collection tab and then click + Add network rule collection.
3. On the Add network rule collection blade, specify the following settings (leave others with their default values):
   - Name >>	Net-Coll01
   - Priority	>> 200
   - Action >>	Allow
4. On the Add network rule collection blade, create a new entry in the IP Addresses section with the following settings (leave others with their default values): <br><img width="320" height="332" alt="image" src="https://github.com/user-attachments/assets/f49be80e-8f0c-47f4-b1a4-301baf1fd398" />
    > Check the notification section to see if the previous firewall is successfully updated before creating another rule, else this will display an error <img width="485" height="308" alt="image" src="https://github.com/user-attachments/assets/d43ab5a5-7999-4460-b151-d022a9ee418e" />
5. Click Add to add the network rule.
   > The destination addresses used in this case are known public DNS servers.
<img width="1437" height="770" alt="image" src="https://github.com/user-attachments/assets/41b41124-914f-4d08-90b2-432a3c1f5d00" />
<img width="1433" height="508" alt="image" src="https://github.com/user-attachments/assets/0dc0c6f9-8203-49f7-b096-1275b1e53e58" />


# Task 6: Configure the virtual machine DNS servers
> In this task, you will configure the primary and secondary DNS addresses for the virtual machine. This is not a firewall requirement.

1. In the Azure portal, navigate back to the AZ500LAB08 resource group.
2. On the AZ500LAB08 blade, in the list of resources, click the Srv-Work virtual machine. <br> <img width="1422" height="770" alt="image" src="https://github.com/user-attachments/assets/5a461bb2-ed76-43fe-a0e8-d83b15bdcbfc" />
3. On the Srv-Work blade, click Networking.
4. On the Srv-Work | Networking Settings blade, click the link next to the Network interface entry. <br> <img width="1422" height="486" alt="image" src="https://github.com/user-attachments/assets/401c7572-c572-469b-a193-4d337d15cb03" />
5. On the network interface blade, in the Settings section, click DNS servers, select the Custom option, add the two DNS servers referenced in the network rule: 209.244.0.3 and 209.244.0.4, and click Save to save the change.
6. Return to the Srv-Work virtual machine page.
   >Wait for the update to complete.
   >Updating the DNS servers for a network interface will automatically restart the virtual machine to which that interface is attached, and if applicable, any other virtual machines in the same availability set.

# Task 7: Test the firewall
> In this task, you will test the firewall to confirm that it works as expected.

1. In the Azure portal, navigate back to the AZ500LAB08 resource group.
2. On the AZ500LAB08 blade, in the list of resources, click the Srv-Jump virtual machine.
3. On the Srv-Jump blade, click Connect and, in the drop down menu, click Connect.
4. Download the RDP file and use it to connect to the Srv-Jump Azure VM via Remote Desktop. When prompted to authenticate, provide the following credentials:
   - User name	>> localadmin
   - Password	>> The secure password you chose during deployment of the custom template in task 1 step 6.
     > The following steps are performed in the Remote Desktop session to the Srv-Jump Azure VM.
     > You will connect to the Srv-Work virtual machine. This is being done so we can test the ability to access the bing.com website.
5. Within the Remote Desktop session to Srv-Jump, right-click Start, in the right-click menu, click Run, and, from the Run dialog box, run the following to connect to Srv-Work. ```mstsc /v:Srv-Work```
6. When prompted to authenticate, provide the following credentials:
   - User name	>> localadmin
   - Password	>> The secure password you chose during deployment of the custom template in task 1 step 6.
     > Wait for the Remote Desktop session to be established and the Server Manager interface to load.
7. Within the Remote Desktop session to Srv-Work, in Server Manager, click Local Server and then click IE Enhanced Security Configuration.
8. In the Internet Explorer Enhanced Security Configuration dialog box, set both options to Off and click OK.
9. Within the Remote Desktop session to Srv-Work, start Internet Explorer and browse to https://www.bing.com.
    - The website should successfully display. The firewall allows you access.
10. Browse to http://www.microsoft.com/
    > Within the browser page, you should receive a message with text resembling the following: ```HTTP request from 10.0.2.4:xxxxx to microsoft.com:80. Action: Deny. No rule matched. Proceeding with default action.``` This is expected, since the firewall blocks access to this website.
<img width="1439" height="901" alt="image" src="https://github.com/user-attachments/assets/3709cadf-72af-4bc6-abda-cdbc981f4d69" />

11. Terminate both Remote Desktop sessions.

> Result: You have successfully configured and tested the Azure Firewall.
