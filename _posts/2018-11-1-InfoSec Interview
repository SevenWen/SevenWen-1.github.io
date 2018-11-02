---
layout: post
title: Interview Questions and answer
---

There is a [blog](https://danielmiessler.com/study/infosec_interview_questions/) mentioned some interview questions of information seciryty. I will choose some question which I am not so familiar with and answer it. 

## System Administration
###How do you change your DNS settings in Linux/Windows?
On Linux, the DNS servers that the system uses for name resolution are defined in the /etc/resolv.conf file. That file should contain at least one nameserver line. Each nameserver line defines a DNS server. 
###What are your first three steps when securing a Linux server?[check out this site](https://medium.com/viithiisys/10-steps-to-secure-linux-server-for-production-environment-a135109a57c5)
1. only install needed applications, remove those useless things. Update the system and application.
2.Turn on SELinux
Security-Enhanced Linux (SELinux) is an access control security mechanism provided in the kernel.
SELinux provides 3 basic modes of operation :
Enforcing: This is default mode which enable and enforce the SELinux security policy on the machine.
Permissive: In this mode, SELinux will not enforce the security policy on the system, only warn and log actions.
Disabled: SELinux is turned off.
It can be managed from ‘/etc/selinux/config’ file, where you can enable or disable it.
