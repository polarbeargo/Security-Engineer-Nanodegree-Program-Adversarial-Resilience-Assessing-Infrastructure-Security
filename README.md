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
#### Task 3: 
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

### Step 5: Final Report