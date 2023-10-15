# [Nmap](https://www.kali.org/tools/nmap/)

```shell
nmap [SCAN TYPE] [OPTIONS] {TARGET SPECIFICATION}
```

## TARGET SPECIFICATION:

Hostnames, IP addresses, networks, etc.

scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254

`-iL <inputfilename>`: Input from list of hosts/networks

<br>

`-sn`: Ping scan - disable port scan

`-Pn`: Port scan - disable ping scan

<br>

`-sS`/`-sT`/`-sA`/`-sW`/`-sM`: TCP SYN/Connect()/ACK/Window/Maimon Scans

`-sU`: UDP Scan

`-sN`/`-sF`/`-sX`: TCP Null, FIN, and Xmas Scans

<br>

`-O`: Enable OS detection

`-sV`: Determine service/version info

`-T<0-5>`: Set timing template (higher is faster)

`-A`: Enable OS detection, version detection, script scanning, and traceroute

<br>

`-oN`/`-oX`/`-oS`/`-oG <file>`: Output scan in Normal, XML, SkrIpt KIddi3, and Grepable format

`-oA <basename>`: Output in the three major formats at once

<br>

`-v`: Increase verbosity level (use -vv or more for greater effect)

`-d`: Increase debugging level (use -dd or more for greater effect)

## [Nmap Scripting Engine:](https://nmap.org/nsedoc/)

`-sC`: equivalent to `--script=default`

`--script=<Lua scripts>`: \<Lua scripts\> is a comma separated list of directories, script-files or script-categories

`--script-args=<n1=v1,[n2=v2,...]>`: provide arguments to scripts

`--script-args-file=<filename>`: provide NSE script args in a file

`--script-updatedb`: Update the script database.

`--script-help=<Lua scripts>`: Show help about scripts

## [Firewall/IDS Evasion and Spoofing:](https://nmap.org/book/man-bypass-firewalls-ids.html)

`-f`; `--mtu <val>`: fragment packets

`--scan-delay`/`--max-scan-delay <time>`: Adjust delay between probes

`--badsum`: Send packets with a bogus TCP/UDP/SCTP checksum

`--data-length <num>`: Append random data to sent packets

`-S <IP_Address>`: Spoof source address

`-e <iface>`: Use specified interface

`-g/--source-port <portnum>`: Use given port number


# [Nmap Live Host Discovery](https://tryhackme.com/room/nmap01)

## Enumerating Targets:

- list: `10.10.10.10 example.com`

- range: `10.10.10.15-20`

- subnet: `10.10.10.0/24`

- file: `-iL list_of_hosts.txt`

- If you want to check the list of hosts that Nmap will scan, you can use `nmap -sL TARGETS` (use  `-n` to disable DNS resolution)

## Host Discovery Using ARP:

- Nmap:

    ```shell
    nmap -PR -sn <TARGETS>
    ```

- ARP Scan:

    ```shell
    arp-scan -l
    ```

## Host Discovery Using ICMP: ([ICMP types](https://www.iana.org/assignments/icmp-parameters/icmp-parameters.xhtml))

- ICMP Echo:

    ```shell
    nmap -PE -sn <TARGETS>
    ```

- ICMP Timestamp:

    ```shell
    nmap -PP -sn <TARGETS>
    ```

- ICMP Address Mask:

    ```shell
    nmap -PM -sn <TARGETS>
    ```

## Host Discovery Using TCP and UDP

- TCP SYN:

    ```shell
    nmap -PS -sn <TARGETS>
    ```

- TCP ACK:

    ```shell
    nmap -PA -sn <TARGETS>
    ```

- UDP:

    ```shell
    nmap -PU -sn <TARGETS>
    ```

- masscan:

    ```shell
    masscan <TARGETS> -p<PORTS>
    ```

## Reverse-DNS Lookup:

- Never do DNS resolution:

    ```shell
    -n
    ```
    
- Always resolve:

    ```shell
    -R
    ```
    
- Specify custom DNS servers:

    ```shell
    --dns-servers <serv1[,serv2],...>
    ```

# Other

## TCP(`-sT`):

- Open:

    [SYN]->

    <-[SYN, ACK]

    [ACK]->

- Closed:

    [SYN]->

    <-[RST]

- Filtered:

    [SYN]->

    <-[NONE]

## SYN(`-sS`):

- Open:

    [SYN]->

    <-[SYN, ACK]

    [RST]->

- Closed:

    [SYN]->

    <-[RST]

- Filtered:

    [SYN]->

    <-[NONE]

## UDP(`-sU`):

- Open | Filtered:

    [PACKET]->

    <-[NONE]

- Closed:

    [PACKET]->

    <-[ICMP (port is unreachable)]

## NULL(`-sN`):

- Open | Filtered:

    [NONE]->

    <-[NONE]

- Closed:

    [NONE]->

    <-[RST]

## FIN(`-sF`):

- Open | Filtered:

    [FIN]->

    <-[NONE]

- Closed:

    [FIN]->

    <-[RST]

## Xmas(`-sX`):

- Open | Filtered:

    [FIN, PSH, URG]->

    <-[NONE]

- Closed:

    [FIN, PSH, URG]->

    <-[RST]