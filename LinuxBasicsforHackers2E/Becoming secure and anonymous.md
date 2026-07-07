`kali> mousepad /etc/proxychains4.conf` : 
`proxychains <your command> <arguments>` : make traffic harder to trace (/etc/you can edit proxychain.conf).
 https://geonode.com/free-proxy-list : free proxies.
 [[proxychains]] defaults to using Tor on port 9050.
 use protonmail 
```
\# dynamic_chain
\# 
\# Dynamic – Each connection will be done via chained proxies 
\# all proxies chained in the order as they appear in the list 
\# at least one proxy must be online to play in chain 
\# 
\# strict_chain 
\# 
\# Strict - Each connection will be done via chained proxies 
\# all proxies chained in the order as they appear in the list 
\# all proxies must be online to play in chain 
\# otherwise EINTR is returned to the app 
\# random_chain 
\# 
\# Random - Each connection will be done via random proxy 
\# (or proxy chain, see chain_len) from the list. 
\# this option is good to test your IDS :) 
\# Makes sense only if random_chain 
chain_len = 3
```
