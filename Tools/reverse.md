# Reverse Engineering

### PE File (.exe or .dll)

- Use **DIE**, **PEID**, **PEBear**, or **PEView** software to do static file analysis. Find details of file in there!

- Use **HxD** to check the header file, file signature. Maybe the corrupt file sign one.

- Find it whether it packed or not. Find online unpack.

- Find it whether the binary has anti-debug or not.

- Use **IDA Pro** software to perform static analysis on the binary.

- When do analysis static or dynamic focus on `strcmp`, function `call`, `conditional jump`.

- You can use **Snowman** or **Ghidra** software  to perform decompiler.

- Use debugger like **Immunity Debugger**, **x64Dbg/x32Dbg**, or **WinDbg** to debug the binary.  

- API monitor

- Frida-trace

### ELF File (.elf)

- Use `ltrace <filename>` command to know what library function are being called in the binary.

- Use `strace <filename>` command to know what system and signal function are being called in the binary.

- Use `nm <filename>` command to know what symbol being called in the binary.

- Use `readelf -a <filename>`  command. It will displays information about ELF files.

- Use Gdb debugger extension. `Peda`, `pwndbg` or `gef` will help you!.

- Or you can use edb debugger.

- Use **IDA Pro** software to perform static analysis on the binary.

### APK File (.apk)

- Use `APKTool <filename>` command tools.

- Use Android Emulator to run the program.

- Use Android Debug Bridge.

- Use `dex2jar <filename>` command tools.

- Use **jd-gui**. 

- **JADX** is good alternative to jd-gui.

- Rename the file to zip file. Unzip it. Take a look the file in your favorite text editor.

### .NET File (.exe)

- Use **dnSpy** software. Very powerful. You can compile the program by

  - Edit in the main interface -> compile -> save all. Try run the program back!

### Java file

- Use **JADX**

### Python file

- There are many options, one of it is **uncompyle6**. Just google dor python decompiler.

- <https://github.com/extremecoders-re/pyinstxtractor> - Python EXE to pyc

### Shellcode

- scdbg

- shellcode2exe

- pdfstreamdumper shellcode analysis

- debugger

- IDA Pro

- unicode2hex-escaped

- hxd

### Others

- <https://www.decompiler.com/>

    - EXE or DLL (C#), JAR or CLASS, APK, XAPK or DEX, PYC or PYO, LUAC or LUB, SMX or AMXX

> Renaming functions and variables, deobfuscation and doing a good work is not something that matters during a CTF; we only need the flag. Thus, why reverse engineer when you don’t have too? The less we reverse, the better it is.