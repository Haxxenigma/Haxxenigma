# [Apache2](https://httpd.apache.org/ "https://httpd.apache.org/")

### Install Apache2:

```shell
apt install apache2
```

### Create folder for website:

```shell
mkdir /var/www/example.com/
chown -R $USER:$USER /var/www/example.com/
chmod -R 755 /var/www/example.com/
nano /var/www/example.com/index.html
```

### /etc/apache2/sites-available/example.com.conf:

```xml
<VirtualHost *:80>
    ServerAdmin webmaster@example.com
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/example.com
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

### Enable website:

```shell
sudo a2ensite example.com.conf
sudo a2dissite 000-default.conf
```

### Start Apache2 service:

```shell
systemctl start apache2
systemctl enable apache2
```

```shell
service apache2 start
service apache2 enable
```

### Create rule in firewall:

```shell
ufw allow 'Apache'
ufw reload
ufw show
```

### Config test:

```shell
sudo apache2ctl configtest
```

<br>

## Self-Signed SSL Certificate for Apache2

```shell
sudo a2enmod ssl
```

```shell
sudo openssl req -x509 -days 365 -nodes -newkey rsa:4096 -keyout private-key.pem -out public-cert.pem
```

### /etc/apache2/sites-available/example.com.conf:

```xml
<VirtualHost *:80>
        Servername example.com
        ServerAlias www.example.com
        
        Redirect permanent / https://example.com
</VirtualHost>

<VirtualHost *:443>
        ServerName example.com
        ServerAlias www.example.com
        ServerAdmin webmaster@example.com
        DocumentRoot /var/www/example.com

        SSLEngine on
        SSLCertificateFile      public-cert.pem
        SSLCertificateKeyFile   private-key.pem

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```