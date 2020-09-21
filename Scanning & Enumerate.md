# Scanning & Enumeration
## Identify
### arp-scan
Broadcast ARP packages to identify hosts
```
arp-scan 192.168.4.0/24
```
### nmap
Basic scan all
```
nmap -T4 -p- -A 192.168.4.4
```

### nmap alternatives
- msf scanner/portscan/syn
- masscan
```
masscan 10.11.0.0 -p0-65535 ––rate 1000000
```

## 21 - FTP
How to use passive
```
USER asdf
PASS asdf
PASV
RETR /path/to/file
nc 10.11.1.111 12 > file.txt
```
Download all
```
wget --mirror 'ftp://user:password@server'
```
## 25,465,587 - SMTP
Get banner and users
```
nc -vn 10.11.1.111 25
HELO x
MAIL FROM:test@test.com
RCPT TO:admin
VRFY root
EXPN root
```

## 110,995 - POP3
Get banner and mail
```
nc -nv 10.11.1.111 110
USER
PASS
LIST
RETR n
```

## 80,443 - Web
```
nmap -vv --reason -Pn -sV -p 80 "--script=banner,(http* or ssl*) and not (brute or broadcast or dos or external or http-slowloris* or fuzzer)" 10.11.1.111
gobuster dir -u http://10.11.1.35 -x php -t 100 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
nikto -h 192.168.4.4
```
Try robots.txt
Read source, including javascript
```
droopescan scan drupal -u http://example.org/ -t 32
```

## 139,445 - SMB

### Obtain information
```
enum4linux -a [-u "<username>" -p "<passwd>"] 10.11.1.111
nmap --script "safe or smb-enum-*" -p 445 10.11.1.111
nmap --script vuln -p 445 10.11.1.111
rpcclient -U "" -N 10.11.1.1.11
rpcclient -U "username" [--pw-nt-hash] 10.11.111 #ask for hash
```

### smbclient
Try to connect
```
smbclient -L \\\\192.168.4.4\\
smbclient \\\\192.168.4.4\\ADMIN$
smbclient -U 'username[%passwd]' -L [--pw-nt-hash] //<IP>
```

### smbmap
```
smbmap -H 10.10.10.100
smbmap -R folder -H 10.10.10.100
smbmap -R folder -H 10.10.10.100 -A Groups.xml -q
smbmap -d domain -u user -p password -H 10.10.10.100
```

### GetADUsers.py
```
GetADUsers.py -all -user username -dc-ip 10.10.10.100
```

### LDAP
```
nmap -n -sV --script "ldap* and not brute" <IP>
ldapsearch -x -h 10.10.10.119 -s base namingcontexts
ldapsearch -x -h 10.10.10.119 -b 'dc=lightweight,dc=htb'
```

## DNS
Reverse DNS lookup
```
dig -x 8.8.8.8
```

Zone tranfer
```
dig axfr cronos.htb @10.10.10.13
host -l megarop.com ns1.megarop.com
dnsrecon -d megarop.com -t axfr
dnsenum megarop.com
dnsenum –f <file> -r <url> --dnsserver 10.10.10.10
```

## 2049 - NFS
```
sudo showmount -e 10.11.1.111
mount -t nfs [-o vers=2] <ip>:<remote_folder> <local_folder> -o nolock
```
https://www.pentestpartners.com/security-blog/using-nfsshell-to-compromise-older-environments/
