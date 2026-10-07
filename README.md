# Ancora-Education-Ucertify-Lab12
# USING IPTABLES COMMAND TO CREATE A PERSONAL FIREWALL IN LINUX

> **Original Lab Source**

> This lab was available through:

> [https://ancoraeducation.ucertify.com/app/?func=ebook&chapter_no=5#top]

1.LINUX: To verify that iptables is installed enter the following command:
```bash
sudo dpkg -l | grep iptab
```
if any information about iptables is returned you know it is installed

2. LINUX: Issue the following command to determine your system's interface ie. eth0,eth1,etc
```bash
sudo ip addr
```
write the name of the interface your system is currently using in a piece of paper
in the following steps you will enter the name of your system's interface when appropriate

3.LINUX:Issue the following command to flush all rules from the inout chain:
```bash
sudo iptables -F
```
4.WINDOWS:Search to open the command prompt and enter ping commands to verify that you can ping Linux (IP
address)
```bash
ping IP address
```
5.WINDOWS: Verify that you can ping Linux

NOTE:Steps 5 and 6 are necessary to ensure taht both Linux and Windows systems know iptables is blocking packets
in the following steps. Otherwise a simple network error or misunderstanding will cause problems with the lab later on.

6.LINUX:The following command specifies to drop all ICMP packets sent from any host. Issue the following
command making sure to substitute the correct interface for your system:
```bash
sudo iptables -I INPUT -i eth0 -p icmp -s 0/0 -d 0/0 -j DROP
```
NOTE: Ensure that you substitute the correct interface in the command if your interface is something other than "eth0"

NOTE:This command causes iptables to add a rule to the INPUT chain that rejects all ICMP packets from all sources
(-s 0/0) to all destinations (-d 0/0). In iptables the -i option specifies the input device. Notice that you must specify the
INPUT chain, not the input chain; case is important for the iptables commands.

7.LINUX: Issue the following command to log this rejection:
```bash
sudo iptables -I INPUT -i eth0 -p icmp -s 0/0 -d 0/0 -j LOG
```
NOTE:Ensure that you substitute the correct interface in the command if your interface is something other than "eth0"

8.WINDOWS: Try to ping Linux. You will not receive any echo reply messages from Linux.

9.LINUX: Now list all your chains:
```bash
sudo iptables --line-numbers -nL
```
You will notice that the input chain contains the ICMP rules you created, complete with line numbers. This option is
helpful when you have a long list of rules.

10.LINUX: Issue the following command to flush all rules from the input chain:
```bash
sudo iptables -F
```
11. WINDOWS: After the rules get flushed in Linux, you will see that you can ping your Linux's host again.
    
12.WINDOWS: Stop pinging Linux.

13.LINUX:Before you flush the remaining rules, use the following command to save your existing rules to a text file:
```bash
sudo iptables-save > iptablesrules.txt
```
14.LINUX: Issue the following command to view the contents of the iptablesrules.txt file:
```bash
sudo less iptablesrules.txt
```
NOTICE that the contents are simple commands within a simple text file. If you do not see any commands, use the
iptables command to create some rules, then issue the iptables-save command again, as written above.

15.LINUX: Enter q to quit viewing the iptablesrules.txt file.

16.LINUX: Flush the iptables rules from your system:
```bash
sudo iptables -F
```
17.LINUX: Now use the iptables-restore command to restore your personal desktop firewall:
```bash
sudo iptables-restore < iptablesrules.txt
```
In this lab you created a persoanl firewall on your Linux system.

## Disclaimer

This repository is for **educational and personal learning purposes only**.  

The original lab content belongs to **uCertify / Ancora Education** and remains their copyrighted material.  
This repository is not affiliated with, endorsed by, or sponsored by uCertify or Ancora Education.  

No copyright infringement is intended.  
Use of any tools or techniques mentioned here should only be performed in authorized, legal environments.
