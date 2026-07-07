![[img/Pasted image 20260217193917.png]]

**Send Group in Sequence over a Single Connection**

This option establishes a single connection to the server and sends all the requests in the group’s tabs before closing the connection. This can be useful for testing for potential client-side desync vulnerabilities.

**Send Group in Sequence over Separate Connections**

As the name suggests, this option establishes a TCP connection, sends a request from the group, and closes the TCP connection before repeating the process for the subsequent request.

![[img/Pasted image 20260217203804.png]]
## Send Request Group in Parallel

Choosing to send the group’s requests in parallel would trigger the Repeater to send all the requests in the group at once. In this case, we notice the following, as shown in the screenshot below:

- ***documentation :*** https://portswigger.net/burp/documentation/desktop/tools/repeater/send-group