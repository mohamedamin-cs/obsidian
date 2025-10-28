![[img/Pasted image 20250826140020.png]]
From a security standpoint, look for domain names that appear almost like real ones but have small differences (this is called **typosquatting**)
# http message
![[img/Pasted image 20250906175003.png]]
- start line  : http request / response
- header
- empty line
- body
___
![[img/Pasted image 20250906181001.png]]
# [[HTTP methods]]
- GET : used to **fetch** data from the server without making any changes
- POST : **send** data to the server
- PUT : **replace** or **update** something in the server
- DELETE : removes something from the server
- PATCH : Updates part of a resource. It’s useful for making small changes without replacing the whole thing
- HEAD : works like GET but only retrives header
- OPTIONS : tells you what methods are available for a spesific ressourse
- TRACE : Similar to OPTIONS, it shows which methods are allowed, often for debugging
- CONNECT : create **secure** connection (HTTPS)
# HTTP Version
- HTTP/0.9 : only supports GET
- HTTP/1.0 : Added headers and better support for different types of content, improving caching.
- HTTP/1.1 : Brought persistent connections, chunked transfer encoding, and better caching. It’s still widely used today.
- HTTP/2.0 : Introduced features like multiplexing, header compression, and prioritisation for faster performance.
- HTTP/3.0 : Built on HTTP/2, but uses a new protocol (QUIC) for quicker and more secure connections.
---
# Request header
- Host: tryhackme.com
- User-Agent: Mozilla/5.0
- Referrer: https://google.com/
- Cookie: user_type=student; room=introtowebapplication; room_status=in_progress
- Content-Type: application/json
# Request body
## forms
- **URL Encoded (application/x-www-form-urlencoded)** : 
```http
POST /profile HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 33

name=Aleksandra&age=27&country=US
```
- **Form Data (multipart/form-data)** : used to send binary data, such as when uploading files or images to a web server ; 
	----WebKitFormBoundary7MA4YWxkTrZu0gW
```http
POST /upload HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="username"

aleksandra
----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="profile_pic"; filename="aleksandra.jpg"
Content-Type: image/jpeg

[Binary Data Here representing the image]
----WebKitFormBoundary7MA4YWxkTrZu0gW--
```
- **JSON (application/json)** 
```http
POST /api/user HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/json
Content-Length: 62

{
    "name": "Aleksandra",
    "age": 27,
    "country": "US"
}
```
- **XML (application/xml)**
```http
POST /api/user HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/xml
Content-Length: 124

<user>
    <name>Aleksandra</name>
    <age>27</age>
    <country>US</country>
</user>
```
# HTTP Response: Status Line and Status Codes
- first line in HTTP response is **status line** (HTTP version / status code/ reason phrase(explains status code))
- **Informational Responses (100-199)** :  It’s a "keep going" signal.
- **Successful Responses (200-299)** : everything worked as expected
- **Redirection Messages (300-399)** : resource you requested has moved to a different location
- **Client Error Responses (400-499)** : indicate a problem with the request
- **Server Error Responses (500-599)** : the server encountered an error while trying to fulfil the request
- ***common status code*** :
	- 100 (continue)
	- 200 (ok)
	- 301 (moved permanantly)
	- 404 (not found)
	- 501 (internal server error)