# Scanning & Enumeration
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

### nikto
Nikto can be detected by good security and can be blocked
```
nikto -h 192.168.4.4
```

### MSF (scanner/smb/smb_version)
Give SMB version

### smbclient
Try to connect
```
smbclient -L \\\\192.168.4.4\\
smbclient \\\\192.168.4.4\\ADMIN$
```
