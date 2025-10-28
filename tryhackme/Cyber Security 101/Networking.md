## Networking Core Protocols

[[HTTP]] : GET/POST/PUT/DELETE
[[FTP]] : 
- `USER` is used to input the username
- `PASS` is used to enter the password
- `RETR` (retrieve) is used to download a file from the FTP server to the client.
- `STOR` (store) is used to upload a file from the client to the FTP server.
  (`type ascii` switched to ASCII mode as this is a text file)
[[SMTP]] :  how a mail client talks with a mail server and how a mail server talks with another.
- `HELO` or `EHLO` initiates an SMTP session
- `MAIL FROM` specifies the sender’s email address
- `RCPT TO` specifies the recipient’s email address
- `DATA` indicates that the client will begin sending the content of the email message
- `.` is sent on a line by itself to indicate the end of the email message
  email sent via `telnet` port 25
[[POP3]] : allow the client to communicate with a mail server and retrieve email messages.
![[Pasted image 20250706183453.png]]
- `USER <username>` identifies the user
- `PASS <password>` provides the user’s password
- `STAT` requests the number of messages and total size
- `LIST` lists all messages and their sizes
- `RETR <message_number>` retrieves the specified message
- `DELE <message_number>` marks a message for deletion
- `QUIT` ends the POP3 session applying changes, such as deletions
[[IMAP]] :allows synchronization of messages across multiple devices instead of deleting a message after retrieving it .
- `LOGIN <username> <password>` authenticates the user
- `SELECT <mailbox>` selects the mailbox folder to work with
- `FETCH <mail_number> <data_item_name>` Example `fetch 3 body[]` to fetch message number 3, header and body.
- `MOVE <sequence_set> <mailbox>` moves the specified messages to another mailbox
- `COPY <sequence_set> <data_item_name>` copies the specified messages to another mailbox
- `LOGOUT` logs out
___
## Networking Secure Protocols

- [[TLS]] (Transport Layer Security
 1. Key Pair Generation(public and private)
 2. server admin creat CSR(Certif Signe Request)
 3. submit to CA(Certificate Authority)
 4. CA Verifies Domain Ownership
 5. CA Issues the TLS Certificate
-  secure protcols like https is HTTP + TLS
___
- [[traceroute]] : uses ICMP to discover the route from your host to the target.
- TTL = time to live
- **[[routing]]** :
	- **[[OSPF]] (Open Shortest Path First)**: OSPF is a routing protocol that allows routers to share information about the network topology and calculate the most efficient paths for data transmission. It does this by having routers exchange updates about the state of their connected links and networks. This way, each router has a complete map of the network and can determine the best routes to reach any destination.
	- **[[EIGRP]] (Enhanced Interior Gateway Routing Protocol)**: EIGRP is a Cisco proprietary routing protocol that combines aspects of different routing algorithms. It allows routers to share information about the networks they can reach and the cost (like bandwidth or delay) associated with those routes. Routers then use this information to choose the most efficient paths for data transmission.
	- **[[BGP]] (Border Gateway Protocol)**: BGP is the primary routing protocol used on the Internet. It allows different networks (like those of Internet Service Providers) to exchange routing information and establish paths for data to travel between these networks. BGP helps ensure data can be routed efficiently across the Internet, even when traversing multiple networks.
	- **[[RIP]] (Routing Information Protocol)**: RIP is a simple routing protocol often used in small networks. Routers running RIP share information about the networks they can reach and the number of hops (routers) required to get there. As a result, each router builds a routing table based on this information, choosing the routes with the fewest hops to reach each destination.
___
- [[DHCP]] : Discover - Offer - Request - Acknowlage.
___

| INSECURE | SECURE            |
| -------- | ----------------- |
| HTTP 80  | [[HTTPS]] 443     |
| FTP 21   | [[FTPS]] 990      |
| IMAP 143 | [[IMAPS]] 993     |
| POP3 110 | [[POP3S]] 110     |
| SMTP 25  | [[SMTPS]] 465/587 |
____
Server Message Block ([[SMB]]) is a **communication protocol** . provide shared access to files and printers across nodes on a network of systems running IBM's OS/2. It also provides an authenticated inter-process communication (IPC) mechanism.

[[NetBIOS]] (Network Basic Input Output System), similar to SMB, allows computers to communicate over the network to share files or send files to printers
The NetBIOS name of the target system can give you an idea about its role and even importance(e.g. CORP-DC, DEVOPS, SALES, etc...).