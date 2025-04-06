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

Now log into a user on client-1.</p>
I chose a different user from the 1000 that we created in the previous guide.

![image](https://github.com/user-attachments/assets/9d8f956b-2b77-4ccc-a7fc-2de46226e540)

After logging into client-1, our wallpaper should now be changed.

![image](https://github.com/user-attachments/assets/9a2b14fb-04ad-4388-b6b9-2e89c0fc2b07)

# Deploying Software</b>

Back on our Domain Controller, create a file and drag your msi package into the folder.</p>
I'm going to be installing Google Chrome. In order for this to work the file type *MUST* be an msi package.

![image](https://github.com/user-attachments/assets/95c67699-631f-45b1-b519-d1b65747d341)

Share the folder over the network. In permission for the share, add "**Authenticated Users**", and remove "**Everyone**"

![image](https://github.com/user-attachments/assets/41706e29-f326-4302-b688-287056e0fbdd)

![image](https://github.com/user-attachments/assets/15bc14e8-13cd-4004-80c8-b164885bdb31)

Make note of the network share path.

![image](https://github.com/user-attachments/assets/a5e40475-4853-4d8b-8de7-2b930611aba9)

In the security permissions for the folder, add "**Authenticated Users**"

![image](https://github.com/user-attachments/assets/8f9af453-f308-4f74-87b4-60d9cf2d38cf)

In run, type "**gpmc.msc**"

![image](https://github.com/user-attachments/assets/0c291fd4-e267-4212-a306-89d7fc42017c)

Inside Group Policy Managment, right click your domain name and add a new GPO.</p>
I named mine, Chrome Deployment.

![image](https://github.com/user-attachments/assets/09ad9fac-5aa6-4e7e-9672-61dd4ec12fe7)

Right click and click edit on the new GPO, navigate to this path and click "**Software Installation**"

![image](https://github.com/user-attachments/assets/99cfdcb0-9dc6-405f-bc31-f003451b1551)

Paste the path from the netowrk folder share, and add <\filename.msi></p>
In my case, it's "chrome.msi"

![image](https://github.com/user-attachments/assets/37d1c508-739f-4dd6-ad1c-9920385dee18)

When prompted, choose "**Assigned**"</p>
Then right click and select properties and enable the following option:</p>
"Uninstall this application when it falls out of the scope of
management"

![image](https://github.com/user-attachments/assets/fbd67dfb-14d8-443c-97d4-3a8e0491bb43)

We're now going to log into client-1.

![image](https://github.com/user-attachments/assets/da050f30-550f-42ba-82d2-6ec53b239d44)

Notice how the software is not installed. This is because we haven't updated the policy on client-1.</p>
To do this, open cmd, and type the following command: "**gpupdate /force**"</p>

![image](https://github.com/user-attachments/assets/3c9708e9-b8bf-4dfc-9f7f-ffe9a90564d7)

This will force an update to the policy, and prompt you to restart the computer. When prompted, type "**y**"

![image](https://github.com/user-attachments/assets/7c314570-bc1e-45a6-8823-f83bfe15bb11)

After the computer is restarted, log back into client-1 and observe how chrome is installed!

![image](https://github.com/user-attachments/assets/f00a7b84-4655-49e8-94f4-4ccb81f4c9db)























