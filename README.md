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
Connect to it. Type,
```bash
ftp <ip>
```

Now, let's view files using ls command.
There are two files named as locks.txt and task.txt.
Get them to your pc and see whats inside.
First one has a username and other has list of words which is a password list for bruteforcing.

# Gaining access:-

Since we have username and password list, let's do a bruteforcing attack using Hydra.
Hydra is a tool we are going to use to do bruteforcing.

Type:-
```bash
hydra -l <username> -P <password_list> -t 1 <ip>
```
