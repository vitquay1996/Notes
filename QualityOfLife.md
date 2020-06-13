## tty shell from fake shell
```
python -c 'import pty; pty.spawn("/bin/bash")'
```

## Test code execution 
```
ping 10.10.10.10
tcpdump -i tun0 icmp 
```
