# Exercise 1: Enable JIT on your VMs from Azure virtual machines
> If you receive the error Error enabling just-in-time access please note that it can take as long as 30 minutes or more for the backend processes to 'onboard' Microsoft Defender for Cloud such that this will succeed.
> You can enable JIT on a VM from the Azure virtual machines pages of the Azure portal.

1. In the search box at the top of the portal, enter virtual machines. Select Virtual machines in the search results.
2. Select myVM.
3. Select Configuration from the Settings section of myVM.
4. Under Just-in-time VM access, select Enable just-in-time.
5. Under Just-in-time VM access, click on the link that reads Open Microsoft Defender for Cloud.
6. By default, just-in-time access for the VM uses these settings:
   - Windows machines
     - RDP port: 3389
     - Maximum allowed access: Three hours
     - Allowed source IP addresses: Any
    - Linux machines
      - SSH port: 22
      - Maximum allowed access: Three hours
      - Allowed source IP addresses: Any
7. By default, just-in-time access for the VM uses these settings:
   - From the Configured tab, right-click on the VM to which you want to add a port, and select edit. <br> <img width="4410" height="2001" alt="image" src="https://github.com/user-attachments/assets/9fa7e825-9667-435a-8a46-b24cc17df3da" />
   - Under JIT VM access configuration, you can either edit the existing settings of an already protected port or add a new custom port.
   - When you've finished editing the ports, select Save.


# Exercise 2: Request access to a JIT-enabled VM from the Azure virtual machine's connect page.
> When a VM has a JIT enabled, you have to request access to connect to it. You can request access in any of the supported ways, regardless of how you enabled JIT.

1. In the Azure portal, open the virtual machines pages.
2. Select the VM to which you want to connect, and open the Connect page.
   - Azure checks to see if JIT is enabled on that VM.
     - If JIT isn't enabled for the VM, you're prompted to enable it.
     - If JIT is enabled, select Request access to pass an access request with the requesting IP, time range, and ports that were configured for that VM. <br> <img width="4410" height="1995" alt="image" src="https://github.com/user-attachments/assets/20aae84f-c318-4b29-8cca-9ce52a2b8582" />

> **Results**: You have explored various methods on how to enable JIT on your VMs and how to request access to VMs that have JIT enabled in Microsoft Defender for Cloud.



