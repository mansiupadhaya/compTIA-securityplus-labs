# 1 - Exploring the Lab Environment

### Objective
Getting familiar with the lab interface, tools and virtual machines (Windows and Kali Linux) that will be used 
throughout the Security+ lab series. The goal here is to understand how to navigate, 
interact with, and get the most out of the virtual lab setup.

### Overview
This lab was mostly foundational and the focus was on learning how to use the virtual lab environment efficiently, 
including the layout, navigation controls, and general interaction patterns with the VMs.
There are 2 main VMs used throughout the course:
* PC10 (Windows Server 2019) - acting as a Windows client
* KALI - running Kali Linux, a distribution I'm already pretty familiar with

### Lab Interface Familiarisation
The lab runs inside the browser, giving you access to VMs through a cloud platform. A few things I picked up 
while getting oriented:
* Tabs to know:
   - Instructions: Step-by-step lab guide with progress checkboxes
   - Resources: List VMs, credentials, and tools available
   - Help: Support, technical info, and troubleshooting tips
 
* Controls worth noting:
   - Full-screen mode is your best friend (much easier to work that way)
   - The Commands menu lets you send keyboard shortcuts (like Ctrl+Alt+Del) and also paste credentials into the VM
   - You can save and resume labs if needed, but keep an eye on the timer since once it runs out, the session restarts (I found that out the hard way)
 
### 💻 Exploring the Windows VM
<img width="512" height="401" alt="image" src="https://github.com/user-attachments/assets/c27cbfca-2408-4607-9287-db0a6d51b598" />

I loggeed into the Windows Server 2019 machine (PC10) using the credentials provided and tested basic interaction:
* Used PowerShell in admin mode
* Ran a couple commands like ``mkdir`` and ``Get-Date``
* Practiced using the TypeText feature (which can auto-send text to the VM from the interface)
The VM essentially behaves like a typical Windows environment, with the exception of it being cloud-hosted, but
nothing out of the ordinary.

### 🐧 Exploring the Kali VM
<img width="765" height="578" alt="image" src="https://github.com/user-attachments/assets/c1bef1a3-0f6f-46d1-b344-1731d5ec36ee" />
Since I've been using Kali for a while, this part was more familiar territory. Still, good to get a feel for how it behaves in this virtual setup.

A few things I did:
* Logged in as root and opened up a terminal
* Ran some basic commands like ``pwd``, ``ip a``, and ``hostname`` 
* Got a refresher on navigating Kali's desktop environment (GNOME), switching workspaces, using the terminal, etc

Unlike the Windows VM, the Kali VM doesn't support the TypeText feature, so commmands need to be entered manually, which isn't a huge deal

### My Final Thoughts
Overall, this lab served as a great introduction to the environment and helped me get familiar with the features provided in CompTIA's virtual setup. I'm keen 
to work my way through the rest of the labs.
