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
http
```
nmap -sT -Pn -sV -p 80 "--script=banner,(http* or ssl*) and not (brute or broadcast or dos or external or http-slowloris* or fuzzer)" 10.1.1.27
```

### nmap alternatives
- msf scanner/portscan/syn
- masscan

## Web

### nikto
Nikto to scan web server. Nikto can be detected by good security and can be blocked
```
nikto -h 192.168.4.4
```

## SMB

### MSF (scanner/smb/smb_version)
Give SMB version

### smbclient
Try to connect
```
smbclient -L \\\\192.168.4.4\\
smbclient \\\\192.168.4.4\\ADMIN$
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
