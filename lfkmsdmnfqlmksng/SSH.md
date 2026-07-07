## 🛠️ Step 1: Prepare the Host (Server) PC

The Host is the remote machine you want to connect _into_.

### 1. Install OpenSSH Server

Depending on the Host operating system:

- **Arch Linux / Fedora:**
    
    Bash
    
    ```
    sudo pacman -S openssh   # Arch
    sudo dnf install openssh-server # Fedora
    ```
    
- **Ubuntu / Debian:**
    
    Bash
    
    ```
    sudo apt update && sudo apt install openssh-server
    ```
    
- **Windows (PowerShell as Admin):**
    
    PowerShell
    
    ```
    Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
    ```
    

### 2. Start and Enable the SSH Service

Ensure the service runs automatically on boot.

- **Linux (systemd):**
    
    Bash
    
    ```
    sudo systemctl enable --now sshd
    ```
    
- **Windows (PowerShell):**
    
    PowerShell
    
    ```
    Start-Service sshd
    Set-Service -Name sshd -StartupType 'Automatic'
    ```
    

### 3. Find the Host's Local IP Address

Run the following on the Host machine to get its IP (e.g., `192.168.1.50`):

- **Linux:** `ip a | grep inet`
    
- **Windows:** `ipconfig`
    

## 💻 Step 2: Connect from the Client PC

Open your terminal (or PowerShell/Alacritty) on your main PC.

### Password Authentication (Basic)

Run the following command replacing `username` and `ip_address` with the Host's details:

Bash

```
ssh username@remote_ip_address
```

_Example:_ `ssh amindev@192.168.1.50`

> ⚠️ **First Time Warning:** You will see a prompt saying: _"The authenticity of host... can't be established."_ Type `yes` and hit Enter. Then, enter the password of the Host user account.

## 🔒 Step 3: Set Up Secure Key-Based Authentication (Recommended)

Password-less authentication via cryptographic keys is faster and significantly more secure against brute-force attacks.

### 1. Generate SSH Keys on the Client

If you don't already have an SSH key pair on your client machine, generate one using Ed25519 (highly secure and efficient):

Bash

```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

_Press Enter to accept default paths and set an optional passphrase._

### 2. Copy the Public Key to the Host Machine

- **From a Linux Client:**
    
    Use the built-in utility to automatically copy it over:
    
    Bash
    
    ```
    ssh-copy-id username@remote_ip_address
    ```
    
- **From a Windows Client (or manual method):**
    
    Append the contents of your client's local `~/.ssh/id_ed25519.pub` file into the remote host's `~/.ssh/authorized_keys` file.
    

### 3. Test the Connection

Run the connection command again. It should log you in instantly without prompting for the user account password:

Bash

```
ssh username@remote_ip_address
```

## ⚙️ Step 4: Hardening the SSH Daemon (Optional)

To improve security, edit the configuration file on the **Host** machine: `/etc/ssh/sshd_config` (Linux).

Bash

```
sudo nvim /etc/ssh/sshd_config
```

Make the following modifications for a production-like local environment:

- Change the default port to a custom one (e.g., `Port 2222`).
    
- Disable root login: `PermitRootLogin no`.
    
- Disable password authentication entirely (only allow SSH keys): `PasswordAuthentication no`.
    

_Remember to restart the daemon after editing:_ `sudo systemctl restart sshd`

## 🔍 Troubleshooting Checklist

- [ ] **Connection Timed Out:** Check if a firewall is blocking port 22 on the Host.
    
    - _UFW (Ubuntu):_ `sudo ufw allow ssh`
        
    - _iptables/nftables:_ Ensure port 22 is open.
        
- [ ] **Connection Refused:** Double-check if the `sshd` service is actually running on the Host.
    
- [ ] **Wrong Network:** Verify both devices are assigned to the exact same subnet mask by your router.