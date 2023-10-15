# Passwords

[Create password](https://www.kali.org/tools/whois/ "https://www.kali.org/tools/whois/")

```shell
mkpasswd -m sha-512 <PASSWORD>
```

```shell
openssl passwd -1 -salt <SALT> <PASSWORD>
```

[John the Ripper](https://www.kali.org/tools/john/ "https://www.kali.org/tools/john/")

```shell
sudo apt install john
```

```shell
cp /etc/passwd passwd.txt && cp /etc/shadow shadow.txt

unshadow passwd.txt shadow.txt > hash_to_crack.txt

john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

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

[Hydra](https://www.kali.org/tools/hydra/ "https://www.kali.org/tools/hydra/") | [(Cheatsheet)](https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Hydra.md "https://github.com/Haxxenigma/CybSecChallenges/blob/main/TryHackMe/Hydra.md")

```shell
sudo apt install hydra
```

```shell
hydra -l root -P /usr/share/wordlists/metasploit/unix_passwords.txt -t 6 ssh://192.168.1.123
```

# Wordlists

[Wordlists](https://www.kali.org/tools/wordlists/ "https://www.kali.org/tools/wordlists/")

```shell
sudo apt install wordlists

gunzip /usr/share/wordlists/rockyou.txt.gz
```

[SecLists](https://www.kali.org/tools/seclists/ "https://www.kali.org/tools/seclists/")

```shell
sudo apt install seclists
```