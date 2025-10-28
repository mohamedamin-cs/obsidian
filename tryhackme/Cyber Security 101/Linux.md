wget :download files from the web via [[HTTP]],example:
wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt
__________________________________________________________________
scp (Secure copy) :transfer files between two computers using the [[SSH]], example:
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
__________________________________________________________________
[[python server]] :Python3's "HTTPServer" will serve the files in the directory where you run the command,example: python3 -m http.server
____________________________________________________________________________
ps: provide a list of the running ([[processes]]) as our user's session, (ps aux)
top/htop: real-time statistics about the processes running
kill PID: kill a command
systemd is th
____________________________________________________________________________
sytemctl :Getting Processes/Services to Start on Boot, systemctl [option]  [service]  ,example: systemctl start [[apache2]]
**options** : 
- Start
- Stop
- Enable
- Disable
____________________________________________________________________________
fg/bg/&/ctrl+Z :bring from (back/fore)ground to (back/fore)ground
____________________________________________________________________________
**APT**  :is a **[[package manager]]** used in Debian-based systems
Software is installed from **repositories** (repos), which are curated collections of packages

- **`/etc/apt/sources.list.d/`**: Directory for custom repository files (one file per repo).
- **`/etc/apt/sources.list`**: Main file for repository entries (used less for custom additions).
- Each repository is signed with a **[[GPG]] key** to ensure package authenticity ,example:  wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
- ### **Manually Adding a Repository**

1. Add GPG key (as above).
    
2. Create a new list file:

	`sudo nano /etc/apt/sources.list.d/sublime-text.list`
    
    Add the repository:
    
    `deb https://download.sublimetext.com/ apt/stable/`
    
3. Update package lists:
    
    `sudo apt update`
    
4. Install the software:
    
    `sudo apt install sublime-text`
    
5. Remove the software:

	 `sudo apt remove sublime-text`
#### pro tip: Always `sudo apt update` after adding/removing repos!(**Update → Install → Remove → Repeat**)
download using **dpkg**: sudo dpkg -i package.**deb**

Key Commands:

| Command                                | What It Does               |
| -------------------------------------- | -------------------------- |
| `sudo apt update`                      | Refresh package lists      |
| `sudo apt install [pkg]`               | Install software           |
| `sudo apt remove [pkg]`                | Uninstall software         |
| `sudo add-apt-repository ppa:name/ppa` | Add a PPA (community repo) |
| `sudo apt-key add [key]`               | Trust a dev’s GPG key      |
____________________________________
### **Linux [[Logs]]**

- **Logs are stored in**: `/var/log/`
    
- **Log Rotation**: Automatically manages old logs to save space (e.g., `logrotate`).
    

---
### **Key Logs to Know**

- **[[Apache2]] Web Server**
    
    - `access.log`: All requests to the server.
        
    - `error.log`: Errors and warnings.
        
- **fail2ban**
    
    - Blocks brute-force attacks.
        
    - Logs found in: `/var/log/fail2ban.log`
        
- **UFW (Firewall)**
    
    - Logs allowed/denied traffic.
        
    - Log file: `/var/log/ufw.log`
        
### **Security Logs**

- **auth.log**: User logins, sudo, SSH attempts.
    
- **syslog**: General system and service messages
## useful commands
- **whois :** retrieves registration and ownership information about a domain name or IP address.
- **tracert** target_name : traces the network route traversed to reach the target.
- **nslookup** example.com : looks up a host or domain and returns its IP address.
- **dig domain.com**  Detailed DNS lookup
- **ip r :** show routing table