Installing Zentyal as Primary Domain Controller and Integrate Windows/Linux based systems

Introduction 

Zentyal Server Development Edition is aimed at organizations with in-house experience and skills to install, configure and maintain the Zentyal deployment by themselves. 
Latest release: Zentyal 6.2
based on Ubuntu Server 18.04.4 LTS 

Full feature list

Directory & Domain :

Central domain and directory management 
Users, Security groups, Distribution lists, Contacts 
Multiple Organization Units (OUs), Group Policy Objects (GPOs) 
NETLOGON scripts, Roaming profiles 
Single Sign-On (SSO) authentication 
Supported OS: Windows® XP/Vista/7/8/10 
File sharing in Windows® environments (CIFS) 
Users and Groups access and modification permissions (ACLs) 
Integrated software: Samba 

Mail :

Supported protocols: SMTP, POP3, IMAP, CalDAV, CardDAV, SIEVE 
Supported clients: Mozilla Thunderbird® 
Webmail 
Synchronization to mobile devices via ActiveSync 
Multiple virtual mail domains 
Single Sign-On (SSO) authentication 
Management via Zentyal or Microsoft ® Active Directory 
Antivirus & Mail filter 
Integrated software: Postfix, Dovecot, Fetchmail, Sieve, SOGo, SOGo ActiveSync, Amavis, ClamAV, SpamAssasin 

Gateway :

Network configuration 
Routing 
Gateway 
Firewall 
Network authentication service (RADIUS) 
FreeRADIUS 
HTTP Proxy 
IDS/IPS 
Integrated software: Iproute2, Netfilter, Squid, Suricata, FreeRADIUS 

Infrastructure :

DHCP and DNS server 
NTP server 
Certification Authority (CA) 
Virtualization Manager 
Virtual Private Networks (VPNs) 
Instant Messaging (IM) service 
Libvirt/KVM, Duplicity 
FTP Server 
Integrated software: BIND, ISC DHCP Software, ntpd, OpenSSL, OpenVPN, ejabbered, vsftpd, Libreswan 

Prerequisites:

To download Zentyal 6.2 Development Edition, please follow this link
 http://download.zentyal.com/zentyal-6.2-development-amd64.iso

We can install Zentyal in two different ways:
 1) Using the Zentyal installer (recommended option) – The above approach
 2) On top of any existing Ubuntu Server Edition installation. 
    sudo apt-get update -y 
    sudo apt-get install -y zentyal-core 

After downloading the image, burn the ISO to the USB or on Virtual box point the ISO image.

Open Virtual box, new → specify the name and Type of OS and Version(64/32 bit)->specify the RAM details → create a virtual hard disk now → VDI(Dynamically allocated) → Specify the location of VDI(D:\VM images\Zentayl-dailyhunt.vdi) with your desired hard disk size and click on Create 

Installation screen appears, after the ISO gets pointed and it gets boots up.

Installation of Zentyal Server

1. Select your desired Language → English 

2. Select Install Zentyal 6.2(expert mode) - 2nd option 

3. Now select your preferred language for installation. - English 

4. Select your location. If your location is not listed by default, just go for other and then choose your continent and country – India in our case 

5. Select your keyboard layout. - English(US)

6. Now the installer will load the components required to configure your system.

7. To configure network manually, Select configure network manually.

Enter your IP address, Netmask, Gateway, NameServer(DNS)

8. In the next stage, set the hostname for your computer and enter your FQDN. Here my FQDN is " zentayl.dailyhunttest.com"

9. Select an user for your system administration and not the user domain controller.Username → dailyhunt

10. Enter password for root user, it must be a stronger one.

11. It prompts you to re-enter your password.

Use weak password, give yes

12. To configure your system time. Select " Yes" if time setting is correct.

13. For Partitioning Disk, select manual and click Enter.

14. To select your HDD, here choose VMware virtual disk.

15. To create new partition table, Click yes and press Enter.

16. To Configure the Hard Disk Partitions.
boot partition

300 MB

swap area

2 GB

/ Partition ext4

8.4 GB

In real scenario, assign more space for all of the partitions, Please follow the below steps

Steps to partition :

Select the free space and click enter, now select create a new partition

Now give the size for the boot partition

Select the partition type, it should be selected as primary

Select the location for the partition as beginning

Select the filesystem type as EXT4 and mount point as /boot. After configuring select Done it setups up the partition

Now select the free space and give enter and then select create a new partition

Give the size for the swap partition

Since the swap partition should be double the size of RAM, Lets go with 2GB for the swap partition. Select the partition type as primary

Select from which position of the free space the partition should be created

Select the filesystem type as Swap area

After configuring select Done it setups up the partition

Select the free space and click enter now and then select the create a new partition

Now give the size for the root partition

Select the partition type as Primary

Select from which position of the free space the partition should be created

Select the filesystem type as EXT4 and mount point as / After configuring give done setting up the partition

Now select Finish partitioning and write changes to disks

17. To setup a Graphical Environment for Zentyal. If your server has both monitor and keyboard attached, then you have to select No, if not then select yes.

18. Now the Installation process starts.

19.If u use proxy server enter the proxy information or else leave the space blank and Click enter.

20. Select yes to install Grub bootloader into MBR.

21. Select Yes for next warning about UTC time.

22. Click enter to continue and the computer starts rebooting.

After rebooting, the system will install zentyal core packages.

To Install Basic Software' s for PDC

Open a web browser and enter the IP address or the hostname in search bar. 

For example: " https://localhost:8443/Login/index"

It gives warnings to you about a security issue certificate.

select " I Understand the Risks" , " Add exception" and " Confirm Security Exception" .

23. Just Enter your admin user name and password (key in your credentials in our case dailyhunt/dailyhunt)

24. In Zentyal Web Administration, click on continue to Select and install software for our Primary Domain Controller.

25. Select the below mentioned packages for the server to become a PDC.
Domain Controller and File sharing
Firewall
DNS Server
DHCP(Optional)
Confirm your packages installation as shown below and click on Install.

The following packages will be installed as per our selection earlier
  
Network Configuration 
Firewall
DNS Server
NTP Server
Domain controller and File sharing

Click on continue to install

26. Configuring your Network Interface as Internal.

27. To select Static Method and give your static IP server address, DNS servers, Gateway and Netmask.

28. Selecting the Standalone server and type your domain name and then click Finish.
dailyhunt.com

29. After PDC installation completes, navigate to DNS Module and check that your domain is in the Domain tab list.

30. Navigate to Users and Computers Module, choose Manage and include a user with Administrator Privileges for Active Directory.
To choose users , hit on " +" button below and type your credentials.

31. To select the user, in right side under User Groups field choose Domain Admins and click the " plus" button like below.

32. Navigate to Domain Module, choose Settings and select a description for your server and then choose " Enable roaming profiles" and also click Change.

33. In the top right, select on Save Changes to apply your new settings and hit Save.

To Integrate Windows System in PDC

34. Navigate to Start and select Control Panel and then click " Network and Internet" , after this choose " Network and Sharing Center" , then " View Network Status and Tasks" , after this choose Local Area Connection.

35. In Local Area Connection, choose Properties and then IPv4 and also enter your static IP address, Gateway, Netmask and DNS.

36. To check all is OK, just ping your pdc server address and domain name using the command prompt.

37. To add Windows 7 into the pdc.linuxhelp.com domain. Select Computer and click System Properties and then Advanced System Settings after that select, Computer Name.

38. Type your computer name in the Name field domain in the Member of Domain.

39. In the next window, type your username and password for the domain Administrator User.

40. Reboot the system to apply setting and then log on to your new domain.

41. In login screen, type your domain and administrator username.

42. Click start and right click computer and select properties. Now you can see the windows system is added to the dailyhunt.com

43. Open Zentyal server and Go to https://localhost:8443 in the browser and verify if the Computer was added to Computers and Users.

Enabling GPO on Zentayl :- 

1) Access your Zentyal Web Administration Tools through “https://your_domain_name” or “https://your_zentyal_ip_addess” and go to Users and Computers Module –> Manage.

2) Highlight your domain, click on green “+” button, select Organizational Unit and on the prompt enter your “Organizational Unit Name” ( choose a descriptive name ) and then click on Add 

3) Now go to your Windows Remote System and open Group Policy Management shortcut 

4) Right click on your Organization Name just created and select Create a GPO in this domain, and Link it here

5) On the New GPO prompt enter a descriptive name for this new GPO and the hit OK. 

6) This creates your GPO Basic File for this Organizational Unit but has no settings configured yet. To start editing this file right click on this file name and select Edit. 

7) This will open Group Policy Management Editor for this file

Joining Cent OS 7 to Zentayl PDC :

Configure Network to reach Zentayl PDC

1. Before starting to install and configure the required services in order to join CentOS 7 Desktop to an Active PDC you need to make sure that your network can reach and get a response from Zentyal PDC 

On the first step go to CentOS Network Settings, turn off your interface Wired Connections, add the DNS IPs that points to your Zentyal PDC or Windows AD DNS servers, Apply the settings and turn on your Network Wired Card. 

2. If your network has only a single DNS sever that resolves your PDC, you need to ensure that this IP is the first from your DNS servers list. Also open resolv.conf file located in /etc directory with root editing permissions and append the following line at the bottom, after nameserver list. 

search dailyhunt.com

3. After you have configured CentOS 7 network connections, issue a ping command against your PDC FQDN and make sure it responds accurately with its IP Address. 

ping pdc_fqdn(dailyhunt.com)

4. On the next step, configure your machine hostname as a Fully Qualified Domain Name and verify it by issuing the following commands with root privileges. 

# hostnamectl set-hostname <hostname>.dailyhunt.com
# cat /etc/hostname
# hostname
The left system hostname configured on this step, will be the name that will appear on Zentyal PDC on joined Computers names.

5. The last step that you will need to carry out before installing required packages to join PDC is to ensure that your system time is synchronized with Zentyal PDC. Run the following command with root privileges against your domain to sync time with the server.

sudo ntpdate -ud dailyhunt.com

6. Install the below packages to authenticate via Zentayl

sudo yum install samba samba-winbind

7. Next install the Kerberos Workstation Client, which provides a strong cryptographic network authentication based on a Key Distribution Center (KDC) trusted by all network systems, by issuing the following command. 

sudo yum install krb5-workstation

8. The last package that you need to install is Authconfig-gtk, which provides a Graphical Interface that manipulates Samba files in order to authenticate to a Primary Domain Controller. Use the following command to install this tool. 

sudo yum install authconfig-gtk

9. After all the required packages had been installed you need to make some changes to Kerberos Client main configuration file. Open /etc/krb5.conf file with your favorite text editor using an account with root privileges and
edit the following lines. 

vi /etc/krb5.conf

Here make sure you replace this lines accordingly – Use uppercase, dots and spaces as suggested in this examples. 

[libdefaults]
default_realm = YOUR_DOMAIN.TLD

[realms]
YOUR_DOMAIN.TLD = {
kdc = dailyhunt_fqdn
}

[domain_realm]
.your_domain.tld = YOUR_DOMAIN.TLD
your_domain.tld = YOUR_DOMAIN.TLD
Join CentOS 7 to Zentyal PDC

After you have made all of the configurations above your system should be ready to become a fully qualified member to Zentyal PDC. Open Authconfig-gtk package with root privileges and make the following adjustments as presented here. 

$ sudo authconfig-gtk

a. On Identity & Authentication tab

1. User Account Database = choose Winbind 
2. Winbind Domain = type YOUR_DOMAIN name (dailyhunt)
3. Security Model = choose ADS 
4. Winbind ADS Realm = type YOUR_DOMAIN name 
5. Domain Controllers = type your Zentyal PDC FQDN (dailyhunt)
6. Template Shell = choose /bin/bash 
7. Allow offline login = checked 

b. Move to Advanced Options tab

1. Local Authentication Options = check Enable fingerprint reader support 
2. Other Authentication Options = check Create home directories on the first login 

Now, after editing Authentication Configuration tabs with the required values don’t close the window and go back to Identity & Authentication tab. Click on Join Domain button and Save the prompt Alert to proceed further. 

If your configuration has been successfully saved, your system will contact the PDC and a new prompt should appear demanding you to enter a domain administrator credentials in order to join the domain.

Enter your domain name administrator user and password, hit on OK button to close the prompt and, then, click on Apply button to apply the final configuration.

If changes are successfully applied, the Authentication Configuration window should close and a message should appear on Terminal which will inform you that your computer has been integrated into your domain.

In order to verify, if your system has been added to Zentyal PDC, login to Zentyal Web Administrative Tool, go to Users and Computers -> Manage menu and check if your machine hostname appears on Computers list.

Login to CentOS 7 with PDC Users

At this point all the users listed in Zentyal PDC infrastructure should now be able to perform logins to your CentOS machine from a local or remote Terminal or by using the first Login Screen. To login from a Console or a Terminal with an PDC user use the following syntax.

$ su - your_domain.tld\pdc_user

The default $HOME for all PDC users is /home/YOUR_DOMAIN/pdc_user. 

In order to perform GUI logins exit to main CentOS 7 Login Screen, click on Not listed? link, supply your PDC user and password in the form of your_domain\pdc_user and you should be able to login onto your machine as a PDC user 

Enable PDC Integration System-Wide

To automatically reach and authenticate to Zentyal PDC after every system reboot you need to enable Samba and Winbind daemons system-wide by issuing the following commands with root privileges.

# systemctl enable smb
# systemctl enable nmb
# systemctl enable winbind





