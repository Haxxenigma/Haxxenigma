# [Linux Privilege Escalation](https://github.com/Haxxenigma/TryHackMe/blob/main/Linux-Privilege-Escalation.md "https://github.com/Haxxenigma/TryHackMe/blob/main/Linux-Privilege-Escalation.md")

[GTFOBins](https://gtfobins.github.io/ "https://gtfobins.github.io/")

[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings "https://github.com/swisskyrepo/PayloadsAllTheThings")

- [Reverse Shell Cheatsheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md "https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md")

[ExploitDB](https://www.exploit-db.com/ "https://www.exploit-db.com/")

- [Searchsploit - ExploitDB in CLI](https://www.kali.org/tools/exploitdb/ "https://www.kali.org/tools/exploitdb/")

- [MySQL - User-Defined Function (UDF)](https://www.exploit-db.com/exploits/1518 "https://www.exploit-db.com/exploits/1518
MySQL 4.x/5.0 (Linux) - User-Defined Function (UDF) Dynamic Library (2)")

[Linux Kernerl CVEs](https://www.linuxkernelcves.com/cves "https://www.linuxkernelcves.com/cves")

<br>

[LinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS "https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS")

[LinEnum](https://github.com/rebootuser/LinEnum "https://github.com/rebootuser/LinEnum")

[Linux Smart Enumeration](https://github.com/diego-treitos/linux-smart-enumeration "https://github.com/diego-treitos/linux-smart-enumeration")

[Linux Priv Checker](https://github.com/linted/linuxprivchecker "https://github.com/linted/linuxprivchecker")

[Linux Exploit Suggester](https://github.com/The-Z-Labs/linux-exploit-suggester "https://github.com/The-Z-Labs/linux-exploit-suggester")

[Linux Exploit Suggester 2 & Dirty Cow](https://github.com/Haxxenigma/TryHackMe/tree/main/Linux-PrivEsc-Scripts/kernel-exploits "https://github.com/Haxxenigma/TryHackMe/tree/main/Linux-PrivEsc-Scripts/kernel-exploits")

<br>

[Linux Privilege Escalation Cheatsheet](https://github.com/Haxxenigma/TryHackMe/blob/main/Linux-Privilege-Escalation.md "https://github.com/Haxxenigma/TryHackMe/blob/main/Linux-Privilege-Escalation.md")

[Metasploit Cheatsheet](https://github.com/Haxxenigma/TryHackMe/blob/main/Metasploit.md "https://github.com/Haxxenigma/TryHackMe/blob/main/Metasploit.md")

[Nmap Cheatsheet](https://github.com/Haxxenigma/TryHackMe/blob/main/Nmap.md "https://github.com/Haxxenigma/TryHackMe/blob/main/Nmap.md")

[Nmap Live Host Discovery Cheatsheet](https://github.com/Haxxenigma/TryHackMe/blob/main/Nmap-Live-Host-Discovery.md "https://github.com/Haxxenigma/TryHackMe/blob/main/Nmap-Live-Host-Discovery.md")

[SQL Injection Cheatsheet](https://github.com/Haxxenigma/TryHackMe/blob/main/SQL-Injection.md "https://github.com/Haxxenigma/TryHackMe/blob/main/SQL-Injection.md")

[OWASP Top-10 Cheatsheet](https://github.com/Haxxenigma/TryHackMe/blob/main/OWASP-Top-10.md "https://github.com/Haxxenigma/TryHackMe/blob/main/OWASP-Top-10.md")

[Google Dorking Cheatsheet](https://github.com/Haxxenigma/TryHackMe/blob/main/Google-Dorking.md "https://github.com/Haxxenigma/TryHackMe/blob/main/Google-Dorking.md")

# OSINT

[awesome-osint](https://github.com/jivoi/awesome-osint "https://github.com/jivoi/awesome-osint")

[Maryam](https://github.com/saeeddhqan/Maryam "https://github.com/saeeddhqan/Maryam")

[OSINT-SAN](https://github.com/Bafomet666/OSINT-SAN "https://github.com/Bafomet666/OSINT-SAN")

# Passwords

[Create password](https://www.kali.org/tools/whois/ "https://www.kali.org/tools/whois/")

```
mkpasswd -m sha-512 <PASSWORD>
```

```
openssl passwd -1 -salt <SALT> <PASSWORD>
```

[John the Ripper](https://www.kali.org/tools/john/ "https://www.kali.org/tools/john/")

```
sudo apt install john
```

```
cp /etc/passwd passwd.txt && cp /etc/shadow shadow.txt

unshadow passwd.txt shadow.txt > hash_to_crack.txt

john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

[Hydra](https://www.kali.org/tools/hydra/ "https://www.kali.org/tools/hydra/") | [(Cheatsheet)](https://github.com/Haxxenigma/TryHackMe/blob/main/Hydra.md "https://github.com/Haxxenigma/TryHackMe/blob/main/Hydra.md")

```
sudo apt install hydra
```

```
hydra -l root -P /usr/share/wordlists/metasploit/unix_passwords.txt -t 6 ssh://192.168.1.123
```

# Wordlists

[Wordlists](https://www.kali.org/tools/wordlists/ "https://www.kali.org/tools/wordlists/")

```
sudo apt install wordlists

gunzip /usr/share/wordlists/rockyou.txt.gz
```

[SecLists](https://www.kali.org/tools/seclists/ "https://www.kali.org/tools/seclists/")

```
sudo apt install seclists
```

# Scan for directories in website

[ffuf](https://www.kali.org/tools/ffuf/ "https://www.kali.org/tools/ffuf/")

```
ffuf -w <wordlist> -u <url>/FUZZ
```

[dirb](https://www.kali.org/tools/dirb/ "https://www.kali.org/tools/dirb/")

```
dirb <url> <wordlist>
```

[gobuster](https://www.kali.org/tools/gobuster/ "https://www.kali.org/tools/gobuster/")

```
gobuster -u <url> -w <wordlist> dir
```

# File metadata reader

[pdfinfo](https://poppler.freedesktop.org/ "https://poppler.freedesktop.org/")

```
sudo apt install poppler-utils
```

[exiftool](https://www.kali.org/tools/libimage-exiftool-perl/ "https://www.kali.org/tools/libimage-exiftool-perl/")

```
sudo apt install libimage-exiftool-perl
```

# General

[wget](https://www.kali.org/tools/wget/)

```
wget [options] <url>
```

[curl](https://www.kali.org/tools/curl/)

```
curl [options] <url>
```

[openssh](https://www.kali.org/tools/openssh/)

```
scp /src/path/ user@host:/dest/path/
```

```
scp user@host:/dest/path/ /src/path/
```

[python](https://www.python.org/downloads/?ref=)

```
python3 [options] [-c cmd | -m mod | file | -]
```

```
python3 -m http.server [port]
```

# Crontab

[Crontab Generator](https://crontab-generator.org/ "https://crontab-generator.org/")

[Crontab Guru](https://crontab.guru/ "https://crontab.guru/")

```
crontab -e
```