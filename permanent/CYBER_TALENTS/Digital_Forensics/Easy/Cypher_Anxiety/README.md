# Cypher_Anxiety
## 問題文

An image was leaked from a babies store. the manager is so annoyed because he needs to identify the image to fire charges against the responsible employee. the key is the md5 of the image

### 問題ファイル
```
wget https://s3-eu-west-1.amazonaws.com/talentchallenges/Forensics/find+the+image.zip
```

## FLAG

```
3beef06be834f3151309037dde4714ec
```

## 解法
平文で見えるところのメッセージからヒントを読み解く
+ cryptcatを使用
+ portは7070
+ passwordはP@ssawordaya

pcapファイルを`tcp.port == 7070`でフィルタリング
tcp streamでデータをraw保存 (ここでは`crypted`)

netcatでcryptedを送信して，cryptcatでデコードしながら受け取る．

terminal1
```
cryptcat -l -p 7070 -k P@ssawordaya > decrypted
```

terminal2
```
netcat localhost 12345 < crypted
```

flagはdecryptedのmd5

### reference
[man-cryptcat](https://manpages.debian.org/jessie/cryptcat/cryptcat.1.en.html)

