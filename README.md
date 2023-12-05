# Security Engineer Nanodegree Program Adversarial Resilience Assessing Infrastructure Security  
 [image1]: ./images/zenmap_ubun.png  
 [image2]: ./images/zenmap_win.png
 [image3]: ./images/nmap_ubuntu.png
 [image4]: ./images/nmap_win_script.png
 [image5]: ./images/ubuntu_script.png
 [image6]: ./images/ubuntu_script2.png
 [image7]: ./images/win_script.png
 [image8]: ./images/samba.png
 [image9]: ./images/ssh.png
 [image10]: ./images/ubuntu_ssh.png
[image11]: ./images/auditStaticSpeeds.png
[image12]: ./images/checkSoftwareUpdate.png
[image13]: ./images/passwdPolicy.png
[image14]: ./images/softwareUpdate.png
[image15]: ./images/windowsUpdate.png
[image16]:images/VNC_ubuntu.png
[image17]:images/vnc_win.png  
[image18]:images/win_software.png
[image19]:images/enableSEHOP.png
[image20]:images/CIS1.6.1.png
[image21]:images/1.6.1.png
[image22]:images/ubuntu_VPN.png
[image23]:images/win_VPN.png
[image24]:images/win_policy.png
[image25]:images/policy_linux.png
[image26]:images/AnonymousAccess.png
[image27]:images/ubuntu_firewall.png
[image28]:images/firewall_win.png
[image29]:images/PII_win.png
[image30]:images/PII_ubuntu.png
[image31]:images/guest_ubuntu.png
[image32]:images/Win_guest_pre.png
[image33]:images/ubutu_guest_pre.png
[image34]:images/bruteforce1.png
[image35]:images/bruteforce2.png
[image36]:images/syslogubuntu.png
[image37]:images/syslogwin.png
[image38]:images/usernamePasswd.png
[image39]:images/file_config.png
[image40]:images/allowLogOnThroughRemote.png
[image41]:images/rootAcessLinux.png
[image42]:images/ssh_config.png
[image43]:images/CIS531ubuntu.png
[image44]:images/cis1152in.png
[image45]:images/ftpSecurityubuntu.png
[image46]:images/nmapSMB.png
[image47]:images/cypher.png
[image48]:images/FIPS.png

### Step 1: Asset identification, address update, dependencies, patches, and native protections at targeted Server/ Desktop Operating Systems

#### Task 1:   
- To use Nmap for Vulnerability Discovery, we need use NSE scripts from Vulscan and Vulners GitHub repositories.

```
git clone https://github.com/scipag/vulscan
git clone https://github.com/vulnersCom/nmap-vulners
```
Also visit https://nmap.org/download#windows to download the latest version of Nmap for Windows.  
- We need to use NSE scripts from Vulscan and Vulners GitHub repositories.

```
sudo nmap -sV --script vuln 10.0.2.4 (Or 10.0.2.6)
```
![image5] ![image6] ![image7]
- Use Zenmap to scan the target IPv6 address.  

```
nmap -sV -6 fe80::5635:9f35:5f5a:1cf9 (Scan IPv6 IP address)
```  
![image1] ![image2]  

- To Discover Unpatched Services on the Linux machine, run the following commands to examine ssh and samba services:  

```
nmap -sV -p 445 10.0.2.6 
nmap -sV -p 22 10.0.2.6
```

![image8] ![image9]  
- We also able to discover unpatched services on the Linux system by running the following command:  

```
ssh -v localhost
samba --version
``````  
![image10]  

- We can see they are not the most updated version of the SSH and  SAMBA versions. OpenSSH 7.6 can be upgraded to OpenSSH 8 and CVE-2020-1472 is the recent security update for this SAMBA version.

#### Task 2: 

On ubuntu we can check software update by the following commands:
```
 sudo apt-cache policy
```
![image14]
Or
```
sudo apt-key list
```
![image12]
We check the status of software updates in Group Policy Object Editor, click either of the Administrative Templates > Windows components > Windows Update.

![image15]
We audit StaticSpeeds systems by the following commands on Linux:

```
grep 'minlen' /etc/security/pwquality.conf
```
![image11]  
On Windows:
We can view password policies by searching for "Local Security Policy" using the windows search feature, and navigating to "Account Policy" > "Password Policy"

![image13]

#### Task 3:   
Windows CIS 18.3.4
Ensure 'Enable Structured Exception Handling Overwrite Protection (SEHOP)' is set to 'Enabled.'

- Click Start, click Run, type regedit, and then press ENTER.
- Locate the following registry subkey:
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\kernel\DisableExceptionChainValidationNote If you cannot find the DisableExceptionChainValidation registry entry under the HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\kernel\ subkey, follow these steps to create it:


    - Right-click kernel, point to
New, and then click DWORD Value.
    - Type
DisableExceptionChainValidation, and then press ENTER.
- Double-click
DisableExceptionChainValidation.
- Change the value of the DisableExceptionChainValidation registry entry to 0 to enable it, and then click OK.

Note A value of 1 disables the registry entry. A value of 0 enables it.
- Exit Registry Editor.
![image19]
Is this system compliant?
Ans: No, The path from CIS is not exsist. An additional group policy template is required to add MS security group. 
![image18]
The registry entry “DisableExceptionChainValidation” is not available.

From the below screenshots vnc is installed on both the Linux and ubuntu machine.

![image16] ![image17]

Ubuntu CIS 1.6.1, 1.6.2
1.6.1 Ensure XD/NX support is enabled
```
journalctl | grep 'protection: active'
```
![image21]
1.6.2 Ensure address space layout randomization (ASLR) is enabled
Run the following command:
```
kernel.randomize_va_space = 2
```
![image20]

#### Task 4: 
Perform a network asset inventory using Nmap to identify VMs with open ports on both Windows and Linux
![image5]

### Step 2: Assess Access Management at Targeted Assets  
#### Task 1: 
I don’t see any VLANs in the following screenshots.
```
ifconfig -a
```
![image22]

```
ipconfig /all
```
![image23]  

There’s no any policy in the following screenshots:

![image24] ![image25]
From the following screenshots we can see the anonymous access has not been granted.
![image26]
#### Task 2: 
#### Task 3: 
On windows we check firewall status by the following command:
```
netsh advfirewall show allprofiles state
```
 ![image28]  
On Ubuntu we use the following command:

```
ufw status
```
 ![image27]  
#### Task 4: 

 Conduct a Principles of Least Privilege assessment of StaticSpeed's system. We need to know: 
- Which users have high privileges? 
- Do important PII folders have the correct permissions and ownership? 
- Are the default settings correct, and are there any excessive permissions? 
- On our initial scan, we found "data" shared folders that need further investigation.
- Are there "guest" accounts enabled? Are they allowed to use Sudo commands? Are they allowed to log in to ALL workstations?. 

In windows, In windows locat “data” folder under "This PC" and see the properties and permissions it has.

![image29]


We can find this folder "data" in documents in linux.
![image30]
![image31]
From the above screenshots we can see ustudent have the high privileges for both windows and ubuntu machine. There’s "guest" accounts enabled you can see it from the above ubuntu screenshots. There’s no guest account in windows machine see below screenshot:
![image32]
![image33]
Run the following command to check if the guest account has administrator privileges:
```
getent group| grep admin
```
and
```
getent group| grep sudo
```
From above screenshot we can see ubuntu guest doesn’t has administrator privileges.


### Step 3: Log Monitoring Setup for Detection at Targeted Assets  

#### Task 1:  

We found that IP 10.0.2.7, which performs a port scan and a brute force assault against SMB 445, is the source of the attack.
It appears that the password was compromised and the FTP on port 21 was open to brute force attacks.
![image35]
![image34]

The following are the password was used successfully and username was compromised.
![image38]

#### Task 2: 
We suspect that an internal user may have compromised another machine inside StaticSpeed's network and pivoted to one of the devices you are auditing. Please use lateralmovement.pcap and determine the following:

- What was the source IP of the "initial" attack?
- Did the attacker try to access your machine from a compromised device - MITRE ATT&CK Technique T1021? 
- What service and port were targeted?
- Was the attacker able to access a sensitive file at the machine you are auditing? Mitre ATT&ACK Technique - T1570

We found that IP 10.0.2.7, which performs a port scan and a brute force assault against SMB 445, is the source of the attack. Yes attacker try to access our machine from a compromised device - MITRE ATT&CK Technique T1021. FTP  on port 21 was open to brute force attacks. Yes as you can see the screenshots from previous task the attacker use built-in file sharing protocols, such as file sharing across SMB/Windows Admin Shares to linked network shares or with authenticated connections via Remote Desktop Protocol, to create, copy files between inside victim systems to enable lateral movement.  

#### Task 3: 

We can spot EventID 4625 in our windows log ans in linux we can see username “nobody” is trying to access the certain things.
![image36]
![image37]

#### Task 4:  

To make sure that the right logging is enabled, check the contents of the /etc/rsyslog.conf by running the following command:
cat  /etc/rsyslog.conf 
We can see  the /etc/rsyslog.conf and set $FileCreateMode to 0640.
![image39]

### Step 4: Assess Authentication Management at Targeted Assets 
#### Task 1: 

By Start > Run > gpedit.msc.
Expand: Computer Configuration > Windows Settings > Security Settings > Local Policies > User Rights Management.
Select: Allow log on through Remote Desktop Services. And sudo cat /etc/sudoers we can see administrators can remotely access windows machines and root access is permitted at the Linux host. 
![image40]
![image41]

From the /etc/ssh/sshd_config file, we can see it doesn’t permit root login via ssh.
![image42]

There’s no users with excessive permissions and root remote login isn’t allowed
There’s no any users that should not have remote access via ssh in Linux.
Remote Desktop Access should only be granted to administrators in Windows there are other accounts “Remote Desktop User” given access.

#### Task 2: 

On Linux use the following command:
We modified Password Length:
minlen = 14 - password must be 14 characters or more 
Password complexity:
minclass = 4 - The minimum number of required classes of characters for the new password (digits, uppercase, lowercase, others) 
![image43]
On windows:
Searching for "Local Security Policy" using the windows search feature, and navigating to "Account Policy" > "Password Policy". We set at least six characters in length and enable password must meet complex requirements.
![image44]

#### Task 3: 
From the following screenshots, these systems are compliant with FIPS 140-2 within the infrastructure. On Windows we enable FIPS configuration.
![image48]
On ubuntu we edit the /etc/ssh/sshd_config file add/modify the Ciphers line to contain a comma separated list of the site approved ciphers.
![image47]

#### Task 4: 

On windows machine we can clear see there is a vulnerability on port 445 with the command 
```
nmap -p 445 --script smb-security-mode.nse 10.0.2.4
```
![image46]

On ubuntu we run the following command to check ftp service:

```
nmap –script ftp-brute 10.0.2.5 -p 21
```
![image45]


[Final Report](2022-staticspeed-vunerability-report-template.pdf)