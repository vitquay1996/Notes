### Email based
Use whois to find admin email. Use admin email to find other domains that are registered by the same admin
```
https://viewdns.info/reversewhois/
```

### Backlink
Use app.neilpatel.com

### AXFR
```
fierce -dns nic.cbre -search cbre
```

### SANs record
```
echo | openssl s_client -connect facilitysource.com:443 | openssl x509 -noout -text | grep DNS:
```

### Google Dork
```
inurl: cbre
```
