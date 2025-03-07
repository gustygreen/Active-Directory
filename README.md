<p align="center">
<img src="https://github.com/user-attachments/assets/e0a11840-0c5b-4aee-800b-031bb0a48fd1" height="30%" width="30%"/>
</p>

<h1>Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we analyze various network traffic flows to and from Azure Virtual Machines using Wireshark.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Windows and Linux Command Line Tools
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Ubuntu Server 22.04

<h2>Actions and Observations</h2>

<p>
<img src="https://github.com/user-attachments/assets/1feffac1-bcc7-40e8-bd70-7fe4d38baaae" height="80%" width="80%"/>

</p>
<p>
Create two VMs in the Azure portal: one using a Windows 10 Pro image and the other using a Linux image, each with 2 vCPUs. Ensure both VMs are attached to the same virtual network during setup. Use RDP to access the Windows machine.
</p>
<br />
