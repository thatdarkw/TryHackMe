# Room name = Bounty Hacker.
# URL = https://tryhackme.com/room/cowboyhacker

tryhackme Bounty Hunter walkthrough:- Room is easy and straight forward.

# Enumeration:-

Lets run quick nmap scan.
```bash
sudo nmap <ip>
```
This returned 3 open ports.
port      |service
----------|----------
21        |FTP
22        |SSH
80        |Web server

Let's enumerate ftp port first.
Connect to it like ```bash
ftp <ip>
```
