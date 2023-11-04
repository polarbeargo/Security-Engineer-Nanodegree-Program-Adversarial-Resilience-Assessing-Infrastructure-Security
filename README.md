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
Is this system compliant?
Ans: No, The path from CIS is not exsist. An additional group policy template is required to add MS security group. 
![image18]
The registry entry “DisableExceptionChainValidation” is not available.

From the below screenshots vnc is installed on both the Linux and ubuntu machine.

![image16] ![image17]

#### Task 4: 

### Step 2: Assess Access Management at Targeted Assets  
#### Task 1: 
#### Task 2: 
#### Task 3: 
#### Task 4: 

### Step 3: Log Monitoring Setup for Detection at Targeted Assets  

#### Task 1: 
#### Task 2: 
#### Task 3: 
#### Task 4: 

### Step 4: Assess Authentication Management at Targeted Assets 
#### Task 1: 
#### Task 2: 
#### Task 3: 
#### Task 4: 


[Final Report](2022-staticspeed-vunerability-report-template.pdf)