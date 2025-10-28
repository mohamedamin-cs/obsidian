**[[binaries]] :** files that can be executed.
**scripts :** a series of commands run in an interpretive environment that converts each line to source code.
**[[shell]] :** environment and interpreter for running commands in Linux.
**subdirs of / :** 
- **/root** The home directory of the all-powerful root user 
- /etc Generally contains the Linux configuration files—files that control when and how programs start up 
- **[[/home]]** The user’s home directory.
- **[[/mnt]]** Where other filesystems are attached or mounted to the filesystem
- **[[/media]]** Where CDs and USB devices are usually attached or mounted to the filesystem.
- **[[/bin]]** Where application binaries (the equivalent of executables in Microsoft Windows or applications in macOS) reside.
- **[[/lib]]** Where you’ll find libraries (shared programs that are similar to Windows DLLs).

**Searching with locate :** `locate aircrack-ng`
**Finding Binaries with whereis :** `whereis aircrack-ng`
**Using sed to Find and Replace :** sed s/o/0/g /usr/share/metasploitframework/data/wordlists/unix_passwords.txt > /usr/share/metasploitframework/data/wordlists/unix_passwords2.txt
