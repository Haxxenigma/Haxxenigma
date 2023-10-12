# General

[wget](https://www.kali.org/tools/wget/)

```shell
wget [options] <url>
```

[curl](https://www.kali.org/tools/curl/)

```shell
curl [options] <url>
```

[openssh](https://www.kali.org/tools/openssh/)

```shell
scp /src/path/ user@host:/dest/path/
```

```shell
scp user@host:/dest/path/ /src/path/
```

<br>

[ssh2john — convert id_rsa key to a format that john will accept](https://www.kali.org/tools/john/#ssh2john "https://www.kali.org/tools/john/#ssh2john")

```shell
locate ssh2john.py
```

```shell
python ssh2john.py id_rsa > id_rsa.hash
```

```shell
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa.hash
```

```shell
chmod 600 id_rsa
```

```shell
ssh -i <id_rsa> user@host
```

```
-i identity_file        Selects a file from which the identity (private key) for public key authentication is read.  You can also specify a public key file to use the corresponding private key that is loaded in ssh‐agent(1) when  the  private  key  file  is not present locally.  The default is ~/.ssh/id_rsa, ~/.ssh/id_ecdsa, ~/.ssh/id_ecdsa_sk, ~/.ssh/id_ed25519, ~/.ssh/id_ed25519_sk and ~/.ssh/id_dsa.  Identity files may also be specified on a perhost basis in the configuration file.  It is possible to have multiple -i options (and multiple identities specified in configuration files).  If no certificates have been explicitly specified by the CertificateFile directive, ssh will also try to load certificate information from the filename obtained by appending ‐cert.pub to identity filenames.
```

[python](https://www.python.org/downloads/?ref=)

```shell
python3 [options] [-c cmd | -m mod | file | -]
```

```shell
python3 -m http.server [port]
```