# File Found
## 問題文

We found the following file on a machine, we know it contains a secret but we do not know what this file is can you help us obtain the code?

### 問題ファイル
```
wget https://s3-eu-west-1.amazonaws.com/hubchallenges/Forensics/foundfile
```

## FLAG

```
FLAG{FORENSICS_101}
```

## 解法
```
$ strings foundfile
<init>
Code
LineNumberTable
main
([Ljava/lang/String;)V
StackMapTable
SourceFile
HelloWorld.java
SYNT{SBERAFVPF_101}
HelloWorld
java/lang/Object
java/lang/String
length
charAt
(I)C
java/lang/System
Ljava/io/PrintStream;
java/io/PrintStream
print
(C)V
```
SYNTはよく見る
[CyberChef](https://gchq.github.io/CyberChef/)でROT13してFLAGげっと

### reference
