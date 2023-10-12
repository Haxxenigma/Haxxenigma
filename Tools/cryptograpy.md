# Cryptography

[URL Encode/](https://www.urlencoder.org/ "https://www.urlencoder.org/")[Decode](https://www.urldecoder.org/ "https://www.urldecoder.org/")

[Base64 Encode/](https://www.base64encode.org/ "https://www.base64encode.org/")[Decode](https://www.base64decode.org/ "https://www.base64decode.org/")

[Base32 Encode/](https://emn178.github.io/online-tools/base32_encode.html "https://emn178.github.io/online-tools/base32_encode.html")[Decode](https://emn178.github.io/online-tools/base32_decode.html "https://emn178.github.io/online-tools/base32_decode.html")

[ASCII, Hex, Binary, Decimal, Base64 converter](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html "https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html")

[ASCII Text to Hex Code Converter](https://www.rapidtables.com/convert/number/ascii-to-hex.html "https://www.rapidtables.com/convert/number/ascii-to-hex.html")

[cryptii — All in one #1](https://cryptii.com/ "https://cryptii.com/")

[dcode — All in one #2](https://www.dcode.fr/ "https://www.dcode.fr/")

[rumkin — All in one #3](https://rumkin.com/tools/cipher/ "https://rumkin.com/tools/cipher/")

[quipqiup](https://quipqiup.com/ "https://quipqiup.com/")

[Substitution Solver](https://www.guballa.de/substitution-solver "https://www.guballa.de/substitution-solver")

[Vigenère Solver](https://www.guballa.de/vigenere-solver "https://www.guballa.de/vigenere-solver")

[Morse code Decoder](http://www.unit-conversion.info/texttools/morse-code/ "http://www.unit-conversion.info/texttools/morse-code/")

[Rot 1 - 25 Decryptor](https://rot13.com/ "https://rot13.com/")

[ASCII85 Decoder](https://cryptii.com/pipes/ascii85-encoding "https://cryptii.com/pipes/ascii85-encoding")

[Ciphey](https://github.com/Ciphey/Ciphey "https://github.com/Ciphey/Ciphey")

Base64 Decode in CLI:

```shell
echo '<base64 string>' | base64 -d
```

<br>

[CyberChef — All in one](https://gchq.github.io/CyberChef/ "https://gchq.github.io/CyberChef/")

[Crackstation — Crack Hash](https://crackstation.net/ "https://crackstation.net/")

[Cryptool](https://www.cryptool.org/en/ "https://www.cryptool.org/en/")

[John the Ripper](https://www.kali.org/tools/john/ "https://www.kali.org/tools/john/")

[Hashcat](https://www.kali.org/tools/hashcat/ "https://www.kali.org/tools/hashcat/")

<br>

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

Others reference
https://gist.github.com/dreikanter/c7e85598664901afae03fedff308736b#file-encrypt_openssl-md

<br>

## Cracking compressed file

[John the Ripper](https://www.kali.org/tools/john/ "https://www.kali.org/tools/john/")

```shell
john --wordlist=<wordlist> <hashfile>
```

[fcrackzip](https://www.kali.org/tools/fcrackzip/ "https://www.kali.org/tools/fcrackzip/")

```shell
fcrackzip -D -u -p <wordlist> <filename.zip>
```