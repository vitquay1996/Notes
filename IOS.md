# Frida guide
## Cannot hook to swift
- Identify process and trace function
```
frida-ps -U
frida-trace -U -i "*jail*" DVIA-v2
```
- Find the function location in Ghidra and hook
```
var targetModule = 'DVIA-v2';
var addr = ptr(0x1959d8);
var moduleBase = Module.getBaseAddress(targetModule);
console.log(moduleBase)
var targetAddress = moduleBase.add(addr);
   Interceptor.attach(targetAddress, {
        onEnter: function(args) {
            this.context.x8 = 0x0
        },
    });
```

# Local Data Storage
## UserDefaults
```
cat /var/mobile/Containers/Data/Application/E825E63E-0E34-4EC1-9A96-186FD2598564/Library/Preferences/com.highaltitudehacks.DVIAswiftv2.plist
```
## plist
```
cat /var/mobile/Containers/Data/Application/E825E63E-0E34-4EC1-9A96-186FD2598564/Documents/userInfo.plist
```

# Side Channel Data Leakage
## Pasteboard
- Use Frida script
## Keystroke logging
```
cat /var/mobile/Library/Keyboard/en-dynamic.lm/dynamic-lexicon.dat
```
## Cookies
```
Use Grapefruit
```
