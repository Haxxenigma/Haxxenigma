# [DNS](https://ru.wikipedia.org/wiki/DNS)

### Install DNS:

```shell
apt install bind9 bind9utils bind9-doc
```

### /etc/default/bind9:

```
OPTIONS="-u bind -4"
```

### /etc/bind/named.conf.options:

```
acl "trusted" {
    192.168.100.1;    # ns1
    192.168.100.2;    # ns2
    192.168.100.100;  # host1
};

options {
    directory "/var/cache/bind";

    recursion yes;
    allow-recursion { trusted; };
    listen-on { trusted; };
    listen-on-v6 { none; };
    allow-transfer { none; };

    forwarders {
        8.8.8.8;
        8.8.4.4;
    };
};
```

### /etc/bind/named.conf.local:

```
zone "nyc3.example.com" {
    type master;
    file "/etc/bind/zones/db.nyc3.example.com";
    allow-transfer { 192.168.100.2; };
};


zone "168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/zones/db.192.168";
    allow-transfer { 192.168.100.2; };
}
```

### /etc/bind/zones/db.nyc3.example.com:

```
$TTL    604800
@       IN      SOA     ns1.nyc3.example.com. admin.nyc3.example.com. (
                              3         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL

; NS Records
@       IN      NS      ns1.nyc3.example.com.
@       IN      NS      ns2.nyc3.example.com.

; A Records
ns1.nyc3.example.com.       IN      A       192.168.100.1
ns2.nyc3.example.com.       IN      A       192.168.100.2
host1.nyc3.example.com.     IN      A       192.168.100.100

; CNAME Records
www     IN      CNAME       nyc3.example.com.
ftp     IN      CNAME       nyc3.example.com.

; MX Records
nyc3.example.com.       IN      MX  10      mail1.nyc3.example.com.
nyc3.example.com.       IN      MX  20      mail2.nyc3.example.com.
```

### /etc/bind/zones/db.192.168:

```
$TTL    604800
@       IN      SOA     nyc3.example.com. admin.nyc3.example.com. (
                              3         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL

; NS Records
@       IN      NS      ns1.nyc3.example.com.
@       IN      NS      ns2.nyc3.example.com.

; PTR Records
1.100       IN      PTR     ns1.nyc3.example.com.
2.100       IN      PTR     ns2.nyc3.example.com.
100.100     IN      PTR     host1.nyc3.example.com.
```

### Start Bind service:

```shell
systemctl start bind9
systemctl enable bind9
```

```shell
service bind9 start
service bind9 enable
```

### Create rule in firewall:

```shell
ufw allow 53/udp
ufw reload
ufw show
```

### Config test:

```shell
sudo named-checkconf
```

<br>

## ON CLIENT SIDE

### /etc/network/interfaces:

```
dns-nameservers 192.168.100.1 192.168.100.2 8.8.8.8
dns-search nyc3.example.com
```

### Restart networking:

```shell
systemctl restart networking
```

```shell
service networking restart
```