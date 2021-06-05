# Writeup for Wonderland room on TryHackMe.
URL = https://tryhackme.com/room/wonderland

Fall down the rabbit hole and enter wonderland.

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

Let's enumerate port 80.
Nothing much on home page except some picture and words. Picture is from /img so let's check it and download them to check for steganography.
Using steghide on white_rabbit_1.jpg with no pass extracts hint.txt file which says follow the r a b b i t. Interesting....

Let's directory burst cause no idea what this hint means.

```
dirsearch -u http://10.10.163.161/ -e php,txt,html -x 400,401,403 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```
This returns 3 interesting directories which are /r/ , /poem/, and /img/. Already checked /img/ so let's check this two.
/poem contains a nice poes. Give it a read!
/r contains some message.
I used -r so its gonna directory burst every directory it find with all dictionary words but I'm gonna stop it after 10% done cause that's enough.
No interesting directory after /poem/ but on /r/ we found another directory which is /r/a/. It contains some conversation type message. Again after some time I stop the scan and tell dirsearch to start on /r/a/.
Now, dirsearch founds /r/a/b/... Interesting huh? Remember the hint. You can do like this or you already know from the hint now. I dirsearch all the way till end after then I notices r a b b i t hint actually suggests to go to the /r/a/b/b/i/t/ directory.
