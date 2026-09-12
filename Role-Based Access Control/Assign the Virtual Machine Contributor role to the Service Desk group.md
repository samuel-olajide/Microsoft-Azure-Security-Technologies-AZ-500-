**Task 1: Create a resource group.**

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type Resource groups and press the Enter key.
2. On the Resource groups blade, click + Create and specify the following settings:
   - Subscription name	>>> the name of your Azure subscription
   - Resource group name	>>> ```AZ500Lab01```
   - Location	>>> ```East US```
3. Click Review + create and then Create.
<img width="1435" height="770" alt="image" src="https://github.com/user-attachments/assets/94a55365-d41b-453a-ab21-c176cd05d1eb" />

4. Back on the Resource groups blade, refresh the page and verify your new resource group appears in the list of resource groups.
<img width="1432" height="345" alt="image" src="https://github.com/user-attachments/assets/7e231b53-0ce7-4a79-a96a-7a05d295164f" />


**Task 2: Assign the Service Desk Virtual Machine Contributor permissions to the resource group.**

1. On the Resource groups blade, click the AZ500LAB01 resource group entry.
2. On the AZ500Lab01 blade, click Access control (IAM) in the middle pane.
3. On the AZ500Lab01 | Access control (IAM) blade, click + Add and then, in the drop-down menu, click Add role assignment. <img width="1432" height="765" alt="image" src="https://github.com/user-attachments/assets/20e40931-d79d-4782-9fbd-f0e2048396de" />

4. On the Add role assignment blade, complete each of the following settings before clicking Next:
   - Role in the search tab	>>> ```Virtual Machine Contributor``` <img width="1431" height="772" alt="image" src="https://github.com/user-attachments/assets/ab69a2d6-25b2-4d9d-935e-b12be62fc499" />

   - Assign access to (Under Members Pane) >>>	```User, group, or service principal```
   - Select (+Select Members)	>>> ```Service Desk65001729```
<img width="1431" height="774" alt="image" src="https://github.com/user-attachments/assets/06bf05e1-65ac-41a3-8d99-13691cb1da87" />

5. **Click Review + assign twice** to create the role assignment.
6. From the Access control (IAM) blade, select Check access. <img width="1437" height="772" alt="image" src="https://github.com/user-attachments/assets/771176cd-b72e-4c7e-947d-99c31f5cb959" />

7. On the AZ500Lab01 | Access control (IAM) blade, on the Check access tab, in the Search by name or email address text box, check access for ```Dylan-65001729@LODSPRODMCA.onmicrosoft.com``` <img width="1431" height="775" alt="image" src="https://github.com/user-attachments/assets/2c1542fa-4504-4187-9d62-c34bde7c339b" />

8. In the list of search results, select the user account of Dylan Williams and, on the Dylan Williams assignments - AZ500Lab01 blade, view the newly created assignment.
**Note:** Always remember to check both the Active and Eligible tabs when confirming RBAC assignments.
9. Close the Dylan Williams assignments - AZ500Lab01 blade.
10. Repeat the same last two steps to check access for ```Joseph-65001729@LODSPRODMCA.onmicrosoft.com```
<img width="1433" height="769" alt="image" src="https://github.com/user-attachments/assets/8a4d78cf-56fb-4bbd-881a-4fb3362dc0e3" />
