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

![]({{site.baseurl}}/https://cheapsslsecurity.com/blog/wp-content/uploads/2017/10/ssl-tls-handshake-process-1024x670.png)

