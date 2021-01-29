# bflag
## 問題文

All of us started from the bottom. Now it's your turn.

### 問題ファイル
```
wget https://hubchallenges.s3-eu-west-1.amazonaws.com/Forensics/bflag.pcap
```

## FLAG

```
analyze_packet_for_fun
```

## 解法
目grepでそれっぽいの見つけてしまった。
httpとかでフィルタをかけるとよさそう。

問題はformat指定がないのでエスパーだったこと

+ FLAG{analyze_packet_for_fun}
+ flag{analyze_packet_for_fun}
+ /f14g/analyze_packet_for_fun

あたりを試した後で、まさかの中身だけ。

### reference
