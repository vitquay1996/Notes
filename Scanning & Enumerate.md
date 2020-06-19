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

## DNS
Reverse DNS lookup
```
dig -x 8.8.8.8
```

Zone tranfer
```
dig axfr cronos.htb @10.10.10.13
```
