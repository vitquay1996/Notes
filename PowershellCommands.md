### Read file
```
Get-Content "C:\Users\"
```

### Base64 encode
```
$fc = Get-Content "C:\Users\"
$fe = [System.Text.Encoding]::UTF8.GetBytes($fc)
[System.Convert]::ToBase64String($fe)
```
```
certutil -encode C:\sam C:\sam.b64
```
