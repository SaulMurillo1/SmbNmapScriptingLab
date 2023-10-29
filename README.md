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
 Command: ping 10.3.26.54
 <br/>
<br/>
<img src="https://i.imgur.com/cY5DR4T.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
Run Nmap scan against target machine IP: <br/>
- It looks like the target has multiple tcp ports open with SMB (port 445) being one of the open ports. <br/>
<br/>
Command: nmap 10.3.26.54
<br/>
<br/>
<img src="https://i.imgur.com/zRfdBFt.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
Run Nmap script that will list supported SMB protocols: <br/>
- You can see that once of the dialects is SMBv1 which is dangerous, but default. <br/>
<br/>
Command: nmap 10.3.26.54 -445 --script smb-protocols
<br/>
<br/>
<img src="https://i.imgur.com/PIx2jcz.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
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
