**Changing Your Network Information :** 
- *Assigning a New IP Address* : sudo ifconfig eth0 192.168.1.11
- *[[Changing]] Your Network Mask and Broadcast Address*: sudo ifconfig eth0 192.168.181.115 netmask 255.255.0.0 broadcast 192.168.1.255
- *[[Spoofing]] Your [[MAC]] Address* : 
		kali> sudo ifconfig eth0 down
		kali> sudo ifconfig eth0 hw ether 00:11:22:33:44:55 
		kali> sudo ifconfig eth0 up
- *Assigning New [[IP]] Addresses from the DHCP Server* : sudo dhclient eth0
____
**Manipulating the Domain Name System :**
- *dig domain.com :* gather DNS information about a target domain.
	- dig domain.com mx :mx is short for mail exchange server.
-*Changing Your DNS Server* : sudo mousepad /etc/resolv.conf