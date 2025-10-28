- **Remote System Control**: allows the attacker to execute commands or software remotely in the target system.
- **Privilege Escalation**: If initial access through a shell is limited or restricted, attackers can explore ways to escalate privileges to more elevated or administrative access.
- **Data Exfiltration**: Once attackers have access to execute commands through an obtained shell, they can explore the system to read and copy sensitive data from it.
- **Persistence and Maintenance Access**: Once shell access is obtained, attackers can create access through users and credentials or copy backdoor software to maintain access to the target system for later usage.
- **Post-Exploitation Activities**: After access to a shell is granted, attackers can perform a wide range of post-exploitation activities, such as deploying malware, creating hidden accounts, and deleting information.
- **Access Other Systems on the Network**: Depending on the attacker's intentions, the obtained shell can be just an initial access point. The goal can be to hop through the network to a different target using the obtained shell as a pivot to different points in the compromised system network. This is also known as pivoting.
____
- ***[[A reverse shell]]***, sometimes referred to as a "connect back shell,"
```
-> ncat --ssl -lnvp 4444 #improved version of Netcat

-> rlwrap nc -lnvp 4444 #This wraps `nc` with `rlwrap`, allowing the use of features like arrow keys and history for better interaction.

-> socat -d -d(verbose x2) TCP-LISTEN:443 STDOUT #create a socket connection between two data sources
```
  ___
  A [[web shell]] is a script written in a language supported by a compromised web server that executes commands through the web server itself. A web shell is usually a file containing the code that executes commands and handles files. It can be hidden within a compromised web application or service, making it difficult to detect and very popular among attackers.
  