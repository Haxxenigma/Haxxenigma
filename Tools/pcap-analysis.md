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