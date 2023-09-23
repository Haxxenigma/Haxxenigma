# [Zabbix](https://www.zabbix.com/download "https://www.zabbix.com/download")

### Install Zabbix repository:

```shell
wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb

dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb

apt update
```

### Install Zabbix server, frontend, agent:

```shell
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

### Create initial database:

```shell
apt install apache2 mysql-server mysql-client
```

```shell
mysql -uroot -p
```

```sql
create database zabbix character set utf8mb4 collate utf8mb4_bin;
create user zabbix@localhost identified by 'zbxPa55Word';
grant all privileges on zabbix.* to zabbix@localhost;
flush privileges;
set global log_bin_trust_function_creators = 1;
quit;
```

### On Zabbix server host import initial schema and data:

```shell
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```

### Disable log_bin_trust_function_creators option after importing database schema:

```shell
mysql -uroot -p
```

```sql
set global log_bin_trust_function_creators = 0;
quit;
```

### Configure the database for Zabbix server (/etc/zabbix/zabbix_server.conf):

```conf
DBHost=localhost
DBName=zabbix
DBUser=zabbix
DBPassword=zbxPa55Word
```

### Start Zabbix server and agent processes:

```shell
systemctl restart zabbix-server zabbix-agent apache2

systemctl enable zabbix-server zabbix-agent apache2
```

### Open Zabbix UI web page:

```
http://host/zabbix
```

### Credentials:

```yaml
Login: Admin

Password: zabbix
```

# Script to alert about changes in MySQL with Python and Zabbix via Telegram:

### Default Telegram Media type:

```
Alerts => Media types => Telegram => Enable

Users => Admin => Media => Telegram (Send to <token>)

Actions => Trigger actions => Operations => Send to Users => Admin => Send only to => Telegram
```

### Python script:

```
Alerts => Media types => Create {
    Name: TelegramPython

    Script: (/usr/lib/zabbix/alertscripts)/TelegramPython.py

    Script Parameters {
        {EVENT.NAME}
        {EVENT.TIME}
        {EVENT.DATE}
        {HOST.NAME}
        {EVENT.SEVERITY}
    }

    Message templates {
        Problem
        (maybe others too)
    }
}

Users => Admin => Media => TelegramPython (Send to <token>)

Actions => Trigger actions => Operations => Send to Users => Admin => Send only to => TelegramPython
```

```python
#!/usr/bin/python3
import requests
import sys

try:
    token = "6421311991:AAEb8Zp2xln3lzqaHRbA3cGNudp-eAvZdtM"
    chat = "5006697590"
    subject = sys.argv[1]
    time = sys.argv[2]
    date = sys.argv[3]
    hostname = sys.argv[4]
    severity = sys.argv[5]

    message = f"Problem: {subject}\n\
    Problem started at {time} on {date}\n\
    Host: {hostname}\n\
    Severity: {severity}\n"

    url = f"https://api.telegram.org/bot{token}/sendMessage"

    payload = {
        "chat_id": chat,
        "text": message,
    }

    response = requests.post(url, json=payload)

    if response.status_code == 200:
        print("OK")
    else:
        print(f"HTTP Error: {response.status_code}")
except Exception as e:
    print(f"Telegram notification failed: {e}")
```

### Create Database/Table for zabbix user:

```sql
create database zbxDB;
use zbxDB;
create table zbxTable(
    id int auto_increment primary key,
    user varchar(50) not null,
    pass varchar(50) not null
);
grant all privileges on zbxDB.zbxTable to zabbix@localhost;
```

### Create zabbix user home directory:

```shell
mkdir /var/lib/zabbix
```

### /var/lib/zabbix/.my.cnf:

```conf
[client]
user=zabbix
password=zbxPa55Word
```

### /etc/zabbix/zabbix_agentd.conf:

```conf
UserParameter=mysql.row.count, mysql -sNe "SELECT COUNT(*) FROM zbxDB.zbxTable;"
```

```shell
sudo service zabbix-agent restart
```

### Item:

```yaml
Name: MySQL Row Count
Type: Zabbix Agent
Key: mysql.row.count
Type of information: Numeric (unsigned)
Update interval: 10s
```

### Trigger:

```yaml
Name: MySQL; zbxDB.zbxTable row count changed
Expression: change(/Zabbix server/mysql.row.count)>=1
```

<br>
<br>
<br>

### UserParameter for monitoring cpu load percentage:

```conf
UserParameter=cpu.load, mpstat -P 0 | awk '$3 == "0" {print 100 - $NF}'
```

### Item:

```yaml
Name: CPU Load exceeded specific value
Type: Zabbix Agent
Key: cpu.load
Type of information: Numeric (float)
Update interval: 10s
```

### Trigger:

```yaml
Name: CPU Load exceeded 10%
Expression: last(/Zabbix server/cpu.load)>=10
```