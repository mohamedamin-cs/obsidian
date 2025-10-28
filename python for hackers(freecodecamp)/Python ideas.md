with open('a.txt', 'w', encoding='utf-8') as fp:
    fp.write(html_content)
 ___
## Virtual Environment
- Create with python3 -m venv ~/myenv
- activate with source ~/myenv/bin/activate
- then install pip install
- pip is the default package installer for Python

| Tool       | Purpose                             | System-Wide on Arch? | Isolation?          | Your Use Case (`a.py`)                        |
| ---------- | ----------------------------------- | -------------------- | ------------------- | --------------------------------------------- |
| **pip**    | Install Python packages             | Restricted (PEP 668) | No (unless in venv) | Avoid; use in virtual environments.           |
| **pip3**   | Install Python 3 packages           | Restricted (PEP 668) | No (unless in venv) | Use in virtual environments or with `--user`. |
| **pipx**   | Run/install apps in isolated envs   | Yes (safe)           | Yes                 | Good for running `a.py` in isolation.         |
| **venv**   | Create isolated Python environments | Yes (safe)           | Yes                 | Best for project-specific setups.             |
| **pacman** | Install system-wide Python packages | Yes (preferred)      | No                  | Simplest for system-wide `requests`.          |
___
![[img/2025-09-05_23-17.png]]

---
## Socket
- INET : ip v4
- socket is a tool that things use to talk to each other ![[img/2025-09-06_16-21.png]]
- **stream** sockets (==TCP==) : Realiable
- **datagram** sockets (==UDP==) : Fast
___
### Fix waypaper caching
sudo sed -i 's/"jpeg"/"png"/g' /usr/lib/python3.13/site-packages/waypaper/common.py
___
mv "/home/aarfi/Pictures/wallpapers/dark-mode-night-mode-abstract-artwork-of-blackhole-viewed-from-earth-colorful-best-most-popular-free-download-wallpapers-for-macbook-pro-and-macbook-air-and-microsoft-windows-desktop-pcs-4k-07-12-2024-1733638236-hd-wallpaper.png" \
   "/home/aarfi/Pictures/wallpapers/blackhole.png"
_____
## Create bootable usb
- sudo umount /dev/sdb*
- sudo dd if=/path/to/file.iso of=/dev/sdb bs=4M status=progress oflag=sync
- sudo eject /dev/sdb