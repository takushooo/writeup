# G&P_List
## 問題文

Just Open the File and Capture the flag . Submission in MD5

### 問題ファイル
```
wget https://s3-eu-west-1.amazonaws.com/talentchallenges/Forensics/G%26P+lists.docx
```

## FLAG

```
877c1fa0445adaedc5365d9c139c5219
```

## 解法

```
$ unzip G\&P+lists.docx -d tmp
$ cat tmp/Flag.txt
```