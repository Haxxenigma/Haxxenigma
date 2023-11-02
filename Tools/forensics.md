# Digital Forensics

> memory dump like `.raw` or image file like `.e01`

[Volatility](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference) — memory extraction utility framework for memory forensic

[Redline](https://fareedfauzi.gitbook.io/windows-forensics-playbook/memory-forensics-analysis/redline-automate-memory-collector-and-analyzer) — alternative to volatility

[Bulk-extractor](https://www.kali.org/tools/bulk-extractor/) — can extracts features such as email addresses, credit card numbers, URLs, and other types of information from digital evidence files

[FTK Imager](https://yandex.kz/search/?text=FTK+Imager) — data preview and imaging tool that allows you to examine files and folders on local hard drives, network drives, CDs/DVDs, and review the content of forensic images or memory dumps

[Autopsy](https://www.autopsy.com/), [ProDiscover](https://prodiscover.com/), [EnCase](https://www.opentext.com/products/encase-forensic) — as FTK Imager

[e2fsck](https://manpages.ubuntu.com/manpages/impish/man8/e2fsck.8.html) — fix corrupt filesystem (ext2-4)

[Recuva](https://www.ccleaner.com/ru-ru/recuva), [R-Studio](https://www.r-studio.com/) — recover files

[RegRipper](https://www.kali.org/tools/regripper/) — for registry analysis

## Tools for scanning event log

- DeepblueCLI

- Chainsaw

- WELA

- HayaBusa

- APTHunter

# PCAP analysis

## Tools

- Wireshark

- NetworkMiner

- Strings

- Tshark

## Checklist

- Understand the packets

- Export objects

- Protocol hierarchy give you general understanding

- Follow TCP streams

- Filtering

- Search for keyword such as "flag" using Find Packet

- Take a look at Info column. Stupid challenge always put the flag letter by letter in different packets.

- If challenge about wifi, USB or keyboard thingy, google the past writeup how they solve.

## Others

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