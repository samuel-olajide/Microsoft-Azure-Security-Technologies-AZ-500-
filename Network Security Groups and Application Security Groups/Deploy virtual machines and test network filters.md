**Task 1: Create a virtual machine to use as a web server.**
_In this task, you will create a virtual machine to use as a web server._

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type ```Virtual machines``` and press the Enter key.
2. On the Virtual machines blade, click + Create and, in the dropdown list, click Virtual machine.
3. On the Basics tab of the Create a virtual machine blade, specify the following settings (leave others with their default values):
   - Subscription	>>> the name of the Azure subscription you will be using in this lab
   - Resource group >>>	```AZ500LAB07```
   - Virtual machine name >>>	```myVmWeb```
   - Region >>>	**(US)East US**
   - Availability options >>>	**No infrastructure redundancy required**
   - Security type >>>	**Standard**
   - Image >>>	```Windows Server 2022 Datacenter: Azure Edition- x64 Gen2```
   - Size	>>> ```Standard D2s v7```
   - Username	>>> ```Student```
   - Password	>>> ```Please create your own password and record it for future reference in subsequent labs```
   - Confirm password	>>> ```Retype your password```
   - Public inbound ports	>>> ```None```
   - Would you like to use an existing Windows Server License	>>> ```No```
_**For public inbound ports, we will rely on the precreated NSG.**_
4. Click Next: Disks > and, on the Disks tab of the Create a virtual machine blade, set the OS disk type to Standard HDD and click Next: Networking >.
5. On the Networking tab of the Create a virtual machine blade, select the previously created network myVirtualNetwork and the default (10.0.0.0/24) subnet.
6. Under NIC network security group select None.
7. Click Next: Management >, then click Next: Monitoring >. On the Monitoring tab of the Create a virtual machine blade, verify the following setting:
   - Boot diagnostics	>>> ```Enabled with managed storage account (recommended)```
8. Click Review + create, on the Review + create blade, ensure that validation was successful and click Create.
<img width="1434" height="778" alt="image" src="https://github.com/user-attachments/assets/1ef4ab25-86ce-4157-913c-513a38e1bf64" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 2: Create a virtual machine to use as a management server.**
_In this task, you will create a virtual machine to use as a management server._

1. In the Azure portal, navigate back to the Virtual machines blade, click + Create, and, in the dropdown list, click Virtual machine.
2. On the Basics tab of the Create a virtual machine blade, specify the following settings (leave others with their default values):
   - Subscription	>>> the name of the Azure subscription you will be using in this lab
   - Resource group >>>	```AZ500LAB07```
   - Virtual machine name >>>	```myVMMgmt```
   - Region >>>	**(US)East US**
   - Availability options >>>	**No infrastructure redundancy required**
   - Security type >>>	**Standard**
   - Image >>>	```Windows Server 2022 Datacenter: Azure Edition- x64 Gen2```
   - Size	>>> ```Standard D2s v7```
   - Username	>>> ```Student```
   - Password	>>> ```Please create your own password and record it for future reference in subsequent labs```
   - Confirm password	>>> ```Retype your password```
   - Public inbound ports	>>> ```None```
   - Would you like to use an existing Windows Server License	>>> ```No```
_**For public inbound ports, we will rely on the precreated NSG.**_
3. Click Next: Disks > and, on the Disks tab of the Create a virtual machine blade, set the OS disk type to Standard HDD and click Next: Networking >.
4. On the Networking tab of the Create a virtual machine blade, select the previously created network myVirtualNetwork and the default (10.0.0.0/24) subnet.
5. Under NIC network security group select None.
6. Click Next: Management >, then click Next: Monitoring >. On the Monitoring tab of the Create a virtual machine blade, verify the following setting:
   - Boot diagnostics >>>	```Enabled with managed storage account (recommended)```  <br> <img width="1422" height="765" alt="image" src="https://github.com/user-attachments/assets/4d3f23f2-a148-4f6d-96f0-5c8a2d2108d5" />

7. Click Review + create, on the Review + create blade, ensure that validation was successful and click Create.
<img width="1434" height="769" alt="image" src="https://github.com/user-attachments/assets/0e60607f-ee55-4bca-83a0-eb6e698831ad" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 3: Associate each virtual machines network interface to it's application security group.**
_In this task, you will associate each virtual machines network interface with the corresponding application security group. The myVMWeb virtual machine interface will be associated to the myAsgWebServers ASG. The myVMMgmt virtual machine interface will be associated to the myAsgMgmtServers ASG._

1. In the Azure portal, navigate back to the Virtual machines blade and verify that both virtual machines are listed with the Running status. <br> <img width="1430" height="709" alt="image" src="https://github.com/user-attachments/assets/d3819efd-ade3-45f6-96ed-aa38eb19896b" />

2. In the list of virtual machines, click the myVMWeb entry.
3. On the myVMWeb blade, in the Networking section, click Network settings and then, on the myVMWeb | Networking settings blade, click the Application security groups tab. <br> <img width="1432" height="774" alt="image" src="https://github.com/user-attachments/assets/4a7af2fa-8045-401b-9959-8cf9f2fe5c20" />

4. Click + Add application security groups, in the Application security group list, select myAsgWebServers, and then click Save. <br> <img width="1433" height="775" alt="image" src="https://github.com/user-attachments/assets/630eb3fa-47fb-429d-b6dd-3ade705bd8b6" />

5. Navigate back to the Virtual machines blade and in the list of virtual machines, click the myVMMgmt entry.
6. On the myVMMgmt blade, in the Networking section, click Networking settings and then, on the myVMMgmt | Networking settings blade, click the Application security groups tab.
7. Click + Add application security groups, in the Application security group list, select myAsgMgmtServers, and then click Add.
<img width="1442" height="601" alt="image" src="https://github.com/user-attachments/assets/a6a7ddd6-1a23-4ca8-ab5c-67cabe6636a8" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 4: Test the network traffic filtering.**
_In this task, you will test the network traffic filters. You should be able to RDP into the myVMMgmnt virtual machine. You should be able to connect from the internet to the myVMWeb virtual machine and view the default IIS web page._

1. Navigate back to the myVMMgmt virtual machine blade.
2. On the myVMMgmt Overview blade, click Connect and, in the drop down menu, click Connect. <br> <img width="1421" height="770" alt="image" src="https://github.com/user-attachments/assets/bf61c498-06d2-43f4-958d-f841ef451bcc" />

3. Download the RDP file and use it to connect to the myVMMgmt Azure VM via Remote Desktop. When prompted to authenticate, provide the following credentials:
   - User name	>>> ```Student```
   - Password	>>> ```Please use your personal password created in Lab 02 > Exercise 1 > Task 1 > Step 9.```
_**Verify that the Remote Desktop connection was successful. At this point you have confirmed you can connect via Remote Desktop to myVMMgmt.**_
<img width="1435" height="770" alt="image" src="https://github.com/user-attachments/assets/19a0ac12-ed39-4b14-b6b7-1581b2c3392e" /> <br>
<img width="1440" height="905" alt="image" src="https://github.com/user-attachments/assets/129dced9-69f8-433f-8ce4-ea992b614d94" />

4. In the Azure portal, navigate to the myVMWeb virtual machine blade.
5. On the myVMWeb blade, in the Operations section, click Run command and then click RunPowerShellScript. <br> <img width="1437" height="775" alt="image" src="https://github.com/user-attachments/assets/074f4116-dd1f-409a-83a3-e3eb64cd1f0b" />

6. On the Run Command Script pane, run the following to install the Web server role on myVmWeb: ```Install-WindowsFeature -name Web-Server -IncludeManagementTools``` 
_**Wait for the installation to complete. This might take a couple of minutes. At that point, you can verify that myVMWeb can be accessed via HTTP/HTTPS.**_
<img width="1433" height="769" alt="image" src="https://github.com/user-attachments/assets/f56209a5-4b56-4bad-a21a-686d4f5cf8b9" />

8. In the Azure portal, navigate back to the myVMWeb blade.
9. On the myVMWeb blade, identify the Public IP address of the myVmWeb Azure VM. <br> <img width="1432" height="770" alt="image" src="https://github.com/user-attachments/assets/617aef43-7e6c-4509-9fdd-74d7372e1587" />

10. Open another browser tab and navigate to IP address you identified in the previous step.
**_The browser page should display the default IIS welcome page because port 80 is allowed inbound from the internet based on the setting of the myAsgWebServers application security group. The network interface of the myVMWeb Azure VM is associated with that application security group._**
<img width="1431" height="847" alt="image" src="https://github.com/user-attachments/assets/61190ae1-14fe-4554-9592-00f07008b9d0" />

**Result:** Validated that the NSG and ASG configuration is working and traffic is being correctly managed.
