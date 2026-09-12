**Remember to remove any newly created Azure resources that you no longer use. Removing unused resources ensures you will not incur unexpected costs.**
1. In the Azure portal, open the Cloud Shell by clicking the first icon in the top right of the Azure Portal.
2. In the drop-down menu in the upper-left corner of the Cloud Shell pane, select PowerShell, and, when prompted, click Confirm.
3. In the PowerShell session within the Cloud Shell pane, run the following to remove the resource group you created in this lab: ```Remove-AzResourceGroup -Name "AZ500LAB01" -Force -AsJob```
