# \*Stallman intensifies*

中身は5枚のJPEG画像とpass付の7zファイル

7zファイルが解凍できればflag GETと予想して，5枚のJPEG画像を調べる．

```
青空白猫[^1]でJPEG画像を調べると，2枚の画像にsteghideの可能性がある．
[^1]: https://digitaltravesia.jp/usamimihurricane/webhelp/_RESOURCE/MenuItem/another/anotherAoZoraSiroNeko.html
```

`bash steg.sh`
```
#!/bin/bash

file_name=${file%.*}

file $1
read -p "Hit enter:"

exiftool $1
read -p "Hit enter:"

binwalk $1
read -p "Hit enter:"

steghide info $1 -p ""
echo pass: ${file_name}
steghide info $1 -p "${file_name}"
while read line
do
    echo pass: $line
    steghide info $1 -p "$line"
done < ./wordlist.txt
read -p "Hit enter:"

strings $1
```

## tool
+ 汎用ファイルアナライザ "青い空を見上げればいつもそこに白い猫" https://digitaltravesia.jp/usamimihurricane/webhelp/_RESOURCE/MenuItem/another/anotherAoZoraSiroNeko.html

+ sstv signal "Qsstv"
https://charlesreid1.com/wiki/Qsstv