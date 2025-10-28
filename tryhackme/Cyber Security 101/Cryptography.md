# Cryptography Basics
- encrypted plaintext = [[cypherthext]]
- **types of [[encryption]] :**
	- [[symmetric encryption]]:
		- ![[Pasted image 20250715113300.png]]
		-  **[[DES]]** uses a 56-bit key.
		- **[[3DES]]** is DES applied three times; the key size is 168 bits, though the effective security is 112 bits. 3DES was more of an ad-hoc solution when DES was no longer considered secure. 3DES was deprecated in 2019 and should be replaced by AES; however, it may still be found in some legacy systems.
		- **[[AES]]** Its key size can be 128, 192, or 256 bits.
	- [[asymmetric encryption]]:
		- ![[Pasted image 20250715113455.png]]
		- Asymmetric encryption tends to be slower
		- asymmetric encryption ciphers use larger keys than symmetric encryption
		- [[RSA]] uses 2048-bit, 3072-bit, and 4096-bit keys; 2048-bit is the recommended minimum key size
		- [[Diffie-Hellman]] also has a recommended minimum key size of 2048 bits but uses 3072-bit and 4096-bit keys for enhanced security.
___
# Public Key Cryptography Basics
### [[RSA]]
- **RSA is a [[public-key]] encryption algorithm that enables secure data transmission over insecure channels. With an insecure channel, we expect adversaries to eavesdrop on it.**
1. Bob chooses two prime numbers: _p_ = 157 and _q_ = 199. He calculates _n_ = _p_ × _q_ = 31243.
2. With _ϕ_(_n_) = _n_ − _p_ − _q_ + 1 = 31243 − 157 − 199 + 1 = 30888, Bob selects _e_ = 163 such that _e_ is relatively prime to _ϕ_(_n_); moreover, he selects _d_ = 379, where _e_ × _d_ = 1 mod _ϕ_(_n_), i.e., _e_ × _d_ = 163 × 379 = 61777 and 61777 mod 30888 = 1. The public key is (_n_,_e_), i.e., (31243,163) and the private key is $(n,d), i.e., (31243,379).
3. Let’s say that the value they want to encrypt is _x_ = 13, then Alice would calculate and send _y_ = _x^e_ mod _n_ = 13163 mod 31243 = 16341.
4. Bob will decrypt the received value by calculating _x_ = _y^d_ mod _n_ = 16341379 mod 31243 = 13. This way, Bob recovers the value that Alice sent.
![[Pasted image 20250718154343.png]]
___
### [[Diffie-Hellman Key Exchange]]
- **Key exchange** aims to establish a shared secret between two parties. It is a method that allows two parties to establish a shared secret over an insecure communication channel without requiring a pre-existing shared secret and without an observer being able to get this key. Consequently, this shared key can be used for symmetric encryption in subsequent communications.
![[Pasted image 20250718154452.png]]
- Diffie-Hellman Key Exchange is often used alongside RSA public key cryptography. Diffie-Hellman is used for key agreement, while RSA is used for digital signatures, key transport, and authentication, among many others. For instance, RSA helps prove the identity of the person you’re talking to via digital signing, as you can confirm based on their public key. This would prevent someone from attacking the connection with a man-in-the-middle attack against Alice by pretending to be Bob. In brief, Diffie-Hellman and RSA are incorporated into many security protocols and standards to provide a comprehensive security solution.
___
### [[ssh]]

#### Generate Key
`ssh-keygen -t ed25519`
- Private: `~/.ssh/id_ed25519`
- Public: `~/.ssh/id_ed25519.pub`
    
- **[[DSA]] (Digital Signature Algorithm)** is a public-key cryptography algorithm specifically designed for [[digital signatures]].
- **[[ECDSA]] (Elliptic Curve Digital Signature Algorithm)** is a variant of DSA that uses elliptic curve cryptography to provide smaller key sizes for equivalent security.
- **[[ECDSA-SK]] (ECDSA with Security Key)** is an extension of ECDSA. It incorporates hardware-based security keys for enhanced private key protection.
- **[[Ed25519]]** is a public-key signature system using EdDSA (Edwards-curve Digital Signature Algorithm) with Curve25519.
- **[[Ed25519-SK]] (Ed25519 with Security Key)** is a variant of Ed25519. Similar to ECDSA-SK, it uses a hardware-based security key for improved private key protection.
---
#### SSH Key Best Practices
- Use a **strong passphrase** (encrypts private key).
- Set proper permissions:
     `chmod 600 ~/.ssh/id_ed25519`
- Never share private key!
- Tools like **John the Ripper** can crack weak keys.
---
#### CTF / Pentest Tip
- Use `ssh-copy-id` or manually add key to `~/.ssh/authorized_keys`.
- Gain stable shell access (e.g., vs unstable reverse shell).
- Can act as a **backdoor**.
---
#### Common Commands
- **Generate key :** ssh-keygen -t ed25519  
- **Copy public key to server :** ssh-copy-id user@host  
- **Login using key :** ssh -i ~/.ssh/id_ed25519 user@host`
____
### [[Digital Signatures]] and [[Certificates]]
- Digital signatures provide a way to verify the **authenticity** and **integrity** of a digital **message** or **document**
- ![[Pasted image 20250718164612.png]]
- the certificate is signed by an **organisation**, the organisation is trusted by a **CA**, and the CA is trusted by your **browser**. Therefore, your browser trusts the certificate.
- https://letsencrypt.org/ = free certif
---
### [[PGP]] and [[GPG]]
**PGP** stands for Pretty Good Privacy. It’s software that implements encryption for encrypting **files**, performing **digital signing**, and more.[[GnuPG]] or GPG is an open-source implementation of the OpenPGP standard.
- GPG is commonly used in email to protect the confidentiality of the email messages
- **generating GPG :** gpg --full-gen-key
- you can attempt to crack it using [[John the Ripper]] and `gpg2john`
- **import your key from backup.key :** gpg --import backup.key
- **decrypt your messages :** - `gpg --decrypt confidential_message.gpg`

___
# Hashing Basics
### Hash Function
- [[Hash]] functions are different from encryption. There is no key, and it’s meant to be impossible (or computationally impractical) to go from the output back to the input
- Common encodings are [[base64]] or [[hexadecimal]]. [[md5sum]], [[sha1sum]], [[sha256sum]], and [[sha512sum]]... they are also cammands
- `md5sum file.txt` show the hash of the file
- hexdump -C file1.txt : ASCII
### Using Hashing to Store Passwords
- What if, instead of storing the password, you just stored its hash value using a secure hashing function
- **[[Rainbow Table]]** is a lookup table of hashes to plaintexts, so you can quickly find out what password a user had just from the hash
- Websites like [CrackStation](https://crackstation.net/) and [Hashes.com](https://hashes.com/en/decrypt/hash) internally use massive rainbow tables to provide fast password cracking for **hashes without salts**. Doing a lookup in a sorted list of hashes is quicker than trying to crack the hash.
- to protect against rainbow tables, we add a [[salt]] to the passwords. The salt is a randomly generated value stored in the database and should be unique to each user
- The salt is added to either the start or the end of the password before it’s hashed
____
### Recognising Password Hashes
- If you find the hash in a web application database, it’s more likely to be MD5 than [[NTLM]]
- On Linux, password hashes are stored in `/etc/shadow`
- Format : `username:$prefix$options$salt$hash:other_fields...`
- Use `man 5 shadow` and `man 5 crypt` for format and algorithm info.

| Prefix                         | Algorithm     | Notes                                      |
| ------------------------------ | ------------- | ------------------------------------------ |
| `$y$`                          | yescrypt      | Strong, default on modern systems          |
| `$gy$`                         | gost-yescrypt | Uses GOST R 34.11-2012 + yescrypt          |
| `$7$`                          | scrypt        | Good for password hashing, memory-hard     |
| `$2b$`, `$2y$`, `$2a$`, `$2x$` | bcrypt        | Based on Blowfish, very common             |
| `$6$`                          | sha512crypt   | SHA-512 based, used in older Linux distros |
| `$md5`                         | SunMD5        | Solaris-specific                           |
| `$1$`                          | md5crypt      | FreeBSD origin, weak                       |
- MS Windows passwords are hashed using [[NTLM]], a variant of MD4
- On MS Windows, password hashes are stored in the [[SAM]] (Security Accounts Manager).
___
###  Password Cracking
- You can use a graphics card (GPU) to crack many hash types quickly
- You can choose how. You’ll need to use online tools, [[Hashcat]], or [[John the Ripper]]
- hashcat -m <hash_type> -a <attack_mode> hashfile wordlist
___
### Hashing for Integrity Checking
- **[[HMAC]] (Keyed-Hash Message Authentication Code)** is a type of message authentication code (MAC) that uses a cryptographic hash function in combination with a secret key to verify the authenticity and integrity of data.
- An HMAC can be used to ensure that the person who created the HMAC is who they say they
![[Pasted image 20250718233649.png]]
___
# John the Ripper: The Basics
### John Basic Syntax
- john \[options] \[file path]
- `john --wordlist=[path to wordlist] [path to file]`
- to know the hash use : python3 [[hash-id]].py
- john --format=\[format] --wordlist=\[path to wordlist] \[path to file]
- `john --list=formats | grep -iF "md5"`. : to know all formats
___
### Cracking Windows Authentication Hashes
- NThash (NTLM) is the hash format modern Windows operating system machines use to store user and service passwords.
___
### Cracking Hashes from /etc/shadow
- to crack `/etc/shadow` passwords, you must combine it with the `/etc/passwd` file for John to understand the data it’s being given
- ``unshadow local_passwd local_shadow > unshadowed.txt`
___
### [[Single Crack Mode]]
- based on username
- `john --single --format=[format] [path to file]`
___
### Custom Rules
- Custom rules in John the Ripper define how to **dynamically modify (mangle)** passwords from a wordlist.
- Used especially in **Single Crack Mode** to match common password patterns (e.g., "Password123!").
- Defined in the `john.conf` file ( `/etc/john/john.conf` or `/opt/john/john.conf`).
- `[List.Rules:RuleName]` : Defining a Rule
- `RuleName` is the name you'll reference in the `--rules=RuleName` argument.

| Modifier  | Effect                          |
| --------- | ------------------------------- |
| `c`       | Capitalize first character      |
| `Az"..."` | Append characters from the set  |
| `A0"..."` | Prepend characters from the set |

| Example  | Meaning                |
| -------- | ---------------------- |
| `[0-9]`  | Any digit 0–9          |
| `[A-Z]`  | Uppercase letters only |
| `[a-z]`  | Lowercase letters only |
| `[!$@#]` | Custom symbols         |
| `[a]`    | Just the letter `a`    |

`[List.Rules:PoloPassword] cAz"[0-9][!£$%@]"`
- `c`: Capitalize first letter 
- `Az"[0-9][!£$%@]"`: Append a number 0–9, then one of the symbols
- Using Custom Rules :`john --wordlist=path/to/wordlist.txt --rules=RuleName path/to/hashfile`
___
### Cracking Password Protected Zip Files
- [[zip2john]] \[options] \[zip file] > \[output file] :(zip2john is like unshadow)
### Cracking Password-Protected RAR Archives
- [[rar2john]]  \[rar file] > \[output file]
### Cracking SSH Key Passwords
- using John to crack the SSH private key password of `id_rsa` files
- `id_rsa` private key is used to log in to the SSH session
- `ssh2john [id_rsa private key file] > [output file]`