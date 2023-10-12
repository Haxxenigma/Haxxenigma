# Binary Exploit / Pwn

`checksec` — check the properties of executable of binary security

- **Stack Canaries** = a secret value placed on the stack which changes every time the program is started. the stack canary is checked and if it appears to be modified, the program exits immeadiately.

- **Nx** = stored input or data cannot be executed as code

- **Address Space Layout Randomization (ASLR)** = The randomization of the place in memory where the program, shared libraries, the stack, and the heap are.

- **RELRO** = makes binary sections read-only.

**Tools**

- Pwntool framework

- Gdb debugger. Peda, pwndbg or gef.

- Use `readelf -a <filename>`  command. It will displays information about ELF files.

- Use `nm <filename>`  command to know what symbol being called in the binary.

- Python

**Function that can lead to bof**

- scanf

- read

- strcat

- fread

- fgets

- sprintf

- strcpy

- gets

- memcpy

- memmove

- strncpy

- snprintf

- strncat