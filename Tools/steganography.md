# Steganography

[List of `file` signatures](https://en.wikipedia.org/wiki/List_of_file_signatures)

```shell
file <filename>
```

[extracts `strings` in the given binary](https://linuxopsys.com/topics/strings-command-in-linux#:~:text=The%20strings%20command%20is%20used,error%20messages%2C%20and%20embedded%20strings)

```shell
strings [options (-a | --all)] <filename>
```

[exiftool](https://www.kali.org/tools/libimage-exiftool-perl/)

```shell
exiftool <filename>
```

[binwalk](https://www.kali.org/tools/binwalk/)

```shell
binwalk <filename>
```

[foremost](https://www.kali.org/tools/foremost/)

```shell
foremost -v <filename>
```

## Images

[TinEye](https://tineye.com/) — Reverse Image Search

[ImageMagick](https://imagemagick.org/) — do image manipulation

[Stegsolve.jar](https://yandex.kz/search/?text=Stegsolve.jar) — unhide flag from an image

[SmartDeblur](https://github.com/Y-Vladimir/SmartDeblur) — fix blurry on image

[Tesseract](https://tesseract-ocr.github.io/) — scan text in image and convert it to .txt file

<br>

[steghide](https://www.kali.org/tools/steghide/) — File carve

```shell
steghide --extract -sf <filename>
```

[pngcheck](https://manpages.ubuntu.com/manpages/focal/man1/pngcheck.1.html) — Check for any corruption on PNG

```shell
pngcheck <filename>
```

[zsteg](https://github.com/zed-0xff/zsteg) — Detect stegano-hidden data in PNG & BMP

```shell
zsteg -a <filename>
```

[stegcracker](https://www.kali.org/tools/stegcracker/) — brute-force password utility to uncover hidden data inside files

```shell
stegcracker <filename> <wordlist>
```

<br>

[futureboy — Steganographic Encoder/](https://futureboy.us/stegano/encinput.html)[Decoder](https://futureboy.us/stegano/decinput.html)

[stylesuxx — Steganographic Encoder/Decoder](http://stylesuxx.github.io/steganography/)

[mobilefish — Steganographic Encrypter/Decrypter](https://www.mobilefish.com/services/steganography/steganography.php)

[manytools — Encoder text into image](https://manytools.org/hacker-tools/steganography-encode-text-into-image/)

[StegOnline](https://stegonline.georgeom.net/upload)

[Magic Eye Solver/Viewer](http://magiceye.ecksdee.co.uk/)

## Compressed file

[zipdetails](https://manpages.ubuntu.com/manpages/trusty/man1/zipdetails.1.html) — display details about the internal structure of a Zip file

```shell
zipdetails -v <filename>
```

[zipinfo](https://manpages.ubuntu.com/manpages/lunar/man1/zipinfo.1.html) — show details info about Zip file

```shell
zipinfo <filename>
```

[zip](https://manpages.ubuntu.com/manpages/focal/man1/zip.1.html) — attempt to repair a corrupted Zip file

```shell
zip -FF <filename> --out <outputfile>
```

[fcrackzip](https://www.kali.org/tools/fcrackzip/) — Brute-force the zip password

```shell
fcrackzip -D -u -p <wordlist>  <filename>
```

To crack 7z:

1.  ```
    7z2hashcat32-1.3.exe filename.7z
    ```

2.  ```
    john --wordlist=/usr/share/wordlists/rockyou.txt hash
    ```

## Mucis file

[Audacity](https://ru.wikipedia.org/wiki/Audacity)

[Sonic Visualizer](https://en.wikipedia.org/wiki/Sonic_Visualiser) — Look at spectogram and other few Pane

[Deepsound](https://medium.com/@ibnshehu/deepsound-audio-steganography-tool-f7ca0a897576)

[SilentEye](https://yandex.kz/search/?text=SilentEye)

[Stegonaut](https://www.stegonaut.com/)

## PDF

[pdfinfo](https://poppler.freedesktop.org/)

```shell
sudo apt install poppler-utils
```

```shell
pdfinfo <filename>
```

[qpdf](https://github.com/qpdf/qpdf)

[PDFStreamdumper](https://github.com/zha0/pdfstreamdumper)

[pdfcrack](https://www.kali.org/tools/pdfcrack/)

[pdfimages](https://manpages.ubuntu.com/manpages/xenial/man1/pdfimages.1.html)

[pdfdetach](https://manpages.ubuntu.com/manpages/kinetic/man1/pdfdetach.1.html)

[pdf-parser](https://www.kali.org/tools/pdf-parser/)

[peepdf](https://github.com/jesparza/peepdf)

[pdfid](https://www.kali.org/tools/pdfid/)

[pdftotext](https://pdftotext.com/)

## Text

[spammimic — can decode hide message in spam text](https://www.spammimic.com/)