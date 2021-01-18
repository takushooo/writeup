# Hidden_Message
## 問題文

A cyber Criminal is hiding information in the below file . capture the flag ? submit Flag in MD5 Format

### 問題ファイル
```
wget https://s3-eu-west-1.amazonaws.com/talentchallenges/Forensics/hidden_message.jpg
```

## FLAG

```
b1a1f2855d2428930e0c9c4ce10500d5
```

## 解法
Copyright tagにMD5列が付与されてる

```
$ exiftool hidden_message.jpg
ExifTool Version Number         : 10.80
File Name                       : hidden_message.jpg
Directory                       : .
File Size                       : 72 kB
File Modification Date/Time     : 2017:03:02 01:59:40+09:00
File Access Date/Time           : 2021:01:18 14:48:35+09:00
File Inode Change Date/Time     : 2021:01:18 14:47:35+09:00
File Permissions                : rwxrwxrwx
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 96
Y Resolution                    : 96
Exif Byte Order                 : Big-endian (Motorola, MM)
Current IPTC Digest             : c51d5b8d73a91167e7fe4bbe5b41e2c9
Envelope Record Version         : 2
Coded Character Set             : UTF8
Application Record Version      : 2
Copyright Notice                : b1a1f2855d2428930e0c9c4ce10500d5
Image Width                     : 768
Image Height                    : 432
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 768x432
Megapixels                      : 0.332
```