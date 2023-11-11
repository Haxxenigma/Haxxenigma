# Digital Forensics

> memory dump like `.raw` or image file like `.e01`

[Volatility](https://github.com/volatilityfoundation/volatility) — memory extraction utility framework to analyze volatile memory

[Redline](https://fareedfauzi.gitbook.io/windows-forensics-playbook/memory-forensics-analysis/redline-automate-memory-collector-and-analyzer) — memory forensics tool to analyze volatile and non-volatile memory

[Bulk-extractor](https://www.kali.org/tools/bulk-extractor/) — can extract features such as email addresses, credit card numbers, URLs, and other types of information from digital evidence files

[FTK Imager](https://yandex.kz/search/?text=FTK+Imager), [Autopsy](https://www.autopsy.com/), [ProDiscover](https://prodiscover.com/), [EnCase](https://www.opentext.com/products/encase-forensic) — can analyze a variety of digital media, including hard drives, USB drives, and memory cards

[e2fsck](https://manpages.ubuntu.com/manpages/impish/man8/e2fsck.8.html) — repair and check corrupt filesystem (ext2-4)

[Recuva](https://www.ccleaner.com/ru-ru/recuva), [R-Studio](https://www.r-studio.com/) — data recovery tools

[RegRipper](https://www.kali.org/tools/regripper/) — for registry analysis

# PCAP analysis

## Tools

- Wireshark

- NetworkMiner

- Strings

- Tshark

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