<h1>SMB Nmap Scripting</h1>


<h2>Description</h2>
This project consists of using Nmap as a Linux tool to enumerate SMB (port 445) security level information, active sessions, shares, users, domains, services, etc.  The target machine is running the SMB service. 
<br />
<br />

Disclaimer: The Kali Linux user machine and target machine used in this project was provided to me by INE for educational purposes. The misuse of the information in this project lab can result in criminal charges brought against the individual/individuals in question.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Nmap</b>


<h2>Environments Used </h2>

- <b>Kali Linux</b>

<h2>Project walk-through:</h2>

<p align="left">
Ping the target machine to discover if it is active: <br/>
- As you can see, we are getting replies from target machine. <br/>
 <br/>
 Command: ping 10.3.16.16
 <br/>
<br/>
<img src="https://i.imgur.com/HUofwPj.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap scan against target machine IP: <br/>
- It looks like the target has multiple tcp ports open with SMB (port 445) being one of the open ports. <br/>
<br/>
Command: nmap 10.3.16.16
<br/>
<br/>
<img src="https://i.imgur.com/RDRsTdV.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script that will list supported SMB protocols: <br/>
- You can see that one of the dialects is SMBv1 which is dangerous, but default. <br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-protocols
<br/>
<br/>
<img src="https://i.imgur.com/qdtJ5se.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script that will enumerate SMB security level: <br/>
- It looks like this SMB server has message signing disabled which is dangerous. If message signing isn't required, the SMB server may be vulnerable to man-in-the-middle attacks or SMB-relay attacks.<br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-security-mode
<br/>
<br/>
<img src="https://i.imgur.com/0pxODL1.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script that will enumerate users logged into system through SMB share: <br/>
- Since we are running this script without SMB server credentials, this Nmap script will only enumerate any user sessions that were accessed without any credentials. It looks like user bob is logged in without any credentials, which is possible due to the target machine having the guest login enabled.<br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-enum-sessions
<br/>
<br/>
<img src="https://i.imgur.com/uA64dCC.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script that will enumerate users logged into system through SMB share: <br/>
- This is same command as before but with the knowledge of knowing the SMB server credentials. As you can see, there is now a new active session that states "it's probably you".<br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-enum-sessions --script-args smbusername=administrator,smbpassword=*password_hidden_for_privacy*
<br/>
<br/>
<img src="https://i.imgur.com/yAyHd7M.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script that will enumerate all available shares: <br/>
- We can see all of the shares using guest users along with the permission of each folder or drive. Also, we can see that the IPC$ share has read and write permissions. The IPC$ share is also known as a null session connection which means that Windows lets anonymous users perform certain activites, such as enumerating the names of domain accounts and network shares.<br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-enum-shares
<br/>
<br/>
<img src="https://i.imgur.com/CwZWsDF.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Using valid SMB credentials, run Nmap script that will enumerate all available shares: <br/>
- We can now see a bit more information, such as the administrator has full read and write privileges to the entire C$.<br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-enum-shares --script-args smbusername=administrator,smbpassword=*password_hidden_for_privacy*
<br/>
<br/>
<img src="https://i.imgur.com/Wg2yiOl.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
 <img src="https://i.imgur.com/DYScVEa.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script that will enumerate Windows users on the target machine: <br/>
- We can see that there are three users on the target machine (Administrator, bob, & Guest).<br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=*password_hidden_for_privacy*
<br/>
<br/>
<img src="https://i.imgur.com/ppEpbRK.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script that will enumerate SMB server statistics: <br/>
- We can see statistics, such as failed logings, permission errors, system errors, etc.<br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-server-stats --script-args smbusername=administrator,smbpassword=*password_hidden_for_privacy*
<br/>
<br/>
<img src="https://i.imgur.com/xdWcvfd.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script that will enumerate available domains on the target machine: <br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-enum-domains --script-args smbusername=administrator,smbpassword=*password_hidden_for_privacy*
<br/>
<br/>
<img src="https://i.imgur.com/rWl9yWu.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script that will enumerate available user groups on the target machine: <br/>
<br/>
Command: nmap 10.3.16.16 -p 445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=*password_hidden_for_privacy*
<br/>
<br/>
<img src="https://i.imgur.com/rOYtILz.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
