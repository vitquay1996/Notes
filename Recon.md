# User, email format, breach credentials
## General
### the Harvester
General but not so effective
```
theHarvester -d tesla.com -l 500 -b google
```
## Find emails
### hunter.io

## Find subdomain
### Sublist3r
```
sublist3r -d tesla.com
```
### crt.sh

### OWASP amass

### httprobe

## Find technology
### builtwith.com
Most informative

### Wappalyzer.com
Right on browser

### whatweb
Terminal tool

### Google Fu

## Scanning & Enumeration
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

### nikto
Nikto can be detected by good security and can be blocked
```
nikto -h 192.168.4.4
```
