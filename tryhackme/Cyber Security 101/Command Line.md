## [[Windows]] command line :

- set : check your path from the command line.
- ipconfig : /all.
- ver : determine OS.
- systeminfo : info about os.
- ping
- **[[netstat]]** -abon : displays current network connections and listening ports.
- **[[tracert]]** target_name : traces the network route traversed to reach the target.
- **[[nslookup]]** example.com : looks up a host or domain and returns its IP address.
___
- cd 
- dir = ls
- tree
- mkdir/rmdir
- copy
- move
- del/erase/rm
- * = multiple files
___
- tasklist
- /? = -h
- tasklist /FI "imagename eq sshd.exe" : search for tasks related to `sshd.exe`
## [[Powershell]] :
- Get-Content: Retrieves (gets) the content of a file and displays it in the console.
- Set-Location: Changes (sets) the current working directory.
- Get-Command (Get-Command -CommandType "Function")
- **Get-Help** = -h (Get-Help Command)
- Get-Alias : `dir` is an alias for `Get-ChildItem`
- Find-Module -Name "PowerShell*"
- Install-Module -Name "PowerShellGet"
- Get-ChildItem = ls
- Set-Location -Path ".\Documents" = cd
- New-Item -Path ".\captain-cabin\captain-wardrobe" -ItemType "Directory"
- Remove-Item -Path ".\captain-cabin\captain-wardrobe\captain-boots.txt"
- Get-Content -Path ".\captain-hat.txt" = cat
___
- Get-ChildItem | Sort-Object Length
- Get-ChildItem | Where-Object -Property "Extension" -eq ".txt" :
	- `-ne`: "**not equal**".
	- `-gt`: "**greater than**".
	- `-ge`: "**greater than or equal to**". 
	- `-lt`: "**less than**".
	- `-le`: "**less than or equal to**".
- Select-String -Path ".\captain-hat.txt" -Pattern "hat"
___
- Get-ComputerInfo
- Get-LocalUser
- Get-NetIPConfiguration
- Get-NetIPAddress
___
- Get-Process
- Get-Service
- Get-NetTCPConnection
- Get-FileHash
___
