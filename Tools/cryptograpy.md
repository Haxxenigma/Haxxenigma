# Cryptography

[CyberChef](https://gchq.github.io/CyberChef/) — All in one #1

[cryptii](https://cryptii.com/) — All in one #2

[dcode](https://www.dcode.fr/) — All in one #3

[rumkin](https://rumkin.com/tools/cipher/) — All in one #4

[CrypTool-Online](https://www.cryptool.org/en/cto/) — All in one #5

[URL Encode](https://www.urlencoder.org/)/[Decode](https://www.urldecoder.org/)

[Base64 Encode](https://www.base64encode.org/)/[Decode](https://www.base64decode.org/)

[Base32 Encode](https://emn178.github.io/online-tools/base32_encode.html)/[Decode](https://emn178.github.io/online-tools/base32_decode.html)

[ASCII, Hex, Binary, Decimal, Base64 converter](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html)

[ASCII Text to Hex Code converter](https://www.rapidtables.com/convert/number/ascii-to-hex.html)

[Vigenère Solver](https://www.guballa.de/vigenere-solver)/[Substitution Solver](https://www.guballa.de/substitution-solver)

[quipqiup — substitution solver](https://quipqiup.com/)

[Morse Code Decoder](https://morsedecoder.com/)

[Rot 1 - 25 Decryptor](https://rot13.com/)

[Ciphey](https://github.com/Ciphey/Ciphey)

[Crackstation](https://crackstation.net/)

<br>

[fcrackzip](https://www.kali.org/tools/fcrackzip/) — crack password protected zip files

```shell
fcrackzip -D -u -p <wordlist> <filename.zip>
```

[base64](https://linuxopsys.com/topics/base64-command-in-linux) — decode in CLI:

```shell
echo '<base64 string>' | base64 -d
```

## OpenSSL

Decrypt a file using RSA private key

```shell
openssl rsautl -decrypt -inkey pub_priv.key -in ciphertext.file -out decrypted.file
```

Decrypt a file using AES-256-CBC and a keyfile

```shell
openssl enc -d -aes-256-cbc -in ciphertext.file -out cleartext.file -pass file:./key.file
```

Decrypt a file using AES-256-CBC

```shell
openssl enc -aes-256-cbc -d -in file.txt.enc -out file.txt
```

Decrypt a file using AES-256-CBC with base64 encoded

```shell
openssl enc -aes-256-cbc -d -a -in file.txt.enc -out file.txt
```

Others reference: <https://gist.github.com/dreikanter/c7e85598664901afae03fedff308736b#file-encrypt_openssl-md>

## Create password

[mkpasswd](https://www.kali.org/tools/whois/#mkpasswd)

```shell
mkpasswd -m sha-512 <PASSWORD>
```

[openssl](https://www.openssl.org/docs/manmaster/man1/openssl.html)

```shell
openssl passwd -1 -salt <SALT> <PASSWORD>
```

## [John the Ripper](https://www.kali.org/tools/john/)

```shell
sudo apt install john
```

```shell
cp /etc/passwd passwd.txt && cp /etc/shadow shadow.txt

unshadow passwd.txt shadow.txt > hash_to_crack.txt

john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

### [ssh2john](https://www.kali.org/tools/john/#ssh2john)

> convert id_rsa key to a format that john will accept

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
-i identity_file        Selects a file from which the identity (private key) for public key authentication is read.  You can also specify a public key file to use the corresponding private key that is loaded in ssh‐agent(1) when  the  private  key  file  is not present locally.  The default is ~/.ssh/id_rsa, ~/.ssh/id_...
```

## [Hydra](https://www.kali.org/tools/hydra/)

```shell
sudo apt install hydra
```

### Options:

`-l LOGIN` or `-L FILE`: login with LOGIN name, or load several logins from FILE

`-p PASS`  or `-P FILE`: try password PASS, or load several passwords from FILE

`-C FILE`: colon separated "login:pass" format, instead of -L/-P options

`-M FILE`: list of servers to attack, one entry per line, ':' to specify port

`-t TASKS`: run TASKS number of connects in parallel per target (default: 16)

`-m OPT`: options specific for a module, see -U output for information

`-s PORT`: if the service is on a different default port, define it here

### FTP:

```shell
hydra -l <username> -P <wordlist> ftp://<IP-address>
```

### SSH:

```shell
hydra -l <username> -P <wordlist> ssh://<IP-address> -t 4
```

```shell
hydra -l <username> -P <wordlist> <IP-address> -t 4 ssh
```

### Post Web Form:

```shell
hydra -l <username> -P <wordlist> <IP-address> http-post-form "<path>:<login_credentials>:<invalid_response>"
```

```shell
hydra -l admin -P rockyou.txt 10.10.1.64 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"
```

## [Hashcat](https://www.kali.org/tools/hashcat/)

```shell
hashcat -m 500 <hash> <wordlists>
```

`-m, --hash-type <num>`

`-a, --attack-mode <num>`

`-o, --outfile <file>`

`-p, --separator <char>`

`-b, --benchmark`

```
| #     | Hash mode |
| ----- | --------- |
| 900   | MD4       |
| 0     | MD5       |
| 100   | SHA1      |
| 1300  | SHA2-224  |
| 1400  | SHA2-256  |
| 10800 | SHA2-384  |
| 1700  | SHA2-512  |
| 17300 | SHA3-224  |
| 17400 | SHA3-256  |
| 17500 | SHA3-384  |
| 17600 | SHA3-512  |
```

```
| #   | Attack Mode            |
| --- | ---------------------- |
| 0   | Straight               |
| 1   | Combination            |
| 3   | Brute-force            |
| 6   | Hybrid Wordlist + Mask |
| 7   | Hybrid Mask + Wordlist |
| 9   | Association            |
```

## Wordlists

[Wordlists](https://www.kali.org/tools/wordlists/)

```shell
sudo apt install wordlists

gunzip /usr/share/wordlists/rockyou.txt.gz
```

[SecLists](https://www.kali.org/tools/seclists/)

```shell
sudo apt install seclists
```