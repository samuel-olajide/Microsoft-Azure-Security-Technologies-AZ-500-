**Task 1: Create a virtual network with one subnet.**

1. Sign-in to the Azure portal ```https://portal.azure.com/```
2. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type ```Virtual networks``` and press the Enter key.
3. On the Virtual networks blade, click + Create.
4. On the Basics tab of the Create virtual network blade, specify the following settings (leave others with their default values) and click Next: IP Addresses:
   - Subscription >>>	Name of the Azure subscription you are using in this lab
   - Resource group	>>> Use the provided Resource Group named AZ500LAB07
   - Name	>>> ```myVirtualNetwork```
   - Region >>>	**East US**
5. On the IP addresses tab of the Create virtual network blade, set the IPv4 address space to 10.0.0.0/16, and, if needed, in the Subnet name column, click default, on the Edit subnet blade, specify the following settings and click Save:
   - Subnet name	>>> ```default```
   - Subnet address range >>>	```10.0.0.0/24```
<img width="1428" height="772" alt="image" src="https://github.com/user-attachments/assets/7c956645-2293-492a-a248-5a7e87c48f68" />

6. Back on the IP addresses tab of the Create virtual network screen, click Review + create.
7. On the Review + create tab of the Create virtual network screen, click Create.
<img width="1434" height="775" alt="image" src="https://github.com/user-attachments/assets/f17a91f1-6407-47f3-8013-277fe3ff3b01" />
<img width="1435" height="772" alt="image" src="https://github.com/user-attachments/assets/3e3bc3a0-b42f-4058-b126-0737f464c342" />

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 2: Create two application security groups.**

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type ```Application security groups``` and press the Enter key.
2. On the Application security groups blade, click + Create.
3. On the Basics tab of the Create an application security group blade, specify the following settings:
   - Resource group	AZ500LAB07
   - Name	myAsgWebServers
   - Region	East US
**This group will be for the web servers.**
4. Click Review + create and then click Create. <img width="1433" height="768" alt="image" src="https://github.com/user-attachments/assets/5aaa9d56-03c9-49f6-8018-f0788f3af352" />
5. Navigate back to the Application security groups blade and click + Create.
6. On the Basics tab of the Create an application security group blade, specify the following settings:
   - Resource group	>>> ```AZ500LAB07```
   - Name >>>	```myAsgMgmtServers```
   - Region	>>> **East US**
**This group will be for the management servers.**
7. Click Review + create and then click Create.
<img width="1434" height="772" alt="image" src="https://github.com/user-attachments/assets/e4fd2246-a562-4df5-80c5-fa71b9319f24" />

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 3: Create a network security group and associate it with the virtual network subnet.**

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type ```Network security groups``` and press the Enter key.
2. On the Network security groups blade, click + Create.
3. On the Basics tab of the Create network security group blade, specify the following settings:
   - Subscription	>>> Name of the Azure subscription you are using in this lab
   - Resource group	>>> **AZ500LAB07**
   - Name >>>	```myNsg```
   - Region >>>	**East US**
4. Click Review + create and then click Create. <img width="1435" height="770" alt="image" src="https://github.com/user-attachments/assets/46d34ff7-30b3-4035-ac66-0f474817a585" />

5. In the Azure portal, navigate back to the Network security groups blade and select the myNsg entry. Or select Go to resource if available. <img width="1426" height="774" alt="image" src="https://github.com/user-attachments/assets/e2944f8f-60ee-405b-88b3-edd27c3d60b4" />

6. On the myNsg blade, in the Settings section, click Subnets and then select + Associate. <img width="1437" height="774" alt="image" src="https://github.com/user-attachments/assets/7b82c301-28c9-483e-89db-d00e740642ce" />

7. On the Associate subnet blade, specify the following settings and select OK:
   - Virtual network >>>	```myVirtualNetwork```
   - Subnet >>>	```default```
<img width="1433" height="777" alt="image" src="https://github.com/user-attachments/assets/78cf5bcc-9141-4ebb-89fd-34847d77d9fa" />

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 4: Create inbound NSG security rules to all traffic to web servers and RDP to the management servers.**

1. On the myNsg blade, in the Settings section, click Inbound security rules.
2. Review the default inbound security rules and then click + Add.
3. On the Add inbound security rule blade, specify the following settings to allow TCP ports 80 and 443 to the **myAsgWebServers** application security group (leave all other values with their default values):
   - Source >>>	**Any**
   - Source port ranges	>>> *
   - Destination	>>> in the drop-down list, select Application security group and then click **myAsgWebServers**
   - Service	>>> **Custom**
   - Destination port ranges	>>> ```80,443```
   - Protocol	>>> ```TCP```
   - Action	>>> ```Allow```
   - Priority	>>> ```100```
   - Name	>>> ```Allow-Web-All```
4. Select the Add button on the Add inbound security rule page, to create the new inbound rule. <img width="1438" height="774" alt="image" src="https://github.com/user-attachments/assets/67b588dd-dea8-4074-8ee2-0f8a9d7e239f" />

5. On the myNsg blade, in the Settings section, click Inbound security rules, and then click + Add.
6. On the Add inbound security rule blade, specify the following settings to allow the RDP port (TCP 3389) to the **myAsgMgmtServers** application security group (leave all other values with their default values):
   - Source	>>> **Any**
   - Source port ranges >>>	*
   - Destination >>>	in the drop-down list, select Application security group and then click **myAsgMgmtServers**
   - Service	>>> **Custom**
   - Destination port ranges >>>	```3389```
   - Protocol	>>> ```TCP```
   - Action	>>> ```Allow```
   - Priority	>>> ```110```
   - Name	>>> ```Allow-RDP-All```
  7. Select Add on the Add inbound security rule page, to create the new inbound rule.
<img width="1435" height="776" alt="image" src="https://github.com/user-attachments/assets/22bb42a9-ebcf-460d-8592-a6640df585a4" />

**Result:** Deployed a virtual network, network security with inbound security rules, and two application security groups.
