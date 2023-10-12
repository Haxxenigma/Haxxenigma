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