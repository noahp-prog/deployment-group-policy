<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Using GPO's to deploy software and change user wallpaper (ADDS)</h1>
This guide outlines two simple use cases of Group Policy within an Active Directory.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop (RDP)
- Active Directory Domain Services (ADDS)
- Group Policy
- Command Prompt (CMD)

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create shared folder
- Create Group Policy Objects (GPOs)
- Chanage wallpaper
- Deploy Software
- Observe changes on client-1

# Deployment Steps </b>

First, on your Domain Controller, create a folder and drag the wallpaper you'd like to use into it.</p>
We're going to share this folder over the network.</p>
Make not of the path, we're going to need it.

![image](https://github.com/user-attachments/assets/f61ad5bc-753d-4965-bd6f-2f4389443698)

![image](https://github.com/user-attachments/assets/66d7d0eb-9850-4dc5-b8fd-7d2ae9a7979a)

Next, go into the security permissions for the folder and add "**Authenticated Users**"

![image](https://github.com/user-attachments/assets/28191a94-6367-4d57-a876-ec4b151ad7c8)

Open run, and type "**gpmc.msc**"

![image](https://github.com/user-attachments/assets/d3dc02d6-ed1c-4477-b7cf-30b8062e7e88)

We're now going to create a new GPO under "**_EMPLOYEES**", I named mine "Wallpaper".

![image](https://github.com/user-attachments/assets/9ee5b5f0-ecde-4d7b-9cc0-f80ae01a86b7)

Right click the GPO you just created and click edit.</p>
Navigate to this path







