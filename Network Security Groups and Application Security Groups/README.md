**Remember to remove any newly created Azure resources that you no longer use. Removing unused resources ensures you will not incur unexpected costs.**

1. Open the Cloud Shell by clicking the first icon in the top right of the Azure Portal. If prompted, select PowerShell and No storage account required, select the name of your subscription, and then select Apply.
2. Ensure PowerShell is selected in the drop-down menu in the upper-left corner of the Cloud Shell pane.
3. In the PowerShell session within the Cloud Shell pane, run the following to remove the resource group you created in this lab: ```Remove-AzResourceGroup -Name "AZ500LAB07" -Force -AsJob```
4. Close the Cloud Shell pane.
