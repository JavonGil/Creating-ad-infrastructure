<table>
  <tr>
    <td>
      <img width="1000" alt="ADS1" src="https://github.com/user-attachments/assets/6764e034-271e-4809-8e91-bb25dba7ba17" />
    </td>
    <td>
      <img width="1000" alt="ADS2" src="https://github.com/user-attachments/assets/2dfb8569-f306-4f94-a01a-6790869d3475" />
    </td>
  </tr>
</table>

<h1>Creating Active Directory Infrastructure in Azure</h1>
This tutorial outlines the creation of an Active Directory infrastructure within Azure. We will use this build to deploy and configure Active Directory in a future project. <br />

<h2>⚠️ Prerequisite</h2>

- [Creating Virtual Machines in the Cloud](https://github.com/JavonGil/Creating-VM-S)
<p>(Reference this project for help creating Virtual Manchines if needed.)</p>

<h2>💻 Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>🖥️ Operating Systems Used </h2>

- macOS Sequoia
- Windows Server 2022
- Windows 10 (21H2)


<h2>⚙️ Deployment and Configuration Steps</h2>

<p>
<img width="1247" alt="Screenshot 2025-06-04 at 3 00 03 PM" src="https://github.com/user-attachments/assets/f4b882e5-2bec-4e23-87fe-a9746917784b" />

</p>

<p>
- In Azure, create a new Resource Group and two Virtual Machines. Ensure the VMs are in the same Virtual Network and Region. Reference the project above in Prerequisites if you need a quick reminder.
<p>- Name the first VM "DC-1" (Domain Controller), set the image to Windows Server 2022, and at least (2 vcpus, 8 GiB memory).</p>
<p>- Name the second VM "Client-1", set the image to Windows 10, and at least (2 vcpus, 8 GiB memory).</p>
<p>- This would be a good time to write the Public IP addresses of both VMs and the Private IP for DC-1. We will need them later for RDP.</p>
<br />

<p>
<img width="1512" alt="Screenshot 2025-06-04 at 3 01 18 PM" src="https://github.com/user-attachments/assets/4bc1b949-5062-4aaf-b081-76b59468d5ef" />
</p>

<p>
- From Virtual machines, click on DC-1 and select Network settings. Then, click on Network interface / IP configuration as shown in Figure 2.
</p>
<br />

<p>
<img width="850" alt="AD10" src="https://github.com/user-attachments/assets/cc03b9ca-0954-4762-a004-75a2908508f4" />
<p>
- In IP configurations, locate and click on "ipconfig1". Under Private IP address settings, change Allocation to "Static". Click Save. (Note the Private IP while we're here if you forgot earlier).
<p>- We set the Private IP to Static because we do not want this IP address to change. Dynamic = Constantly changing and Static = Stay same. DC-1 will be our Server for upcoming AD Projects. 
</p>
<br />

<p>
<img width="1512" alt="Screenshot 2025-06-04 at 3 03 23 PM" src="https://github.com/user-attachments/assets/5aa4b72d-c965-4040-b6f0-f655293f5a54" />
 </p>
<p>
-You will be back in the IP configurations screen after clicking Save. Here, we can confirm our changes were saved by looking next to the Private IP address.
</p>
<br />

<p>
<img width="593" alt="Screenshot 2025-06-04 at 3 33 01 PM" src="https://github.com/user-attachments/assets/4aa092d5-830d-44e9-9ea5-44480b638b57" />
 </p>
<p>
- Minimize Azure for now and hop over to Remote Desktop (Windows) or Windows App (MacOS). Use DC-1's Public IP address and create a new RDP connection.
<p>- Once logged into DC-1, right-click the Start Menu and open Run. Type in wf.msc and click OK.</p>
<p>- This will open the firewall settings for DC-1. (NOTE: Server Manager Dashboard should showing once logged into DC-1. If not, or if Windows is showing as normal, there is an issue. Make sure you are in the right VM and/or check Azure to verify the DC-1 VM was setup correctly).</p>
</p>
<br />

<table>
  <tr>
    <td>
      <img width="1036" alt="Screenshot 2025-06-04 at 3 07 15 PM" src="https://github.com/user-attachments/assets/63d9de34-cae9-4357-a882-59dc6bbcef16" />
    </td>
    <td>
      <img width="1034" alt="Screenshot 2025-06-04 at 3 07 43 PM" src="https://github.com/user-attachments/assets/1f1e46ad-3786-47f1-9a9c-3c8fe60647c5" />
    </td>
  </tr>
</table>
<p>
  -Select Windows Defender Firewall Properties. Then for Domain, Private, and Public Profiles, change Firewall state to Off. (You will need to do this for each tab). Click Apply and then OK to save the changes.
</p>
<br />

<table>
  <tr>
    <td>
      <img width="1512" alt="Screenshot 2025-06-04 at 3 08 49 PM" src="https://github.com/user-attachments/assets/64fef3d2-8d56-459a-a744-8d587a4a0a08" />
    </td>
    <td>
      <img width="1512" alt="Screenshot 2025-06-04 at 3 10 41 PM" src="https://github.com/user-attachments/assets/dff76fec-0b44-4ad5-af67-1b36d47d5c01" />
    </td>
  </tr>
</table>
<p>
  - Head back to Azure and go to Virtual machines. Click on Client-1. Select Network settings and then Network inferace / IP configuration. See Figure 8.
</p>
<p>
  - Select DNS servers. Click Custom and enter DC-1's Private IP under DNS Server.(Good thing we noted the IPs earlier.😁) Click Save. See Figure 9.
</p>
<br />

<p>
<img width="1512" alt="Screenshot 2025-06-04 at 3 12 03 PM" src="https://github.com/user-attachments/assets/179dcab0-12bf-4642-8ac4-6cc951685268" />
 </p>
<p>
- Since we changed the DNS Server for Client-1, we need to restart the VM. Run,🏃‍♂️, back to the Virtural machines main screen and restart Client-1.  
</p>
<p>- Check the box next to Client-1, click Restart, and tell Azure Yes.</p>
<br />

<p>
<img width="786" alt="Screenshot 2025-06-04 at 3 15 24 PM" src="https://github.com/user-attachments/assets/f1dc500c-a285-4391-9d77-e94dab8e1f0c" />
 </p>
<p>
- Once Client-1 finishes restarting, grab your notes with the Public IP adrresses, and use Client-1's Public IP to login using RDP. (Don't forget username and password.) 😉</p>
<p>-After you get logged in to Client-1, open up PowerShell. </p>
<br />

<p>
<img width="494" alt="Screenshot 2025-06-04 at 3 17 24 PM" src="https://github.com/user-attachments/assets/a6876cf8-6d26-4ccf-9059-43bad609656f" />
 </p>
<p>
- From PowerShell, we are going to test our connection from Client-1 to DC-1 (Our Server) with command ping 10.0.0.4 and press enter. This shows us that both VMs are on the same Virtual Network and we disabled DC-1's firewall correctly.
</p>
<br />

<p>
<img width="582" alt="Screenshot 2025-06-04 at 3 18 48 PM" src="https://github.com/user-attachments/assets/7807a0fc-16f4-4206-9476-cb9fd0df6e98" />
 </p>
<p>
- Now for our final act of the eveving, we will make sure the DNS Server of Client-1 is set to DC-1's Private IP address. In PowerShell use the command ipconfig /all and press enter.
</p>
<br />

<h2>✅ Conclusion</h2>

<p>
And that’s it. You just set up a solid cloud setup for running Active Directory inside Azure.
With just a couple of VMs and the right settings, you now have your own little network running in the cloud no wires, no desks, no stress.
Don’t forget to Stop your VMs when you’re done so Azure doesn’t keep charging you.
Appreciate you for rocking with the project. We’ll catch you in the next one 😎   
</p>
<br />
