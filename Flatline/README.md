## Enumeration
### nmap
```bash
# Nmap 7.92 scan initiated Sun Feb 27 09:11:58 2022 as: nmap -T4 -p3389,8021 -A -oA nmap/Flatline -Pn 10.10.213.98
Nmap scan report for 10.10.213.98
Host is up (0.16s latency).

PORT     STATE SERVICE          VERSION
3389/tcp open  ms-wbt-server    Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: WIN-EOM4PK0578N
|   NetBIOS_Domain_Name: WIN-EOM4PK0578N
|   NetBIOS_Computer_Name: WIN-EOM4PK0578N
|   DNS_Domain_Name: WIN-EOM4PK0578N
|   DNS_Computer_Name: WIN-EOM4PK0578N
|   Product_Version: 10.0.17763
|_  System_Time: 2022-02-27T14:12:18+00:00
| ssl-cert: Subject: commonName=WIN-EOM4PK0578N
| Not valid before: 2021-11-08T16:47:35
|_Not valid after:  2022-05-10T16:47:35
|_ssl-date: 2022-02-27T14:12:19+00:00; 0s from scanner time.
8021/tcp open  freeswitch-event FreeSWITCH mod_event_socket
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: specialized
Running (JUST GUESSING): AVtech embedded (87%)
Aggressive OS guesses: AVtech Room Alert 26W environmental monitor (87%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 5 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

TRACEROUTE (using port 8021/tcp)
HOP RTT       ADDRESS
1   8.24 ms   10.17.0.1
2   ... 4
5   169.37 ms 10.10.213.98

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Feb 27 09:12:19 2022 -- 1 IP address (1 host up) scanned in 21.65 seconds
```

Okay, so port 8021 is running freeswitch which has 2 exploits available on exploitdb. 
![[Pasted image 20220227214757.png]]

## Exploitation
Metasploit one is tricky, I only got shell one time after several attempts so tried the python one and it worked got rce.
![[Pasted image 20220227210145.png]]

Now, let's get reverse shell. I'll use encoded powershell payload.
![[Pasted image 20220227210227.png]]

### PrivEsc
**winpeas** revealed a lot of things.
![[Pasted image 20220227210310.png]]
Vulnerable to couple of exploits.... Interesting...

![[Pasted image 20220227210352.png]]
No AV is on machine... Great!

![[Pasted image 20220227214041.png]]
Ooh, look... SeImpersonatePrivilege... My bad, should have done `whoami /priv` before running winpeas.

So, juicypotato, printspoofer exploits should work. I'll use printspoofer.
![[Pasted image 20220227214407.png]]
![[Pasted image 20220227214418.png]]

