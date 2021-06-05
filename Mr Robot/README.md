# Writeup for Mr Robot room on TryHackMe.
URL = https://tryhackme.com/mrrobot
Based on the Mr. Robot show, can you root this box?

Enumeration: -
Lets run quick nmap scan.
```bash
sudo nmap -A <ip>
```
This returned 2 open ports.
port      |service
----------|----------
22        |SSH
80        |Web server
443       |Web server (HTTPS)

Let's enumerate port 80.
Hmm... Interesting page. Let's check /robots.txt
