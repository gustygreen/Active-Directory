<p align="center">
<img src="https://github.com/user-attachments/assets/7a73b456-adac-4f3b-ac4a-b09f282f134f" height="30%" width="30%"/>
</p>

<h1>Create an Active Directory Domain</h1>
In this tutorial, we create an Active Directory Domain joining a Windows client to the Domain Controller.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Virtual Network inside Azure Resource Group
- Powershell

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)-Client 1
- Windows Server- DC-1(Domain Controller)

<h2>Actions and Observations</h2>

<p>
<img src="https://github.com/user-attachments/assets/70f2f67d-7876-4788-9802-a6119c9efd16" height="80%" width="80%"/>
</p>

<p>
Create a Resource Group, as seen [here](https://github.com/gustygreen/Azure). Create and add a Virtual Network. Create and add the Domain Controller. Create and add the Client.<br />
<p>

<h2> Create a Virtual Network</h2>

<p>
<img src="https://github.com/user-attachments/assets/6c93cd1b-c8c3-4828-855b-b748dc9b76a2" height="80%" width="80%"/>

Select Virtual Network.
</p>



<p>
<img src="https://github.com/user-attachments/assets/ab58633b-7ade-43e2-89ec-e7562d73446c" height="50%" width="50%"/>

Add the Virtual Network to the Resource Group. Name it. Verify it's in the same Region as the Resource Group. Review and Create.
</p>
 
<h2> Create the Domain Controller(DC-1)</h2>
<p>
<img src="https://github.com/user-attachments/assets/64617047-3cfb-46e7-bf73-2bf80954640f" height="50%" width="50%"/>

Create a new Virtual Machine for the Domain Controller. Name it(1). Verify it's in the correct Resource Group(2). Verify it's in the same Region as the Resource Group(3). Make sure that the Image is Windows Server 2022 DataCenter(4).
</p>

<p>
<img src="https://github.com/user-attachments/assets/b6341e2a-108c-4820-83cf-09b1179f0aa2" height="50%" width="50%"/>

Verify that the Server has a decent size 2vncpus and 8Gb is fine. Add a user and password. Select Next:Disks 
</p>
<p>
<img src="https://github.com/user-attachments/assets/caf60678-7af9-4781-9ea8-e75c11227682" height="50%" width="50%"/>

Select Next:Networking
</p>

<p>
<img src="https://github.com/user-attachments/assets/875282ac-19a8-4b80-b74e-fa2a385780e4" height="50%" width="50%"/>

Place the Server in the Active-Directory-VNet. Review and Create
</p>

When Azure has completed Verifying, Select Create. This will create the new Domain Controller in our Resource Groups Virtual Network.

<h2> Create the Client(Client-1)</h2>

<p>
<img src="https://github.com/user-attachments/assets/22d1b2cf-00a8-4ff4-8ffd-b597048afe96" height="50%" width="50%"/>

We will go through the same process as creating the Domain Controller except that for the Image we will use Windows 10 Pro(22H2). We will name the VM client-1.

<img src="https://github.com/user-attachments/assets/555378f6-55e1-4790-91e0-9e838e436ade" height="50%" width="50%"/>

We verify that the size of the image is good, give it a user, password, and check the Licensing. Review and Create
</p>

When Azure has completed Verifying, Select Create. This will create the new Client in our Resource Groups Virtual Network.

Our Resource Group is now setup with a Virtual Network, Domain Controller, and Client.

<h2>Set DC-1 to have Static IP address</h2>
This is to prevent Azure from resetting the Private IP address if the server is turned off. We are using the DC as a DNS server.

<p>
<img src="https://github.com/user-attachments/assets/eb2f697c-17cf-41fa-a9be-d394e56155b7" height="50%" width="50%"/>

In Azure go to the DC-1 VM-Networking-Network settings-Configure the virtual NIC.
</p>

<img src="https://github.com/user-attachments/assets/6e995ea8-1fb2-4b66-8877-103895881110" height="50%" width="50%"/>

Select ipconfig-Static-Save

<p>
<img src="https://github.com/user-attachments/assets/0de78f43-554b-499b-a50d-25269e5907fc" height="50%" width="50%"/>

Verify that the Private IP Address shows as Static.
</p>

<h2>Disable Domain Controller Firewall</h2>

<p>
<img src="https://github.com/user-attachments/assets/0db3d3c3-c605-41d6-ae83-782fe21a66f8" height="50%" width="50%"/>

RDP to the Domain Controller.
</p>

<p>
<img src="https://github.com/user-attachments/assets/76911fdf-de7f-4117-bacc-fe2fcc6c2b84" height="50%" width="50%"/>

 Select Run-fw.msc
</p>

<p>
<img src="https://github.com/user-attachments/assets/dc4e7c19-0486-4fc9-95f4-efdeb9fdcf4c" height="50%" width="50%"/>

 Select Windows Defender Firewall Properties-Change Firewall state to Off-Apply-OK. (Turn this off for Domain, Private, and Public Profiles).
</p>

<h2>Set Client to point to DNS on Domain controller</h2>

<p>
<img src="https://github.com/user-attachments/assets/98a7f80d-37e6-430a-a48e-678df487dad4" height="50%" width="50%"/>

 Go to client-1 in Azure-Network settings-Virtual NIC
</p>

<p>
<img src="https://github.com/user-attachments/assets/0f243259-0327-4669-927c-7a5469608238" height="50%" width="50%"/>

 Select DNS servers. Change DNS servers to Custom. Put in the Domain Controllers Private IP address for the DNS server. Save.
</p>

<img src="https://github.com/user-attachments/assets/2507468f-6cfd-445a-b5c2-38d0c774c1d8" height="50%" width="50%"/>

In Azure, Restart client-1 for the DNS info to take affect.

<h2>Verify connection between DC and Client</h2>
<p>
<img src="https://github.com/user-attachments/assets/60f0318e-42e9-42f1-9c57-0a2a251e6b7e" height="50%" width="50%"/>

RDP to client-1. Verify that you can ping DC-1(10.0.0.4)
</p>

<p>
<img src="https://github.com/user-attachments/assets/3c9f77ab-59cb-4c85-af43-d229292923b9" height="50%" width="50%"/>

Run ipconfig /all. Verify tthat the DNS Servers is pointing to the Domain Controller(10.0.0.4).
</p>
