# [Web Server](https://ru.wikipedia.org/wiki/Веб-сервер)

**Install Apache2:**

```
apt install apache2
```

**Create folder for website:**

```
mkdir /var/www/example.com/
chown -R $USER:$USER /var/www/example.com/
chmod -R 755 /var/www/example.com/
nano /var/www/example.com/index.html
```

**/etc/apache2/sites-available/example.com.conf:**

```
<VirtualHost *:80>
    ServerAdmin webmaster@example.com
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/example.com
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

**Enable website:**

```
sudo a2ensite example.com.conf
sudo a2dissite 000-default.conf
```

**Start Apache2 service:**

```
systemctl start apache2
systemctl enable apache2

# OR

service apache2 start
service apache2 enable
```

**Create rule in firewall:**

```
ufw allow 'Apache'
ufw reload
ufw show
```

**Config test:**

```
sudo apache2ctl configtest
```

<br>
<br>

***Self-Signed SSL Certificate for Apache2***

```
sudo a2enmod ssl
sudo a2enmod headers

sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/apache2/cert.key -out /etc/ssl/apache2/cert.crt
```

**/etc/apache2/sites-available/example.com.conf:**

```
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
        SSLCertificateFile      /etc/ssl/apache2/cert.crt
        SSLCertificateKeyFile   /etc/ssl/apache2/cert.key

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

<br>
<br>
<hr>
<br>
<br>

![URL](https://i.imgur.com/el7IjNX.jpg)

Example Request:

```
GET / HTT/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

Example Response:

```
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>
```

HTTP Methods:

GET Request | POST Request | PUT Request | DELETE Request
:---:|:---:|:---:|:---:
This is used for getting information from a web server. | This is used for submitting data to the web server and potentially creating new records | This is used for submitting data to a web server to update information | This is used for deleting information/records from a web server.

HTTP Status Codes:

<table>
  <tr>
    <th>100-199 - Information Response</th>
    <td>These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are no longer very common.</td>
  </tr>
  <tr>
    <th>200-299 - Success</th>
    <td>This range of status codes is used to tell the client their request was successful.</td>
  </tr>
    <tr>
    <th>300-399 - Redirection</th>
    <td>These are used to redirect the client's request to another resource. This can be either to a different webpage or a different website altogether.</td>
  </tr>
    <tr>
    <th>400-499 - Client Errors</th>
    <td>Used to inform the client that there was an error with their request.</td>
  </tr>
    <tr>
    <th>500-599 - Server Errors</th>
    <td>This is reserved for errors happening on the server-side and usually indicate quite a major problem with the server handling the request.</td>
  </tr>
</table>

Common HTTP Status Codes:

<table>
  <tr>
    <th>200 - OK</th>
    <td>The request was completed successfully.</td>
  </tr>
  <tr>
    <th>201 - Created</th>
    <td>A resource has been created (for example a new user or new blog post).</td>
  </tr>
  <tr>
    <th>301 - Permanent Redirect</th>
    <td>This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere
      else and to look there instead.</td>
  </tr>
  <tr>
    <th>302 - Temporary Redirect</th>
    <td>Similar to the above permanent redirect, but as the name suggests, this is only a temporary change and it may
      change again in the near future.</td>
  </tr>
  <tr>
    <th>400 - Bad Request</th>
    <td>This tells the browser that something was either wrong or missing in their request. This could sometimes be used
      if the web server resource that is being requested expected a certain parameter that the client didn't send.</td>
  </tr>
  <tr>
    <th>401 - Not Authorised</th>
    <td>You are not currently allowed to view this resource until you have authorised with the web application, most
      commonly with a username and password.</td>
  </tr>
  <tr>
    <th>403 - Forbidden</th>
    <td>You do not have permission to view this resource whether you are logged in or not.</td>
  </tr>
  <tr>
    <th>405 - Method Not Allowed</th>
    <td>The resource does not allow this method request, for example, you send a GET request to the resource
      /create-account when it was expecting a POST request instead.</td>
  </tr>
  <tr>
    <th>404 - Page Not Found</th>
    <td>The page/resource you requested does not exist.</td>
  </tr>
  <tr>
    <th>500 - Internal Service Error</th>
    <td>The server has encountered some kind of error with your request that it doesn't know how to handle properly.
    </td>
  </tr>
  <tr>
    <th>503 - Service Unavailable</th>
    <td>This server cannot handle your request as it's either overloaded or down for maintenance.</td>
  </tr>
</table>

Common Request Headers:

* **Host:** Some web servers host multiple websites so by providing the host headers you can tell it which one you require, otherwise you'll just receive the default website for the server.

* **User-Agent:** This is your browser software and version number, telling the web server your browser software helps it format the website properly for your browser and also some elements of HTML, JavaScript and CSS are only available in certain browsers.

* **Content-Length:** When sending data to a web server such as in a form, the content length tells the web server how much data to expect in the web request. This way the server can ensure it isn't missing any data.

* **Accept-Encoding:** Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.

* **Cookie:** Data sent to the server to help remember your information.

Common Response Headers:

* **Set-Cookie:** Information to store which gets sent back to the web server on each request.

* **Cache-Control:** How long to store the content of the response in the browser's cache before it requests it again.

* **Content-Type:** This tells the client what type of data is being returned, i.e., HTML, CSS, JavaScript, Images, PDF, Video, etc. Using the content-type header the browser then knows how to process the data.

* **Content-Encoding:** What method has been used to compress the data to make it smaller when sending it over the internet.