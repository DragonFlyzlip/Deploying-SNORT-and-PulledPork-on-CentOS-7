# Deploying-SNORT-and-PulledPork-on-CentOS-7


## Objective

The objective of this project is to successfully deploy and configure SNORT, a widely-used open-source intrusion detection system (IDS), on CentOS 7, and integrate it with PulledPork for automated rule management and updates. This involves setting up a robust IDS environment capable of monitoring network traffic for potential threats, detecting suspicious activities, and leveraging rule sets to enhance security. By completing this project, the goal is to gain hands-on experience with SNORT's configuration, understand how it functions as a core security tool, and utilize PulledPork to streamline the process of updating and managing SNORT rules efficiently. This ensures a practical understanding of implementing IDS solutions in real-world scenarios while addressing challenges such as rule integration, logging, and system optimization.

### Skills Learned

- SNORT Configuration: Set up and customize an open-source IDS for real-time threat detection.
- PulledPork Integration: Automate rule updates and manage SNORT rule sets efficiently.
- Network Traffic Analysis: Monitor and analyze packets for suspicious activity.
- Intrusion Detection Deployment: Implement an IDS in a Linux environment.
- CentOS Administration: Perform system updates, dependency installation, and configuration on CentOS 7.
- Rule Management: Create, test, and troubleshoot custom detection rules.
- Logging and Alerts: Configure logs for threat visibility and response.
- System Optimization: Enhance IDS performance with resource management and configuration tweaks.

### Tools Used


- SNORT: Open-source intrusion detection and prevention system (IDS/IPS).
- PulledPork: Rule management and update tool for SNORT.
- CentOS 7: Linux-based operating system for deploying the IDS.
- YUM/DNF: Package managers for installing dependencies.
- tcpdump: Command-line tool for capturing and analyzing network packets.
- vi/nano: Text editors for modifying configuration files.
- wget/curl: Tools for downloading files and dependencies.
- Firewall (iptables/Firewalld): Configured to manage traffic to/from SNORT.
- Log Management Tools (e.g., syslog): For monitoring SNORT logs.

## Steps
 Step 1:

![image](https://github.com/user-attachments/assets/5c876d84-4681-4c00-9da1-b8b808fbbf8f)


*sudo yum install epel-release -y*

Step 2:


Run ldconfig:

- This command updates the system’s shared library cache, essential for SNORT to function correctly:
sudo ldconfig

- Troubleshooting: Address any errors by checking library paths in /etc/ld.so.conf.

- Create Directories and Set Permissions:

- For SNORT to store its configuration and logs, set up directories:
- 
  
*sudo mkdir -p /etc/snort/rules sudo mkdir /var/log/snort sudo mkdir /usr/local/lib/snort_dynamicrules*

- Set permissions for these directories to avoid permission-related issues

- 
*sudo chmod -R 5775 /etc/snort*


![image](https://github.com/user-attachments/assets/b11b76a5-bd4c-4c23-a6f1-81e932485a2e)

step 3:

 Install PulledPork and Dependencies:

-Install dependencies for PulledPork using:


*sudo yum install perl-LWP-Protocol-https perl-Crypt-SSLeay -y*


-Clone the PulledPork repository from GitHub and install it:


*git clone https://github.com/shirkdog/pulledpork.git cd pulledpork sudo cp pulledpork.pl /usr/local/bin/*


![image](https://github.com/user-attachments/assets/af686fac-bd11-4dde-a793-ca731286f2dc)


![image](https://github.com/user-attachments/assets/8a5135ba-4113-4e28-87bd-640a46cabc83)

step 4

Configure PulledPork:

-First, sign up for an Oinkcode at SNORT’s website to obtain access to the latest rules.
Open the PulledPork configuration file:

*sudo nano /etc/snort/pulledpork.conf*

-Add your Oinkcode and configure any necessary paths for SNORT rules and signatures.


![image](https://github.com/user-attachments/assets/ebe3a1fd-dbee-4899-af67-0b7a50ea4038)



![image](https://github.com/user-attachments/assets/0ce5343e-1271-42ee-8f0c-3944305144f4)



![image](https://github.com/user-attachments/assets/c6339c9f-2985-49cf-827f-6be6e15160cd)



![image](https://github.com/user-attachments/assets/0c85333e-f352-4609-8bb7-1ae27a18297c)




![image](https://github.com/user-attachments/assets/e76d0c53-858c-4a1f-a84c-c25ebafe3299)




![image](https://github.com/user-attachments/assets/8948ca6e-b41c-4157-8c0b-bd571c98fcff)




![image](https://github.com/user-attachments/assets/66dd2159-769e-4e9a-a6db-4e3b4658f40c)



![image](https://github.com/user-attachments/assets/69ec84c3-ef09-4f2b-aebd-f9bd60d92590)




![image](https://github.com/user-attachments/assets/414c5ad8-0d69-4599-be36-551e67dcbfc7)




![image](https://github.com/user-attachments/assets/751dbed0-06e5-4839-863c-7805cbf4a7ec)


##step 5:
 
 Verify SNORT Installation and Configuration:

Ensure SNORT is working as expected:
*snort -v*


![image](https://github.com/user-attachments/assets/137ad874-ed1a-4cab-99f2-0cb44357c8e5)


step 6:

-Update SNORT Rules:

Run PulledPork to pull the latest rule updates:

*sudo pulledpork.pl -c /etc/snort/pulledpork.conf*


![image](https://github.com/user-attachments/assets/b01c81a8-14f8-419b-9eb8-b5ff4c995c14)


step 7:

-Test SNORT Functionality:

Add test rules in local.rules to detect network traffic, such as ICMP:

*alert icmp any any -> any any (msg:"ICMP test"; sid:1000001; rev:1;)*4


![image](https://github.com/user-attachments/assets/b649a7c3-d52c-4028-b10c-036936dd0144)


![image](https://github.com/user-attachments/assets/a9e2e61a-9d29-4fbe-b171-0823629c554e)


## Final Thoughts

Deploying SNORT with PulledPork on CentOS provides a powerful, open-source NIDS capable of keeping up with evolving threats through automatic rule updates. This hands-on lab not only introduces you to the basics of SNORT and PulledPork but also equips you with practical knowledge to manage, configure, and maintain a network intrusion detection setup in a real-world environment.
















