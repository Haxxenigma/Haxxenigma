# [DHCP](https://ru.wikipedia.org/wiki/DHCP)

**Install DHCP:**

```
apt install isc-dhcp-server
```

**/etc/default/isc-dhcp-server:**

```
INTERFACESv4="eth0"
```

**/etc/dhcp/dhcpd.conf:**

```
option domain-name "example.com";
option domain-name-servers ns1.example.com, ns2.example.com;
default-lease-time 3600; 
max-lease-time 7200;
authoritative;


subnet 192.168.10.0 netmask 255.255.255.0 {
    option routers 192.168.10.1;
    option subnet-mask 255.255.255.0;
    option broadcast-address 192.168.10.255;
    option domain-search "example.com";
    option domain-name-servers 192.168.10.1;
    range 192.168.10.10 192.168.10.100;
    range 192.168.10.110 192.168.10.200;


    # For static IP-addresses:


    host SERVER {
        hardware ethernet 00:f0:m4:6y:89:0g;
        fixed-address 192.168.10.105;
    }
}
```

**Start DHCP service:**

```
systemctl start isc-dhcp-server.service
systemctl enable isc-dhcp-server.service

# OR

service isc-dhcp-server.service start
service isc-dhcp-server.service enable
```

**Create rule in firewall:**

```
ufw allow 67/udp
ufw reload
ufw show
```

<br>

***ON CLIENT SIDE***

**/etc/network/interfaces:**

```
auto eth0
iface eth0 inet dhcp
```

**Restart networking:**

```
systemctl restart networking

# OR

service networking restart
```

<br>
<hr>
<br>

> Client --DHCPDISCOVER--> Server
> 
> Client <--DHCPOFFER-- Server
> 
> Client --DHCPREQUEST--> Server
> 
> Client <--DHCPACK-- Server