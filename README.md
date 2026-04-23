# Gameserver-Hosting-On-Ubuntu
This project provides a comprehensive, enterprise-grade guide for hosting a high-performance Minecraft server on Ubuntu 24.04 LTS. It focuses on maximizing resource efficiency, professional-grade monitoring, and secure networking without the need for traditional port forwarding.

1	WHY LINUX IS THE STANDARD FOR MINECRAFT HOSTING?

Running a Minecraft server on Linux provides a leaner, more stable environment compared to Windows. By eliminating the graphical overhead and prioritizing process efficiency, Linux ensures that your hardware is focused on one thing: maintaining 20 Ticks Per Second (TPS).

1.1	Resource Efficiency & Performance

Windows environments are built for user interaction, which means they carry significant "bloat” background services, telemetry, and a mandatory Graphical User Interface (GUI).

•	Headless Advantage: Most Linux servers run "headless" (command-line only). This frees up hundreds of megabytes of RAM and significant CPU cycles that would otherwise be wasted on rendering a desktop.

•	Java Optimization: Linux manages Java threads more natively, often resulting in lower "garbage collection" spikes and smoother gameplay for your players.


1.2	Professional Management Tooling

Linux is the native home of modern DevOps tools. If you plan on scaling your community, Linux provides the infrastructure to do it properly.

•	Containerization: Using Docker allows you to "wrap" your server in a consistent environment, making backups, migrations, and deployments effortless.

•	Automation: Through Bash scripting and Cron jobs, you can automate everything from world backups to auto-restarts and plugin updates.

1.3	Cost-Effectivness

Simply put, Linux is free. Windows Server licenses can add a significant "tax" to your hosting costs. By choosing Linux, every dollar / euro of your budget goes directly toward better hardware—faster CPUs and NVMe storage—rather than software licensing.
 

2	TESTING OUT IN VIRTUALBOX

2.1	What is Virtualbox & Virtual Machine?

Oracle VirtualBox is a free, open-source hypervisor that enables users to run multiple, separate operating systems (guests) simultaneously on a single physical computer (host). It creates virtual machines (VMs) that simulate hardware, allowing, for example, Linux or Windows to run inside a window on a macOS desktop. A virtual machine (VM) is a software-based emulation of a physical computer that runs on a host machine, acting as an isolated "guest" computer with its own CPU, memory, and storage

Key Features and Uses:
•	Cross-Platform: Runs on Windows, Linux, macOS, and Solaris hosts.

•	Versatility: Supports a wide range of guest operating systems, including older versions.

•	Snapshot System: Users can create snapshots to save the state of a VM, allowing them to revert to a previous state instantly.

•	Isolated Environment: Guest OSs are completely isolated from the host machine, making it ideal for testing software or running suspicious applications safely.

•	Hardware Virtualization: Uses modern CPU features to provide near-native performance. 


2.2	Setting up ubuntu VM

2.2.1	What is ubuntu?

Ubuntu is a free, open-source Linux operating system based on Debian, known for its user-friendliness, stability, and security. Developed by Canonical and a global community, it is popular for desktops, servers, cloud computing, and IoT. It offers a modern interface, pre-installed apps, and is widely used by developers.

2.2.2	Download Ubuntu Server version 24.04.4 LTS

Before starting anything you need to download the file from theyr official site: https://ubuntu.com/download/server
The latest LTS version of Ubuntu Server. LTS stands for long-term support — which means five years of free security and maintenance updates, extended to up to 15 years with Ubuntu Pro.

2.2.3	Setting up Ubuntu Server Virtual Machine

We start with creating a new virtual machine, so for that press New -> name it wathever and set Type and Version to Linux and Ubuntu (64-bit).
I recommend for smoother experience to use 2 vCPUs (Processors)  and  3GB  or 3072 MB (im going to use 8GB). For disk size it is recommended 25GB to 50GB.
<img width="945" height="580" alt="image" src="https://github.com/user-attachments/assets/86faaec9-701d-4536-b616-6222327df8ff" />

 
Now that we have it setup, we need to insert the server iso file into this vm. For that navigate to Storage -> Controller: IDE -> Empty disk  and on the right side next to Optical Drive theres a blue disk, click on it and choose  ubuntu-24.04.4-live-server-amd64.
<img width="622" height="448" alt="image" src="https://github.com/user-attachments/assets/f37ecd7d-16a4-4e28-acfe-61125ce3cd32" />

 
And in Network  set you’re Adapter 1 to Bridged Adapter.
 <img width="625" height="456" alt="image" src="https://github.com/user-attachments/assets/e6d1b033-7aad-4731-915a-42c9a1357727" />


2.3	Install the machine

Choose your language
 <img width="945" height="329" alt="image" src="https://github.com/user-attachments/assets/49625e54-4e2f-4299-90f7-50e7d343cf38" />

For the type of installation choose only Ubuntu Server
 <img width="945" height="529" alt="image" src="https://github.com/user-attachments/assets/da73b545-ab45-4eff-b712-0ea21983ddbb" />

It should give your machines DHCPv4 
 <img width="945" height="506" alt="image" src="https://github.com/user-attachments/assets/345f8ce8-be96-4074-a35e-045c77797322" />

No need to put anything in Proxy configuration

 
Dont change anything here since we already made a disk.
 <img width="945" height="498" alt="image" src="https://github.com/user-attachments/assets/62569446-737c-4828-a025-55363d8a3c4b" />

Setup your server’s name, password etc...
 <img width="945" height="235" alt="image" src="https://github.com/user-attachments/assets/ba3033fd-7b03-40c5-b612-dbb26172c31d" />

You can choose, if you want Ubuntu Pro since its free for personal use ( 1 to 5 machines)
 <img width="945" height="176" alt="image" src="https://github.com/user-attachments/assets/c2509b67-e651-41ef-a643-d92b321b6738" />

Install OpenSSH server so you could use ssh  command to easily use the machine in windows cmd for example.
 <img width="945" height="127" alt="image" src="https://github.com/user-attachments/assets/fd24a96f-f2d1-4a15-877c-2f896949e246" />

We’re not choosing any Featured server snaps, so you can just press Done.
Now wait for the machine to install and press Reboot Now  when its done. 
After its done rebooting press Enter on your keyboard
Login to your machine
 <img width="945" height="511" alt="image" src="https://github.com/user-attachments/assets/ba0caa5e-d22a-4479-bd07-fff10033dbfe" />

2.3.1	What is  Gnome?

GNOME (GNU Network Object Model Environment) is the default graphical user interface (desktop environment) for Ubuntu. It provides the visual, interactive experience—windows, icons, top panel, and app launcher—allowing users to manage files, applications, and settings in a modern, clean, and distraction-free workspace.

2.3.2	Installing Gnome

First of all we are going to update our systems package list using command: sudo apt update.
If you dont want to always insert your password after using sudo just log into the administrator account using command  sudo su.
 <img width="945" height="265" alt="image" src="https://github.com/user-attachments/assets/a9c40c5c-a467-488a-a8c9-a250c0e28858" />


After updating we’re gonna use command sudo apt install ubuntu-gnome-desktop
Press  Y  to continue
After the installation completed use command Reboot to reboot the virtual machine.
And now our Ubuntus Interface should look like this.
 <img width="945" height="484" alt="image" src="https://github.com/user-attachments/assets/db5ef8c4-830b-4f10-9755-fc6d8813a170" />

And when you login
 <img width="945" height="501" alt="image" src="https://github.com/user-attachments/assets/d37883b6-83e1-4a24-8963-ffedf93cdfb0" />

 

3	SETTING UP MONITORING SOFTWARE

3.1	What is monitoring software?

Monitoring software is a category of tools designed to track, record, and analyze activity on computers, networks, or applications. It acts as a surveillance or diagnostic system, reporting data like user actions, bandwidth usage, or system uptime to administrators to ensure productivity, security, and performance.

3.1.1	Zabbix & Installation

Zabbix is a free, open-source enterprise-level monitoring solution designed to monitor IT infrastructure, including networks, servers, virtual machines, cloud services, and applications in real-time. It enables proactive IT management by collecting metrics via agents, SNMP, or APIs, providing alerting, visualization, and automated network discovery, often used to prevent downtime. 
First things first go to this website:
https://www.zabbix.com/download?zabbix=7.0&os_distribution=ubuntu&os_version=24.04&components=server_frontend_agent&db=mysql&ws=apache

And under Product we’re gonna choose Zabbix Packages. For platform choose options from the picture below.
 <img width="945" height="406" alt="image" src="https://github.com/user-attachments/assets/2601faa8-fc0c-440b-8fdb-fded0b61689b" />

Install Zabbix repository using following commands:
 <img width="945" height="111" alt="image" src="https://github.com/user-attachments/assets/ef9a90d2-afc3-4087-b73e-76fd558f2ac0" />

After installing Zabbix repository we’re gonna have to also install Zabbix server, frontend and agent 2. 
 <img width="945" height="81" alt="image" src="https://github.com/user-attachments/assets/e3f7d8ba-14cc-400c-b627-f3676279a480" />





3.2	What is Database?

A database is a structured, electronically stored collection of data designed for rapid searching, management, and updating. It acts as a digital repository, organizing information into formats like tables (rows/columns) or documents to allow multiple users to efficiently access, secure, and manipulate data.

3.2.1	Why Use a Database?

Databases are essential for modern applications, including online banking, e-commerce stores, social media platforms, and large-scale, enterprise applications. They offer significant advantages over simple file storage, such as improved data integrity, simultaneous multi-user access, enhanced security, and rapid retrieval.

3.2.2	Before installing MySQL

Separate your VMs. Host the Minecraft Server and Zabbix Agent on one instance, and the Zabbix Server and SQL Database on a second instance.

The Reasoning:

•	Performance: Minecraft relies on consistent "ticks." Database housekeeping (SQL writes/logs) causes micro-stuttering and TPS drops if hosted on the same CPU or Disk.

•	Stability: If the monitoring database fills the disk or crashes the OS, your game world remains online and uncorrupted.

•	Simplicity: Using a lightweight Zabbix Agent on the game server captures all necessary metrics (RAM, CPU, player counts) without the heavy resource footprint of the full Zabbix suite.


The Goal:

Zero-lag monitoring. You get professional-grade observability without sacrificing the player experience.

3.2.3	MySQL & Installation
Create another Ubuntu 24.04 server for monitoring. There we will only install Zabbix Server and Database (MySQL) and on the Virtual Machine where we’re hosting minecraft we will only install the Zabbix Agent 2. All the command you will find on the zabbix product download page.
 <img width="945" height="99" alt="image" src="https://github.com/user-attachments/assets/8026eb9a-ade6-4f6b-b43b-f13f922e75f3" />

MySQL is a popular, open-source Relational Database Management System (RDBMS) that organizes data into tables with rows and columns. It uses Structured Query Language (SQL) to add, access, and process data, and is known for being fast, reliable, and scalable, often used in web application development (e.g., LAMP stack).
To install it, update the package index on your server if you’ve not done so recently
 <img width="945" height="197" alt="image" src="https://github.com/user-attachments/assets/0e692507-44d1-4981-b99d-bfcf8b68120f" />

(Monitoring VM) Then install the mysql-server package
 <img width="945" height="72" alt="image" src="https://github.com/user-attachments/assets/7c41f204-4c9d-479a-9d8e-ab6c82f7665b" />

Press  Y  to continue
Ensure that the server is running using sudo systemctl status mysql
<img width="945" height="462" alt="image" src="https://github.com/user-attachments/assets/2949f826-74ff-4ade-9dba-a4000d3c6ba0" />
 
Now to configure MySQL
Use command sudo mysql_secure_installation to run the script
Press  Y to setup validate password component. 
Set the password validation policy to STRONG  (nr.2)
 <img width="945" height="325" alt="image" src="https://github.com/user-attachments/assets/3f7d9c35-bd9a-4ef4-9d76-69cb5cc2f514" />

Press Y to everything it asks of you
Use command sudo mysql to enter mysql
 <img width="945" height="426" alt="image" src="https://github.com/user-attachments/assets/460ab9d3-c324-48ef-a76c-045b7961c495" />

Using status  command, we can check the status of our database
<img width="945" height="530" alt="image" src="https://github.com/user-attachments/assets/c5e5e4e7-faf8-4f57-8278-60cfe7d15434" />
 
(Monitoring VM) Now we’re gonna create initial database
Run the following on your database host
 <img width="945" height="171" alt="image" src="https://github.com/user-attachments/assets/695e002b-3522-4601-a8e1-00121b718139" />
<img width="945" height="396" alt="image" src="https://github.com/user-attachments/assets/5886285b-a27e-4501-8ce3-eca4931a06d1" />

 
(Monitoring VM) On Zabbix server host import initial schema and data. You will be prompted to enter your newly created password
 <img width="945" height="61" alt="image" src="https://github.com/user-attachments/assets/7d3ca267-3a40-4bbb-ba06-cdc402591b65" />

(Monitoring VM) Disable log_bin_trust_function_creators option after importing database schema
 <img width="945" height="375" alt="image" src="https://github.com/user-attachments/assets/8524c22a-0f10-4e82-93c4-3abca2751afb" />

(Monitoring VM) Configure the database for Zabbix server
Edit file /etc/zabbix/zabbix_server.conf
Use command nano /etc/zabbix/zabbix_server.conf to edit the file
Use CTRL+W to easily find DBPassword location in this file
Remove # from it and insert password that you made in mysql
 <img width="861" height="370" alt="Kuvatõmmis 2026-04-03 202511" src="https://github.com/user-attachments/assets/a7f2c779-4e32-40c4-84a0-d2200ba40c02" />

Use CTRL+X to save and exit the file

3.3	What is Web Server?

A web server is a system comprising computer hardware and software that stores website files (HTML, CSS, images, JS) and delivers them to users over the internet via HTTP/HTTPS. It acts as a digital librarian, receiving requests from browsers (clients) and serving the requested web pages.

3.3.1	Nginx & Installation

NGINX (pronounced "engine-x") is a high-performance, open-source web server, reverse proxy, load balancer, and HTTP cache. Designed for maximum speed and stability, it handles thousands of concurrent connections efficiently using an event-driven architecture, making it ideal for high-traffic websites and reducing server load.
(Monitoring VM) In ubuntu browser search up localhost and you should get this
 <img width="945" height="248" alt="image" src="https://github.com/user-attachments/assets/b9b130b1-1474-4a3c-a328-fa2a48ff39be" />

This means that nginx has downloaded successfully and its working.
Navigate to Nginx enabled site
Remove default configuration
 <img width="945" height="83" alt="image" src="https://github.com/user-attachments/assets/17470c36-54d9-466d-9a8f-912497ee9822" />

Enable Zabbix configuration and test configuration
 <img width="945" height="144" alt="image" src="https://github.com/user-attachments/assets/7a323e8c-64ce-475c-b0f6-bc23d26b1f5f" />

Restart nginx
 <img width="945" height="55" alt="image" src="https://github.com/user-attachments/assets/add2e63f-f5a5-4507-94e1-81bb228deb79" />

(Monitoring VM) Start Zabbix server 
(Game Server) and agent processes
 <img width="945" height="182" alt="image" src="https://github.com/user-attachments/assets/06a9c2db-0aa7-4c3c-926c-f2f50e3e5162" />

Refresh your browser and Zabbix should show up
Choose your prefer language
<img width="945" height="507" alt="image" src="https://github.com/user-attachments/assets/5af30a9b-18f1-45c3-8a5d-d466ea5eebe9" />

 
Press Next step
<img width="945" height="494" alt="image" src="https://github.com/user-attachments/assets/1b140eb3-3328-4a01-82ea-da0808fc4436" />

 
Configure Database connection
 <img width="945" height="504" alt="image" src="https://github.com/user-attachments/assets/e413f81f-ba4f-4116-b65f-81d1c0527d50" />


Choose a name for your Zabbix server and set default time zone, press Next step and Install
 <img width="945" height="504" alt="image" src="https://github.com/user-attachments/assets/82829bd3-e63e-4550-b7a2-5ee27e562895" />

Login to Zabbix
 <img width="611" height="541" alt="image" src="https://github.com/user-attachments/assets/d76f8d66-432b-495c-993f-ebdf15278ac3" />

Zabbix is now setup and working
 <img width="945" height="501" alt="image" src="https://github.com/user-attachments/assets/04240d6f-4aa3-408f-9327-fac30266c163" />


4	SETTING UP THE AGENT


4.1	What is Playit.gg?

Playit.gg is a free, popular networking tool that allows you to host online game servers (like Minecraft, Valheim, or Terraria) from your own computer without needing to configure router port forwarding or share your public IP address. It creates a secure tunnel that acts as a proxy, making local servers accessible to friends over the internet.
The tool is highly regarded for being lightweight and user-friendly, providing an alternative for those wanting to host games privately without paying for a hosting provider.

4.2	Setting up Playit.gg

Open up Firefox or whatever browser you’re using in ubuntu and search playit.gg
 <img width="945" height="504" alt="image" src="https://github.com/user-attachments/assets/3dca6135-2a17-4039-b07d-8d7f4acd891a" />

Go to Downloads and copy lines from the Install via APT option.
 <img width="945" height="456" alt="image" src="https://github.com/user-attachments/assets/981a210b-66b8-423f-b2d2-ec8663da4870" />

After downloading the agent use the command playit setup  and you should get the link to setup.
 <img width="945" height="273" alt="image" src="https://github.com/user-attachments/assets/f739c275-b764-454a-a6b2-1e8334d77ec6" />

Copy pasteing the link to browser you have to Claim the Agent by Loging in to an already excisting account or making a new one.
 <img width="945" height="284" alt="image" src="https://github.com/user-attachments/assets/04380cd8-9af3-4e95-a21f-21eb1802b7c0" />

After creating the account asks you to verify details before continuing
 <img width="617" height="529" alt="image" src="https://github.com/user-attachments/assets/95aee2b4-7d48-4b00-9708-d24be9ef7c4c" />

 
Create agent name and wait for the agent to finish setting up
 <img width="945" height="323" alt="image" src="https://github.com/user-attachments/assets/353ef207-c4d9-47de-910c-3b673aa8531d" />

Start playit agent on terminal with the command sudo systemctl start playit
 <img width="945" height="60" alt="image" src="https://github.com/user-attachments/assets/da0090bd-1436-4745-9f87-7b62fec48fe8" />


4.2.1	Creating tunnel

After the agent has been installed and set up, we must create a tunnel for people to join our server
(Make sure to verify your email!)
Name your tunnel
 <img width="945" height="91" alt="image" src="https://github.com/user-attachments/assets/72a0bee4-c041-49f4-9059-47b8d299ea94" />

Choose the tunnel type. For this documentation we’re choosing Minecraft Java
 <img width="329" height="497" alt="image" src="https://github.com/user-attachments/assets/13573e3f-6d09-4be8-94e6-c79b0fa16d13" />


Since we’re using the Free Network people are routed to one of thir datacenters based on their ISP connection.
Confirm your server’s origin
 <img width="945" height="253" alt="image" src="https://github.com/user-attachments/assets/25f26e46-530c-45af-bf0b-94a48b2b9366" />

And now Create the tunnel
 <img width="803" height="233" alt="image" src="https://github.com/user-attachments/assets/2930c3c2-b301-41f5-907d-b03521d9eabc" />



5	INSTALLING MINECRAFT JAVA EDITION

5.1	What is Minecraft?
Minecraft is a sandbox game developed and published by the Swedish company Mojang Studios. Following its initial public alpha release as an early access title in 2009, it was formally released in 2011 for personal computers. The game has since been ported to numerous platforms, including mobile devices and various video game consoles.

5.2	 Java

Java is a high-level, class-based, and object-oriented programming language designed by Sun Microsystems in 1995 to have as few implementation dependencies as possible. It is famous for its "Write Once, Run Anywhere" (WORA) principle, where compiled Java code runs on all platforms supporting the Java Virtual Machine (JVM).

5.2.1	Installing Java

Install java using sudo apt install default-jdk  command
 <img width="945" height="120" alt="image" src="https://github.com/user-attachments/assets/43074ddc-5695-4f1e-8f01-ee1ae43556fe" />

Create a server folder using mkdir command
 <img width="870" height="55" alt="image" src="https://github.com/user-attachments/assets/b1cb2312-7033-446a-aa7a-5c8450b55346" />

Move to server folder using cd server command
 <img width="775" height="116" alt="image" src="https://github.com/user-attachments/assets/53fdea75-b3a4-4aa1-8e5a-e170c4d27996" />

Search PaperMC which is a minecraft server software that is designed to significantly increase performanc, reduse lag and fix gameplay incosistencies. Search papermc.io and right click on Paper1.21.11 or whatever version you’re conna use and copy the link.
Now to download this use command wget.
 <img width="945" height="68" alt="image" src="https://github.com/user-attachments/assets/590119d1-066d-4603-b38d-c8a02419a35a" />

To confirm, that the file is downloaded use command ls to check.
 <img width="722" height="283" alt="image" src="https://github.com/user-attachments/assets/800be1c1-6134-4f15-b3e3-37b68c6244c4" />

Rename installed file to server.jar
 <img width="945" height="92" alt="image" src="https://github.com/user-attachments/assets/6b5bd26a-47e7-4198-9e8d-44899c4835c0" />

Create executable shortcut using nano start.sh
Insert command to the file
-Xmx8G means machine max ram is 8gb and -Xms4G is minimum ram
CTRL + X and Y to save the file
 <img width="945" height="203" alt="image" src="https://github.com/user-attachments/assets/7275f171-e384-4b2c-90c3-bfc57d4cfa41" />

Give the file executable permission using command chmod +x start.sh 
 <img width="945" height="50" alt="image" src="https://github.com/user-attachments/assets/ef1c59f9-0059-4cff-afff-6b65f16724bd" />

Execute the start.sh file
 <img width="945" height="97" alt="image" src="https://github.com/user-attachments/assets/8fbd9562-c936-4679-a325-4a3047de54c0" />

Accept eula agreement using command nano eula.txt set eula=false to true
 <img width="945" height="231" alt="image" src="https://github.com/user-attachments/assets/c39e3da4-80d9-48ec-a802-422eed135774" />


5.2.2	Starting the server

Run the ./start.sh  again to generate the world
To keep the server running in the background, install tmux using sudo apt install tmux
Use command tmux new-session -t minecraft „name“ and now the instance wont be killed even if you close the SSH connection.
Start the agent in terminal by using systemctl start playit
 <img width="945" height="101" alt="image" src="https://github.com/user-attachments/assets/f1e1cdbb-9d6f-45e4-9003-3eeef4d22601" />

Now that’s the agent is running copy the public  address from playit.gg and insert this in Minecraft Multiplayer section
 <img width="945" height="110" alt="image" src="https://github.com/user-attachments/assets/f09ae20f-48c8-4677-a6e5-35e0abfd2640" />

In Minecraft choose Multiplayer and Add Server and create name for your server and insert your public address
 <img width="945" height="706" alt="image" src="https://github.com/user-attachments/assets/b6d00ba7-d4c2-4695-940f-92f45a108efe" />

And it works! Dont forget to start the server if it gives you can’t connect to server pop-up
 <img width="945" height="241" alt="image" src="https://github.com/user-attachments/assets/09831a53-e9fb-420f-9574-8dcf70c39528" />





#6	Zabbix Server Monitoring

To monitor a Minecraft server with Zabbix on Ubuntu, you need to bridge the gap between the Minecraft Java process and the Zabbix Agent. Since Minecraft doesn't natively speak to Zabbix, the most reliable method is using RCON (Remote Console) to pull metrics via custom scripts.

6.1. Enable RCON on Your Minecraft Server
Open your server.properties file and ensure RCON is enabled so you can query the server externally.

In server.properties

enable-rcon=true

rcon.port=25575

rcon.password=your_secure_password

Restart your server after saving.

6.2. Install an RCON Client

You need a way for Ubuntu to send commands to the server. mcrcon is the industry standard for this.

Update your machine with sudo apt update

After updating install mcrcon

<img width="719" height="37" alt="image" src="https://github.com/user-attachments/assets/a8ae910a-7165-4937-98b2-82010e810a3b" />

6.3. Create the Monitoring Script

Create a script (e.g., /usr/local/bin/mc_stats.sh) that Zabbix will run to fetch data. This script uses mcrcon to ask for TPS and entity counts.

Create a new script directory in /urs/local/bin and name the  script file to mc_stats.sh.

<img width="964" height="174" alt="image" src="https://github.com/user-attachments/assets/5f8b7d81-1ec6-45e1-976d-5de0a5037f74" />

Write the script:

<img width="1820" height="978" alt="image" src="https://github.com/user-attachments/assets/21d8e2ac-e026-4b23-8e77-6f69472e9496" />

Make it executable: sudo chmod +x /usr/local/bin/mc_monitor.sh

<img width="1171" height="65" alt="image" src="https://github.com/user-attachments/assets/d878cb1a-c5fa-400c-8af8-2de6db504f46" />

6.4. Connect Zabbix Agent to the Script

Now, we tell the Zabbix Agent that these new "keys" exist. Edit your agent configuration:

<img width="863" height="46" alt="image" src="https://github.com/user-attachments/assets/4de82636-9bd3-46da-b220-42a8273d8d1a" />

Add these UserParameters at the very bottom:

<img width="1201" height="239" alt="image" src="https://github.com/user-attachments/assets/1ffd6446-6521-480f-a8aa-66e6d37a1251" />


The memory command calculates the "Resident Set Size" (actual physical RAM usage) of your Java process in bytes.

Restart the agent: sudo systemctl restart zabbix-agent

6.5. Setting up the Zabbix Web UI

Step 1: Tell Zabbix what "Gauges" to look at (Items)
You need to tell Zabbix to start watching the specific numbers we set up earlier (TPS, Players, and RAM).

Open your Zabbix website and go to Data Collection > Hosts.

Find your Ubuntu server in the list and click the word Items next to it.

Click the blue Create item button at the top right.

Fill it out for TPS (Lag):

Name: Minecraft Lag (TPS)

Key: mc.tps (This must match exactly what you typed in the black-and-white terminal earlier).

Type of information: Numeric (float) — This just means "a number with a decimal point."

Click Add.

<img width="1252" height="730" alt="image" src="https://github.com/user-attachments/assets/77b35383-fc78-44d6-8e90-70c8d221eab4" />

Repeat this for everything else under thius table:

<img width="634" height="285" alt="image" src="https://github.com/user-attachments/assets/c61d24cd-4640-4cee-97e1-ba3d301d108c" />



Step 2: Set the "Check Engine" Lights (Triggers)
A "Trigger" is just a rule that says: "If this number looks bad, send me an alert."

Click on the Triggers tab (it’s right next to "Items" at the top).

Click Create trigger.

To catch lag:

Name: Server is Lagging!

Severity: Average (or High if you're worried).

Expression: Click "Add" and find your mc.tps item. Set it so if the result is < 16, the alarm goes off. (Perfect Minecraft speed is 20).

Click Add.

<img width="1623" height="864" alt="image" src="https://github.com/user-attachments/assets/d5cd27b7-d95e-42cc-ba78-b5224c233a22" />

Also make sure, that the Item "Type" is Zabbix agent (active).


Step 3: Make it Pretty (Dashboards)

This is the satisfying part where you see the live data.

Go to Monitoring > Dashboards.

Click Create dashboard (or edit an existing one).

Add a Widget:

Type: Graph.

Name: Minecraft Performance.

Data set: Add mc.tps and mc.players.

Pro Tip: Use a "Stacked" graph for memory usage, but a "Line" graph for TPS so you can see dips clearly.


7	OPTIONAL: CREATING SSL CERTIFICATION FOR ZABBIX

7.1	What is SSL Certificate?

An SSL certificate is a digital credential that authenticates a website's identity and enables an encrypted connection between a web server and a browser, ensuring the secure transmission of sensitive data via the TLS protocol.

This is optional for this documentation but highly recommended.

7.2	Setting up SSL

You can generate a certificate and a private key directly on your Ubuntu server using OpenSSL.
Create a directory for the keys
 <img width="945" height="222" alt="image" src="https://github.com/user-attachments/assets/1112bb5b-8696-48f9-8334-963881cb7786" />

Run the following command. It will ask for information like Country and City—you can leave these blank or fill them in with whatever you like. 
 <img width="1003" height="388" alt="image" src="https://github.com/user-attachments/assets/22b8e48f-93dd-4788-91b4-5468e8e94e88" />

•	days 365: The certificate will be valid for one year.

•	rsa:2048: Standard encryption strength.

Now, tell Nginx to look for those files when someone hits your server's IP via HTTPS.

Edit the Zabbix Nginx config
<img width="945" height="39" alt="image" src="https://github.com/user-attachments/assets/f6e3e6d3-062d-4aa8-b536-f9156be6d00d" />
 
Modify the server block to look like this (replace the listen 80 section or add this alongside it)
 <img width="945" height="339" alt="image" src="https://github.com/user-attachments/assets/696c3bc0-0339-40c9-8276-e8c427642f7d" />

Test and restart
 <img width="945" height="109" alt="image" src="https://github.com/user-attachments/assets/f1ca7456-d759-4c4f-bc9f-feedc66a1cff" />

Now proceed to localhost (Zabbix) page and it should be https instead of http
 <img width="945" height="335" alt="image" src="https://github.com/user-attachments/assets/da24b404-3ac7-43f9-aa73-d6a76a339859" />




