**Task 1: Use Azure CLI to create a user account for Dylan Williams.**

1. In the drop-down menu in the upper-left corner of the Cloud Shell pane, select **Bash** (or: Switch to Bash), and, when prompted, click Confirm.
2. In the Bash session within the Cloud Shell pane, run the following to identify the name of your Microsoft Entra tenant: ```DOMAINNAME=$(az ad signed-in-user show --query 'userPrincipalName' | cut -d '@' -f 2 | sed 's/\"//')```
3. In the Bash session within the Cloud Shell pane, run the following to create a user, Dylan Williams. Use yourdomain: ```az ad user create --display-name "Dylan Williams" --password "Pa55w.rd1234" --user-principal-name Dylan@$DOMAINNAME``` Domain added here: ```az ad user create --display-name "Dylan Williams" --password "Pa55w.rd1234" --user-principal-name Dylan@dare3103gmail.onmicrosoft.com```
4. In the Bash session within the Cloud Shell pane, run the following to list Microsoft Entra ID user accounts (the list should include user accounts of Joseph, Isabel, and Dylan) ```az ad user list --output table | grep 65001729```
<img width="1919" height="941" alt="image" src="https://github.com/user-attachments/assets/874d49c7-2e79-4a50-af77-465520a59dff" />

<img width="1432" height="451" alt="image" src="https://github.com/user-attachments/assets/8e2295fc-e294-4b67-afe5-645d8773fcc7" />


**Task 2: Use Azure CLI to create the Service Desk group and add the user account of Dylan to the group.**

1. In the same Bash session within the Cloud Shell pane, run the following to create a new security group named Service Desk. ```az ad group create --display-name "Service Desk65001729" --mail-nickname "ServiceDesk"``` <img width="1919" height="937" alt="image" src="https://github.com/user-attachments/assets/210cedeb-6c2c-406c-a14b-bd1b481f7f14" />

2. In the Bash session within the Cloud Shell pane, run the following to list the Microsoft Entra ID groups (the list should include Service Desk65001729, Senior Admins65001729, and Junior Admins groups): ```az ad group list -o table``` <img width="1708" height="123" alt="image" src="https://github.com/user-attachments/assets/a77a815a-8993-4b23-a3b1-9780e6c1e4f5" />

3. In the Bash session within the Cloud Shell pane, run the following to obtain a reference to the user account of Dylan Williams: ```USER=$(az ad user list --filter "UserPrincipalName eq 'Dylan-65001729@LODSPRODMCA.onmicrosoft.com'")```
4. In the Bash session within the Cloud Shell pane, run the following to obtain the objectId property of the user account of Dylan Williams: ```OBJECTID=$(echo $USER | jq '.[].id' | tr -d '"')```
<img width="1432" height="766" alt="image" src="https://github.com/user-attachments/assets/4daec011-4e39-49b4-bd22-4053cf0efc79" />

5. In the Bash session within the Cloud Shell pane, run the following to add the user account of Dylan to the Service Desk65001729 group: ```az ad group member add --group "Service Desk65001729" --member-id $OBJECTID```
6. In the Bash session within the Cloud Shell pane, run the following to list members of the Service Desk65001729 group and verify that it includes the user account of Dylan: ```az ad group member list --group "Service Desk65001729"``` <img width="1918" height="591" alt="image" src="https://github.com/user-attachments/assets/2ac00304-e403-488f-b69e-2f7a121afb95" />
