# I love images
## 問題文

A hacker left us something that allows us to track him in this image, can you find it?

### 問題ファイル
```
wget https://s3-eu-west-1.amazonaws.com/hubchallenges/Forensics/godot.png
```

## FLAG

```
FLAG{Not_Only_Base64}
```

## 解法
```
$ file godot.png
godot.png: PNG image data, 64 x 64, 8-bit/color RGBA, non-interlaced
$ file godot.png
godot.png: PNG image data, 64 x 64, 8-bit/color RGBA, non-interlaced
```
なんか入ってるみたいなので、zstegする。
```
$ zsteg godot.png
[?] 41 bytes of extra data after image end (IEND), offset = 0xdaa
/usr/lib/ruby/2.5.0/open3.rb:199: warning: Insecure world writable dir /home/takumasa/.local/bin in PATH, mode 040777
extradata:0         .. text: "IZGECR33JZXXIX2PNZWHSX2CMFZWKNRUPU======\n"
b1,rgb,msb,xy       .. file: dBase IV DBT, block length 19968, next free block index 13023744
b2,r,lsb,xy         .. text: "UUUUUUUUUUUU*"
b2,r,msb,xy         .. text: "nUUUUUUUUUUUU"
b2,g,lsb,xy         .. text: "4UUUUUUUUUUUU"
b2,b,msb,xy         .. text: "UUUUUUUUUUUUv"
b2,a,msb,xy         .. file: raw G3 (Group 3) FAX
b2,rgba,lsb,xy      .. text: ["S" repeated 48 times]
b2,abgr,lsb,xy      .. file: TeX font metric data (\342\342\342\342\342\342\342\342\342\342\342\342\342\342\342\342\342\342\342\342\342\342\342\036\241\273%\021)
b2,abgr,msb,xy      .. text: "xGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGx"
b3,r,msb,xy         .. file: hp200 (68010) BSD
b3,rgb,lsb,xy       .. file: X11 SNF font data, MSB first
b3,abgr,msb,xy      .. text: "ZWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtEWtE"
b4,r,lsb,xy         .. text: "$UUUUUUUUUUUUUUUUUUUUUUUUB"
b4,r,msb,xy         .. text: "YUUUUUUUUUUUUUUUUUUUUUUUU"
b4,g,lsb,xy         .. text: "CDDDDDDDDDDDDDDDDDDDDDDDD4!"
b4,g,msb,xy         .. text: "\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\","
b4,b,msb,xy         .. text: "UUUUUUUUUUUUUUUUUUUUUUUUYL\n"
b4,rgb,msb,xy       .. text: "%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR"
b4,bgr,msb,xy       .. text: "\\%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR%UR"
b4,abgr,msb,xy      .. text: "\\_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R_R"
```
抽出されたテキストデータ`IZGECR33JZXXIX2PNZWHSX2CMFZWKNRUPU======`を[CyberChef](https://gchq.github.io/CyberChef/)に投入する．
今回はBase32でデコードしてFLAGげっと。

### reference
