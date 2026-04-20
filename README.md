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
 
And in Network  set you’re Adapter 1 to Bridged Adapter.
 

2.3	Install the machine

Choose your language
 
For the type of installation choose only Ubuntu Server
 
It should give your machines DHCPv4 
 
No need to put anything in Proxy configuration

 
Dont change anything here since we already made a disk.
 
Setup your server’s name, password etc...
 
You can choose, if you want Ubuntu Pro since its free for personal use ( 1 to 5 machines)
 
Install OpenSSH server so you could use ssh  command to easily use the machine in windows cmd for example.
 
We’re not choosing any Featured server snaps, so you can just press Done.
Now wait for the machine to install and press Reboot Now  when its done. 
After its done rebooting press Enter on your keyboard
Login to your machine
 
2.3.1	What is  Gnome?
GNOME (GNU Network Object Model Environment) is the default graphical user interface (desktop environment) for Ubuntu. It provides the visual, interactive experience—windows, icons, top panel, and app launcher—allowing users to manage files, applications, and settings in a modern, clean, and distraction-free workspace.
2.3.2	Installing Gnome
First of all we are going to update our systems package list using command: sudo apt update.
If you dont want to always insert your password after using sudo just log into the administrator account using command  sudo su.
 

After updating we’re gonna use command sudo apt install ubuntu-gnome-desktop
Press  Y  to continue
After the installation completed use command Reboot to reboot the virtual machine.
And now our Ubuntus Interface should look like this.
 
And when you login
 
 

3	SETTING UP MONITORING SOFTWARE

3.1	What is monitoring software?

Monitoring software is a category of tools designed to track, record, and analyze activity on computers, networks, or applications. It acts as a surveillance or diagnostic system, reporting data like user actions, bandwidth usage, or system uptime to administrators to ensure productivity, security, and performance.

3.1.1	Zabbix & Installation

Zabbix is a free, open-source enterprise-level monitoring solution designed to monitor IT infrastructure, including networks, servers, virtual machines, cloud services, and applications in real-time. It enables proactive IT management by collecting metrics via agents, SNMP, or APIs, providing alerting, visualization, and automated network discovery, often used to prevent downtime. 
First things first go to this website:
https://www.zabbix.com/download?zabbix=7.0&os_distribution=ubuntu&os_version=24.04&components=server_frontend_agent&db=mysql&ws=apache

And under Product we’re gonna choose Zabbix Packages. For platform choose options from the picture below.
 
Install Zabbix repository using following commands:
 
After installing Zabbix repository we’re gonna have to also install Zabbix server, frontend and agent 2. 
 




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
 
MySQL is a popular, open-source Relational Database Management System (RDBMS) that organizes data into tables with rows and columns. It uses Structured Query Language (SQL) to add, access, and process data, and is known for being fast, reliable, and scalable, often used in web application development (e.g., LAMP stack).
To install it, update the package index on your server if you’ve not done so recently
 
(Monitoring VM) Then install the mysql-server package
 
Press  Y  to continue
Ensure that the server is running using sudo systemctl status mysql
 
Now to configure MySQL
Use command sudo mysql_secure_installation to run the script
Press  Y to setup validate password component. 
Set the password validation policy to STRONG  (nr.2)
 
Press Y to everything it asks of you
Use command sudo mysql to enter mysql
 
Using status  command, we can check the status of our database
 
(Monitoring VM) Now we’re gonna create initial database
Run the following on your database host
 
 
(Monitoring VM) On Zabbix server host import initial schema and data. You will be prompted to enter your newly created password
 
(Monitoring VM) Disable log_bin_trust_function_creators option after importing database schema
 
(Monitoring VM) Configure the database for Zabbix server
Edit file /etc/zabbix/zabbix_server.conf
Use command nano /etc/zabbix/zabbix_server.conf to edit the file
Use CTRL+W to easily find DBPassword location in this file
Remove # from it and insert password that you made in mysql
 
Use CTRL+X to save and exit the file

3.3	What is Web Server?

A web server is a system comprising computer hardware and software that stores website files (HTML, CSS, images, JS) and delivers them to users over the internet via HTTP/HTTPS. It acts as a digital librarian, receiving requests from browsers (clients) and serving the requested web pages.

3.3.1	Nginx & Installation

NGINX (pronounced "engine-x") is a high-performance, open-source web server, reverse proxy, load balancer, and HTTP cache. Designed for maximum speed and stability, it handles thousands of concurrent connections efficiently using an event-driven architecture, making it ideal for high-traffic websites and reducing server load.
(Monitoring VM) In ubuntu browser search up localhost and you should get this
 
This means that nginx has downloaded successfully and its working.
Navigate to Nginx enabled site
Remove default configuration
 
Enable Zabbix configuration and test configuration
 
Restart nginx
 
(Monitoring VM) Start Zabbix server 
(Game Server) and agent processes
 
Refresh your browser and Zabbix should show up
Choose your prefer language

 
Press Next step

 
Configure Database connection
 

Choose a name for your Zabbix server and set default time zone, press Next step and Install
 
Login to Zabbix
 
Zabbix is now setup and working
 

4	SETTING UP THE AGENT


4.1	What is Playit.gg?

Playit.gg is a free, popular networking tool that allows you to host online game servers (like Minecraft, Valheim, or Terraria) from your own computer without needing to configure router port forwarding or share your public IP address. It creates a secure tunnel that acts as a proxy, making local servers accessible to friends over the internet.
The tool is highly regarded for being lightweight and user-friendly, providing an alternative for those wanting to host games privately without paying for a hosting provider.

4.2	Setting up Playit.gg

Open up Firefox or whatever browser you’re using in ubuntu and search playit.gg
 
Go to Downloads and copy lines from the Install via APT option.
 
After downloading the agent use the command playit setup  and you should get the link to setup.
 
Copy pasteing the link to browser you have to Claim the Agent by Loging in to an already excisting account or making a new one.
 
After creating the account asks you to verify details before continuing
 
 
Create agent name and wait for the agent to finish setting up
 
Start playit agent on terminal with the command sudo systemctl start playit
 

4.2.1	Creating tunnel

After the agent has been installed and set up, we must create a tunnel for people to join our server
(Make sure to verify your email!)
Name your tunnel
 
Choose the tunnel type. For this documentation we’re choosing Minecraft Java
 

Since we’re using the Free Network people are routed to one of thir datacenters based on their ISP connection.
Confirm your server’s origin
 
And now Create the tunnel
 


5	INSTALLING MINECRAFT JAVA EDITION

5.1	What is Minecraft?
Minecraft is a sandbox game developed and published by the Swedish company Mojang Studios. Following its initial public alpha release as an early access title in 2009, it was formally released in 2011 for personal computers. The game has since been ported to numerous platforms, including mobile devices and various video game consoles.

5.2	 Java

Java is a high-level, class-based, and object-oriented programming language designed by Sun Microsystems in 1995 to have as few implementation dependencies as possible. It is famous for its "Write Once, Run Anywhere" (WORA) principle, where compiled Java code runs on all platforms supporting the Java Virtual Machine (JVM).

5.2.1	Installing Java

Install java using sudo apt install default-jdk  command
 
Create a server folder using mkdir command
 
Move to server folder using cd server command
 
Search PaperMC which is a minecraft server software that is designed to significantly increase performanc, reduse lag and fix gameplay incosistencies. Search papermc.io and right click on Paper1.21.11 or whatever version you’re conna use and copy the link.
Now to download this use command wget.
 
To confirm, that the file is downloaded use command ls to check.
 
Rename installed file to server.jar
 
Create executable shortcut using nano start.sh
Insert command to the file
-Xmx8G means machine max ram is 8gb and -Xms4G is minimum ram
CTRL + X and Y to save the file
 
Give the file executable permission using command chmod +x start.sh 
 
Execute the start.sh file
 
Accept eula agreement using command nano eula.txt set eula=false to true
 

5.2.2	Starting the server

Run the ./start.sh  again to generate the world
To keep the server running in the background, install tmux using sudo apt install tmux
Use command tmux new-session -t minecraft „name“ and now the instance wont be killed even if you close the SSH connection.
Start the agent in terminal by using systemctl start playit
 
Now that’s the agent is running copy the public  address from playit.gg and insert this in Minecraft Multiplayer section
 
In Minecraft choose Multiplayer and Add Server and create name for your server and insert your public address
 
And it works! Dont forget to start the server if it gives you can’t connect to server pop-up
 




6	VIRTUAL MACHINE MONITORING

Now, that our server is running, we want zabbix to monitor player count, TPS, entities, memory leaks and etc.
You need to tell the VM which server is allowed to request data.

Open the configuration file sudo nano /etc/zabbix/zabbix_agent2.conf , locate and configure following parameters:

•	Server: Set this to the IP address of your Zabbix Server.
•	ServerActive: Set this to the IP address of your Zabbix Server.
•	Hostname: Set this to the exact name of the VM (this must match the name you use later in the Zabbix Web UI).

After that save the file and restart the agent to apply changes
 
The Zabbix Server communicates with the Agent via port 10050. You must open this on the target VM.
 
Now, head to your Zabbix Server dashboard in your browser.
1.	Go to Data collection > Hosts.
2.	Click Create host in the top right.
3.	Host name: Must exactly match the Hostname you typed in the config file.
4.	Templates: Search for and select Linux by Zabbix agent.
5.	Host groups: Select a group (e.g., Virtual machines or Linux servers).
6.	Interfaces: Click Add > Agent.
o	Enter the IP address of the target VM.
7.	Click Add.
 

7	OPTIONAL: CREATING SSL CERTIFICATION FOR ZABBIX

7.1	What is SSL Certificate?

An SSL certificate is a digital credential that authenticates a website's identity and enables an encrypted connection between a web server and a browser, ensuring the secure transmission of sensitive data via the TLS protocol.
This is optional for this documentation but highly recommended.

7.2	Setting up SSL

You can generate a certificate and a private key directly on your Ubuntu server using OpenSSL.
Create a directory for the keys
 
Run the following command. It will ask for information like Country and City—you can leave these blank or fill them in with whatever you like. 
 
•	days 365: The certificate will be valid for one year.
•	rsa:2048: Standard encryption strength.
Now, tell Nginx to look for those files when someone hits your server's IP via HTTPS.
Edit the Zabbix Nginx config
 
Modify the server block to look like this (replace the listen 80 section or add this alongside it)
 
Test and restart
 
Now proceed to localhost (Zabbix) page and it should be https instead of http
 




