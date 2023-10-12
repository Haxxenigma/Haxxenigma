# Steganography

[List of `file` signatures](https://en.wikipedia.org/wiki/List_of_file_signatures "https://en.wikipedia.org/wiki/List_of_file_signatures")

```shell
file <filename>
```

[extracts `strings` in the given binary](https://linuxopsys.com/topics/strings-command-in-linux#:~:text=The%20strings%20command%20is%20used,error%20messages%2C%20and%20embedded%20strings "https://linuxopsys.com/topics/strings-command-in-linux#:~:text=The%20strings%20command%20is%20used,error%20messages%2C%20and%20embedded%20strings")

```shell
strings [options (-a | --all)] <filename>
```

[exiftool](https://www.kali.org/tools/libimage-exiftool-perl/ "https://www.kali.org/tools/libimage-exiftool-perl/")

```shell
exiftool <filename>
```

[binwalk](https://www.kali.org/tools/binwalk/ "https://www.kali.org/tools/binwalk/")

```shell
binwalk <filename>
```

[foremost](https://www.kali.org/tools/foremost/ "https://www.kali.org/tools/foremost/")

```shell
foremost -v <filename>
```

<br>

## Images

[tineye — Reverse search](https://tineye.com/ "https://tineye.com/")

[imagemagick — do image manipulation](https://imagemagick.org/ "https://imagemagick.org/")

[Stegsolve.jar — unhide flag from an image](https://yandex.kz/search/?text=Stegsolve.jar "https://yandex.kz/search/?text=Stegsolve.jar")

[SmartDeblur — fix blurry on image](https://github.com/Y-Vladimir/SmartDeblur "https://github.com/Y-Vladimir/SmartDeblur")

[tesseract — scan text in image and convert it to .txt file](https://tesseract-ocr.github.io/ "https://tesseract-ocr.github.io/")

<br>

[steghide — File carve](https://www.kali.org/tools/steghide/ "https://www.kali.org/tools/steghide/")

```shell
steghide --extract -sf <filename>
```

[pngcheck — Check for any corruption on PNG](https://manpages.ubuntu.com/manpages/focal/man1/pngcheck.1.html "https://manpages.ubuntu.com/manpages/focal/man1/pngcheck.1.html")

```shell
pngcheck <filename>
```

[zsteg — Detect stegano-hidden data in PNG & BMP](https://github.com/zed-0xff/zsteg "https://github.com/zed-0xff/zsteg")

```shell
zsteg -a <filename>
```

[stegcracker — brute-force password utility to uncover hidden data inside files](https://www.kali.org/tools/stegcracker/ "https://www.kali.org/tools/stegcracker/")

```shell
stegcracker <filename> <wordlist>
```

<br>

[futureboy — Steganographic Encoder/](https://futureboy.us/stegano/encinput.html "https://futureboy.us/stegano/encinput.html")[Decoder](https://futureboy.us/stegano/decinput.html "https://futureboy.us/stegano/decinput.html")

[stylesuxx — Steganographic Encoder/Decoder](http://stylesuxx.github.io/steganography/ "http://stylesuxx.github.io/steganography/")

[mobilefish — Steganographic Encrypter/Decrypter](https://www.mobilefish.com/services/steganography/steganography.php "https://www.mobilefish.com/services/steganography/steganography.php")

[manytools — Encoder text into image](https://manytools.org/hacker-tools/steganography-encode-text-into-image/ "https://manytools.org/hacker-tools/steganography-encode-text-into-image/")

[StegOnline](https://stegonline.georgeom.net/upload "https://stegonline.georgeom.net/upload")

[Magic Eye Solver/Viewer](http://magiceye.ecksdee.co.uk/ "http://magiceye.ecksdee.co.uk/")

<br>

## Compressed file

[zipdetails — display details about the internal structure of a Zip file](https://manpages.ubuntu.com/manpages/trusty/man1/zipdetails.1.html "https://manpages.ubuntu.com/manpages/trusty/man1/zipdetails.1.html")

```shell
zipdetails -v <filename>
```

[zipinfo — show details info about Zip file](https://manpages.ubuntu.com/manpages/lunar/man1/zipinfo.1.html "https://manpages.ubuntu.com/manpages/lunar/man1/zipinfo.1.html")

```shell
zipinfo <filename>
```

[zip — attempt to repair a corrupted Zip file](https://manpages.ubuntu.com/manpages/focal/man1/zip.1.html "https://manpages.ubuntu.com/manpages/focal/man1/zip.1.html")

```shell
zip -FF <filename> --out <outputfile>
```

[fcrackzip — Brute-force the zip password](https://www.kali.org/tools/fcrackzip/ "https://www.kali.org/tools/fcrackzip/")

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

<br>

## Mucis file

[Audacity](https://ru.wikipedia.org/wiki/Audacity "https://ru.wikipedia.org/wiki/Audacity")

[Sonic Visualizer — Look at spectogram and other few Pane](https://en.wikipedia.org/wiki/Sonic_Visualiser "https://en.wikipedia.org/wiki/Sonic_Visualiser")

[Deepsound](https://medium.com/@ibnshehu/deepsound-audio-steganography-tool-f7ca0a897576 "https://medium.com/@ibnshehu/deepsound-audio-steganography-tool-f7ca0a897576")

[SilentEye](https://yandex.kz/search/?text=SilentEye "https://yandex.kz/search/?text=SilentEye")

[Stegonaut](https://www.stegonaut.com/ "https://www.stegonaut.com/")

<br>

## PDF

[pdfinfo](https://poppler.freedesktop.org/ "https://poppler.freedesktop.org/")

```shell
sudo apt install poppler-utils
```

```shell
pdfinfo <filename>
```

[qpdf](https://github.com/qpdf/qpdf "https://github.com/qpdf/qpdf")

[PDFStreamdumper](https://github.com/zha0/pdfstreamdumper "https://github.com/zha0/pdfstreamdumper")

[pdfcrack](https://www.kali.org/tools/pdfcrack/ "https://www.kali.org/tools/pdfcrack/")

[pdfimages](https://manpages.ubuntu.com/manpages/xenial/man1/pdfimages.1.html "https://manpages.ubuntu.com/manpages/xenial/man1/pdfimages.1.html")

[pdfdetach](https://manpages.ubuntu.com/manpages/kinetic/man1/pdfdetach.1.html "https://manpages.ubuntu.com/manpages/kinetic/man1/pdfdetach.1.html")

[pdf-parser](https://www.kali.org/tools/pdf-parser/ "https://www.kali.org/tools/pdf-parser/")

[peepdf](https://github.com/jesparza/peepdf "https://github.com/jesparza/peepdf")

[pdfid](https://www.kali.org/tools/pdfid/ "https://www.kali.org/tools/pdfid/")

[pdftotext](https://pdftotext.com/ "https://pdftotext.com/")

<br>

## Text

[spammimic — can decode hide message in spam text](https://www.spammimic.com/ "https://www.spammimic.com/")