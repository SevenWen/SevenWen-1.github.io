---
layout: post
title: Interview Questions and answer
published: true
---

There is a [blog](https://danielmiessler.com/study/infosec_interview_questions/) mentioned some interview questions of information seciryty. I will choose some question which I am not so familiar with and answer it. 

## System Administration
### How do you change your DNS settings in Linux/Windows?
On Linux, the DNS servers that the system uses for name resolution are defined in the /etc/resolv.conf file. That file should contain at least one nameserver line. Each nameserver line defines a DNS server. 
### What are your first three steps when securing a Linux server?[check out this site](https://medium.com/viithiisys/10-steps-to-secure-linux-server-for-production-environment-a135109a57c5)
1. only install needed applications, remove those useless things. Update the system and application.
2.Turn on SELinux
Security-Enhanced Linux (SELinux) is an access control security mechanism provided in the kernel.
SELinux provides 3 basic modes of operation :
Enforcing: This is default mode which enable and enforce the SELinux security policy on the machine.
Permissive: In this mode, SELinux will not enforce the security policy on the system, only warn and log actions.
Disabled: SELinux is turned off.
It can be managed from ‘/etc/selinux/config’ file, where you can enable or disable it.
3. use strong passwords, close useless ports
4. and so on...

## Encryption
### TLS Handshake
- The client sends a "Client hello" message to the server, along with the client's random value and supported cipher suites.
- The server responds by sending a "Server hello" message to the client, along with the server's random value.
- The server sends its certificate to the client for authentication and may request a certificate from the client. The server sends the "Server hello done" message.
- If the server has requested a certificate from the client, the client sends it.
- The client creates a random Pre-Master Secret and encrypts it with the public key from the server's certificate, sending the encrypted Pre-Master Secret to the server.
- The server receives the Pre-Master Secret. The server and client each generate the Master Secret and session keys based on the Pre-Master Secret.
- The client sends "Change cipher spec" notification to server to indicate that the client will start using the new session keys for hashing and encrypting messages. Client also sends "Client finished" message.
- Server receives "Change cipher spec" and switches its record layer security state to symmetric encryption using the session keys. Server sends "Server finished" message to the client.
- Client and server can now exchange application data over the secured channel they have established. All messages sent from client to server and from server to client are encrypted using session key.

![](https://cheapsslsecurity.com/blog/wp-content/uploads/2017/10/ssl-tls-handshake-process-1024x670.png)

### If someone steals the server’s private key can they decrypt all previous content sent to that server?

Because attacker got the private key of server and he can see call the previous traffic, the attacker can decrypt the master secret and got the key for symmetric encryption. Then attacker can decrypt the traffic. 

### what should the server do if its private key is lost

one should add the SSL Certificate to the Certificate Revocation List (CRL). This will alert other participants in the Public Key Infrastructure (PKI) that the certificate in question can no longer be trusted. In order to do this, you will usually need to login to the account you created with the Certificate Authority (CA) who issued the SSL Certificate or otherwise notify them of the suspected breach.

### What are some common ways that TLS is attacked,and/or what are some ways it’s been attacked in the past?
-For [64-bit block CBC mode](https://blog.cryptographyengineering.com/2016/08/24/attack-of-week-64-bit-ciphers-in-tls/), if server used one key to encrypt too many data, attacker may find a cllision of ciphertext, that (p1 xor IV1) = (p2 xor IV2). And IVs are known to attacker, so attacker can know p1 xor p2.
- [downgrade attack](https://p16.praetorian.com/blog/man-in-the-middle-tls-ssl-protocol-downgrade-attack)
- [Heartbleed](https://blog.cryptographyengineering.com/2014/04/08/attack-of-the-week-openssl-heartbleed/) The problem is fairly simple: there’s a tiny vulnerability — a simple missing bounds check — in the code that handles TLS ‘heartbeat’ messages. By abusing this mechanism, an attacker can request that a running TLS server hand over a relatively large slice (up to 64KB) of its private memory space. Since this is the same memory space where OpenSSL also stores the server’s private key material, an attacker can potentially obtain (a) long-term server private keys, (b) TLS session keys, (c) confidential data like passwords, (d) session ticket keys.
- BEAST

### What is Forward Secrecy?
In cryptography, forward secrecy (FS), also known as perfect forward secrecy (PFS), is a feature of specific key agreement protocols that gives assurances your session keys will not be compromised even if the private key of the server is compromised. Forward secrecy protects past sessions against future compromises of secret keys or passwords. By generating a unique session key for every session a user initiates, even the compromise of a single session key will not affect any data other than that exchanged in the specific session protected by that particular key. 

### What’s more secure, SSL, TLS, or HTTPS?
TLS is an updated version of SSL. HTTPS appears in the URL when a website is secured by an SSL certificate.

## Network Security
### What port does ping work over?
