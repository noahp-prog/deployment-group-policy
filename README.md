<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Using GPOs to deploy software and change users wallpaper (ADDS)</h1>
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

# Changing Wallpaper</b>

First, on your Domain Controller, create a folder and drag the wallpaper you'd like to use into it.</p>
We're going to share this folder over the network.</p>
Make note of the path, we're going to need it.

![image](https://github.com/user-attachments/assets/f61ad5bc-753d-4965-bd6f-2f4389443698)

![image](https://github.com/user-attachments/assets/66d7d0eb-9850-4dc5-b8fd-7d2ae9a7979a)

Next, go into the security permissions for the folder and add "**Authenticated Users**"

![image](https://github.com/user-attachments/assets/28191a94-6367-4d57-a876-ec4b151ad7c8)

Open run, and type "**gpmc.msc**"

![image](https://github.com/user-attachments/assets/d3dc02d6-ed1c-4477-b7cf-30b8062e7e88)

We're now going to create a new GPO under "**_EMPLOYEES**", I named mine "Wallpaper".

![image](https://github.com/user-attachments/assets/9ee5b5f0-ecde-4d7b-9cc0-f80ae01a86b7)

Right click the GPO you just created and click edit.</p>
Navigate to this path, and choose "**Desktop Wallpaper**"

![image](https://github.com/user-attachments/assets/80cf8cb7-3da7-4bd7-a30f-1e19b0024c04)

Click Enabled, select how you'd like the wallpaper to be displayed, then paste the path from the network share followed by the name of your wallpaper.<ext>.</p>
My wallpaper is a jpg file, so my file path is: **\\dc-1\wallpaper\wallpaper.jpg**

![image](https://github.com/user-attachments/assets/04cfb3e2-bae5-406f-bcb3-ffedbc06790e)

Now log into your user on client-1.</p>
I chose a different user from the 1000 that we created in the previous guide.

![image](https://github.com/user-attachments/assets/9d8f956b-2b77-4ccc-a7fc-2de46226e540)

After logging into our user, our wallpaper should now be changed.

![image](https://github.com/user-attachments/assets/9a2b14fb-04ad-4388-b6b9-2e89c0fc2b07)














