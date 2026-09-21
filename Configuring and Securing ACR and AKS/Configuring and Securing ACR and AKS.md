**Task 1: Create an Azure Container Registry**
_In this task, you will create a resource group for the lab and an Azure Container Registry._

1. Sign-in to the Azure portal ```https://portal.azure.com/```
2. In the Azure portal, open the Cloud Shell by clicking the first icon in the top right of the Azure Portal. If prompted, click Bash, No storage account required, select your Subscription, and then click Apply.
3. In the Bash session within the Cloud Shell pane, run the following to create a new resource group for this lab: ```az group create --name AZ500LAB09 --location eastus2```
4. In the Bash session within the Cloud Shell pane, run the following to verify the resource group was created: ```az group list --query "[?name=='AZ500LAB09']" -o table```
5. In the Bash session run the following commands to register the **Container Registery** in the lab environment.
   - ```az provider register --namespace Microsoft.Kubernetes```
   - ```az provider register --namespace Microsoft.KubernetesConfiguration```
   - ```az provider register --namespace Microsoft.OperationsManagement```
   - ```az provider register --namespace Microsoft.OperationalInsights```
   - ```az provider register --namespace Microsoft.ContainerService```
   - ```az provider register --namespace Microsoft.ContainerRegistry```
6. In the Bash session within the Cloud Shell pane, run the following to create a new Azure Container Registry (ACR) instance (The name of the ACR must be globally unique): ```az acr create --resource-group AZ500LAB09 --name az50065239665 --sku Basic```
7. In the Bash session within the Cloud Shell pane, run the following to confirm that the new ACR was created: ```az acr list --resource-group AZ500LAB09 -o table```

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 2: Create a Dockerfile, build a container and push it to Azure Container Registry**
_In this task, you will create a Dockerfile, build an image from the Dockerfile, and deploy the image to the ACR._

1. In the Bash session within the Cloud Shell pane, run the following to create a Dockerfile to create an Nginx-based image: ```echo FROM nginx > Dockerfile```
2. In the Bash session within the Cloud Shell pane, run the following to build an image from the Dockerfile and push the image to the new ACR.
   - ```ACRNAME=$(az acr list --resource-group AZ500LAB09 --query '[].{Name:name}' --output tsv)```
   - ```az acr build --resource-group AZ500LAB09 --image sample/nginx:v1 --registry $ACRNAME --file Dockerfile .```
**Wait for the command to successfully complete. This might take about 2 minutes.**
3. Close the Cloud Shell pane.
4. In the Azure portal, navigate to the **AZ500LAB09** resource group and, in the list of resources, click the entry representing the Azure Container Registry instance you provisioned in the previous task. <br> <img width="1432" height="523" alt="image" src="https://github.com/user-attachments/assets/1dc0dfbb-ca1d-4d41-bf9e-5a14f5cc3852" />
5. On the Container registry blade, in the **Services** section, click **Repositories**.
6. Verify that the list of repositories includes the new container image named sample/nginx. <br> <img width="1432" height="775" alt="image" src="https://github.com/user-attachments/assets/0f8c64c7-9ed6-49d4-ae2e-bd7c743e9d79" />

7. Click the sample/nginx entry and verify presence of the v1 tag that identifies the image version.
8. Click the v1 entry to view the image manifest. <br> <img width="1430" height="768" alt="image" src="https://github.com/user-attachments/assets/2ca35fbb-77c0-4750-a0b3-aa06e01f3122" />

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 3: Create an Azure Kubernetes Service cluster**
_In this task, you will create an Azure Kubernetes service and review the deployed resources._

1. In the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type ```Kubernetes services``` and press the Enter key.
2. On the Kubernetes services blade, click + Create and, in the drop-down menu, click + Create a Kubernetes cluster
3. On the Basics tab of the Create Kubernetes cluster blade, select Cluster preset configuration, select Dev/Test ($). Now specify the following settings (leave others with their default values):
   - Subscription	>> Use the name of the Azure subscription you are using in this lab
   - Resource group	>> **AZ500LAB09**
   - Cluster preset configuration >>	**Dev/Test** <br> <img width="1427" height="708" alt="image" src="https://github.com/user-attachments/assets/77fdac84-587f-4420-8763-888166098344" />
   - Kubernetes cluster name	>> ```MyKubernetesCluster```
   - Region >>	**eastus2**
   - Fleet Manager >>	**None**
   - Availability zones	>> **None**
   - AKS pricing tier	>> **Free**
   - Enable long term support	>> **Unchecked**
   - Kubernetes version	>> Use default
   - Automatic upgrade	>> Keep the default
   - Node security channel type	>> Keep the default
   - Authentication and Authorization	>> **Local accounts with Kubernetes RBAC**
4. Click Next and, on the Node Pools tab of the Create Kubernetes cluster blade, specify the following settings (leave others with their default values):
   - Enable node auto-provisioning >>	**Uncheck box**
   - Enable virtual nodes	>> **Uncheck box**
   - Other values	>> **Keep the defaults**
⚠️**Regardless of what any Recommendations popup suggests, ensure you click on the Node size in the Node pools section, and set it to Standard_D2s_v5 or Standard_D2s_v7**
5. Click Next, to get to Networking.
6. On the Networking tab of the Create Kubernetes cluster blade, specify the following settings (leave others with their default values):
   - Enable private cluster	>> **Unchecked**
   - Set authorized IP ranges	>> **Unchecked**
   - Network configuration	>> **Azure CNI Overlay**
   - DNS name prefix	>> **Leave the default value**
   - Network policy	>> **None**
**AKS can be configured as a private cluster. This assigns a private IP to the API server to ensure network traffic between your API server and your node pools remains on the private network only. For more information, visit ```https://docs.microsoft.com/en-us/azure/aks/private-clusters page.```**
7. Click Next and, on the Integrations tab of the Create Kubernetes cluster page, leave All values at default.
📝 **In production scenarios, you would want to enable monitoring. Monitoring is disabled in this case since it is not covered in the lab.**
8. Click Review + Create and then click Create. <br> <img width="1424" height="427" alt="image" src="https://github.com/user-attachments/assets/cf165bb5-605f-41e1-8158-1e4e9c7c3386" />
9. Once the deployment completes, in the Azure portal, in the Search resources, services, and docs text box at the top of the Azure portal page, type ```Resource groups``` and press the Enter key.
10. On the Resource groups blade, in the listing of resource groups, note a new resource group named **MC_AZ500LAB09_MyKubernetesCluster_eastus2** that holds components of the AKS Nodes. Review resources in this resource group. <br> <img width="1424" height="772" alt="image" src="https://github.com/user-attachments/assets/97230a85-a04b-4f56-a8ea-2ed8237f0ab2" />
11. Navigate back to the Resource groups blade and click the AZ500LAB09 entry. <br> <img width="1435" height="770" alt="image" src="https://github.com/user-attachments/assets/ef1acf27-b731-413d-bee4-583c5e660aff" />

12. In the Azure portal, open a Bash session in the Cloud Shell.
13. In the Bash session within the Cloud Shell pane, run the following to connect to the Kubernetes cluster: ```az aks get-credentials --resource-group AZ500LAB09 --name MyKubernetesCluster```
14. In the Bash session within the Cloud Shell pane, run the following to list nodes of the Kubenetes cluster: ```kubectl get nodes```
*Verify that the Status of the cluster node is listed as Ready.*
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 4: Grant the AKS cluster permissions to access the ACR**
_In this task, you will grant the AKS cluster permission to access the ACR and manage its virtual network._

1. In the Bash session within the Cloud Shell pane, run the following to configure the AKS cluster to use the Azure Container Registry instance you created earlier in this lab. ```ACRNAME=$(az acr list --resource-group AZ500LAB09 --query '[].{Name:name}' --output tsv)``` ```az aks update -n MyKubernetesCluster -g AZ500LAB09 --attach-acr $ACRNAME```
_This command grants the 'acrpull' role assignment to the ACR. It may take a few minutes for this command to complete._
2. In the Bash session within the Cloud Shell pane, run the following to grant the AKS cluster the Contributor role to its virtual network.
   ```RG_AKS=AZ500LAB09```
   ```RG_VNET=MC_AZ500LAB09_MyKubernetesCluster_eastus2```
   ```AKS_VNET_NAME=aks-vnet-30198516```
   ```AKS_CLUSTER_NAME=MyKubernetesCluster```
   ```AKS_VNET_ID=$(az network vnet show --name $AKS_VNET_NAME --resource-group $RG_VNET --query id -o tsv)```
   ```AKS_MANAGED_ID=$(az aks show --name $AKS_CLUSTER_NAME --resource-group $RG_AKS --query identity.principalId -o tsv)```
   ```az role assignment create --assignee $AKS_MANAGED_ID --role "Contributor" --scope $AKS_VNET_ID```

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 5: Deploy an external service to AKS**
_In this task, you will download the Manifest files, edit the YAML file, and apply your changes to the cluster._

1. In the Bash session within the Cloud Shell pane, click the Upload/Download files icon, in the drop-down menu, click Upload, in the Open dialog box, navigate to the location where you downloaded the lab files, select **\Allfiles\Labs\09\nginxexternal.yaml** click Open. Next, select **\Allfiles\Labs\09\nginxinternal.yaml**, and click **Open**.
2. In the Bash session within the Cloud Shell pane, run the following to identify the name of the Azure Container Registry instance: ```echo $ACRNAME```
_Record the Azure Container Registry instance name. You will need it later in this task._
3. In the Bash session within the Cloud Shell pane, run the following to open the nginxexternal.yaml file, so you can edit its content.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 6: Verify the you can access an external AKS-hosted service**


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 7: Deploy an internal service to AKS**


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Task 8: Verify the you can access an internal AKS-hosted service**

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
