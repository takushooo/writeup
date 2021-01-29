# Partition Lost
## 問題文

Our Company's CEO had a car accident. His HDD was damaged and he lost all his files and partitions. Can you help him to recover his important data

### 問題ファイル
```
wget https://s3-eu-west-1.amazonaws.com/talentchallenges/Forensics/partition-lost.img
```

## FLAG

```
FLAG(701_L@b$_DR_DFIR)
```

## 解法
```
$ fls partition-lost.img
r/r 4-128-4:    $AttrDef
r/r 8-128-2:    $BadClus
r/r 8-128-1:    $BadClus:$Bad
r/r 6-128-1:    $Bitmap
r/r 7-128-1:    $Boot
d/d 11-144-4:   $Extend
r/r 2-128-1:    $LogFile
r/r 0-128-1:    $MFT
r/r 1-128-1:    $MFTMirr
r/r 9-128-8:    $Secure:$SDS
r/r 9-144-11:   $Secure:$SDH
r/r 9-144-5:    $Secure:$SII
r/r 10-128-1:   $UpCase
r/r 3-128-3:    $Volume
d/d 27-144-1:   System Volume Information
-/r * 29-128-1: fl@4.rar
-/r * 30-128-4: MCU(10000000-12000000).bin
-/r * 31-128-3: setup.exe
d/d 48: $OrphanFiles
```
fl@4.rarが怪しい
```
$ icat partition-lost.img -r 29-128-1 > fl@4.rar
```
取り出したfl@4.rarは壊れていて解凍できない
```
$ strings fl@4.rar
fl@4.txt
fMFLAG(701_L@b$_DR_DFIR)
```
FLAGげっと `FLAG(701_L@b$_DR_DFIR)`
### reference
