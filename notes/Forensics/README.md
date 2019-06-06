# Forensics
ツールとか解法とかやったことない手法のメモとか
# 0．共通
何が来てもとりあえずやっとく．
## CUIツール
+ file
    + 別データが拡張子だけ変えてある場合があるので確認
+ strings
    + 一番簡単なのは，ascii文字でflagがべた貼りしてある場合
        + そうでなくても，steghide等のpasswordが貼ってある場合がある
    + `grep`と合わせたら簡単な問題は大体片付く
+ binwalk
    + とりあえず中身のデータを確認
    + 中身のデータを取り出せる
        + usage: `binwalk -e [file]`
+ exiftool
    + ファイルのExif情報が見れる
    + たまに怪しい文字列が見つかる
+ foremost
    + ファイルのヘッダやフッタ，内部データ構造に基づいてファイルを復元してくれる．
    + binwalkより強力？
## webツール
+ [CyberChef](https://gchq.github.io/CyberChef/)
    + 出てきた文字列が暗号文の場合に利用
# 1. 画像ファイル
中難易度まではツールの組み合わせでflagが取れる印象．
難易度が高い問題のほとんどは最終的には画像系ではなくなるか，エスパー系の問題．
## webツール
+ Google
    + 見慣れない単語はとりあえず検索するとツールの名前だったりする．
    + google画像検索にかける
+ [Steganography Online](https://stylesuxx.github.io/steganography/)
    + とりあえず投げてもいいけど満足感が低い．
    + たまに手元でできないのにこいつが解いてくる．
## CUIツール
+ steghide
    + jpgファイル用のsteganographyツール
    + パスワードは問題中で取得 or それっぽいのを予想
    + [stegcracker](https://github.com/Paradoxis/StegCracker)
        + Steghideのpassphraseの総当りができるツール
+ [zsteg](https://github.com/zed-0xff/zsteg)
    + png，bmpファイルにおけるLSB stego検出ツール
    + 青空白猫ツールでpng画像を見たときに，画像上部に帯状のノイズがのっていると大体これ
    + それ以外でもpngファイルは結構これ．
+ pngcheck
    + pngファイルが開けない場合に．

### スクリプト
+ 複数画像ファイルが渡されて面倒な時とか用
+ steghide用にwordlist.txtを作成しておく
    + wordlistに追加するもの
        + 空文字，大会名，ファイル名，ctf，flag，steghide，password，admin，問題中でみかけたそれらしい文字列
```
#!/bin/bash

file_name=${file%.*}

file $1
read -p "Hit enter:"

exiftool $1
read -p "Hit enter:"

binwalk $1
read -p "Hit enter:"

#steghide info $1 -p ""
steghide extract -sf $1 -p ""
echo pass: ${file_name}
#steghide info $1 -p "${file_name}"
steghide extract -sf $1 -p "${file_name}"
while read line
do
    echo pass: $line
    #steghide info $1 -p "$line"
    steghide extract -sf $1 -p "$line"
#done < ./wordlist.txt
done < $2
read -p "Hit enter:"

strings $1
```
## GUIツール
+ [青空白猫](https://digitaltravesia.jp/usamimihurricane/webhelp/_RESOURCE/MenuItem/another/anotherAoZoraSiroNeko.html)
    + 汎用ファイルアナライザ「青い空を見上げればいつもそこに白い猫」
    + 対応フォーマット: jpg，png，gif など
    + 中難易度ぐらいまでの問題ならコマンドとこれだけでなんとかなる．
+ [Stirling](https://www.vector.co.jp/soft/win95/util/se079072.html)
    + 使いやすいバイナリエディタ

# 2. 音声ファイル
問題タイトル，問題文がヒントになることが多い印象．
## CUIツール
+ [mp3stego](https://www.petitcolas.net/steganography/mp3stego/)
    + 平文⇔mp3 
## GUIツール
+ Audacity
+ [Sonic Visualiser](https://sonicvisualiser.org/download.html)
+ Qsstv(Linux)
    + [ﾋﾟﾋﾟｰｶﾞﾋﾟｶﾞﾋﾟｰ](https://charlesreid1.com/wiki/Qsstv)
        + [関連writeup: stallman_intensifies@201904wpi_by_ishioka](https://github.com/takushooo/writeup/tree/master/2019/04-wpi/Steganography/stallman_intensifies)
# 3. 動画ファイル
動画を見ていて音声に違和感があれば音声問題に，特になければ画像問題になる印象．
## ツール
+ ffmpeg
    + flagが書かれたフレームが挿入されている場合がある
+ imagemagick
    + フレーム切り出しは画像めちゃあって大変．
+ [search movie diff](https://github.com/teatime13/search_movie_diff)
    + 動画のフレームごとの差を求めて変化してた場合に保存するプログラム
+ [SiriusComp](http://phaku.net/siriuscomp/)
    + 比較明合成用フリーソフト
    + 大量の撮影画像から星の軌跡を描くことのできる合成「比較明合成」と同時にコマ撮り動画「タイムラプス動画」を作成できる．
## CUIツール
+ zipinfo
    + zipのメタ情報を調べる
+ unzip
    + 書くまでもないが，パスワードがかかっていないファイルだけが出てきてヒントになることもあったので一応．
+ [PkCrack](https://github.com/keyunluo/pkcrack)
    + 既知平文攻撃
        + zipの中身のファイルが分かっていれば，パスワードが分かっていなくても開ける．
    + zip以外にファイルが渡されている場合，それ自体やそこから抽出できるファイルで攻撃できる場合がある．
    + 圧縮フォーマットを合わせる必要がある
        + 関連wirteup: [she@201904xctf_by_ishioka](https://github.com/takushooo/writeup/tree/master/2019/04-xctf/Misc/otaku)
## GUIツール
+ [Lhaplus](https://forest.watch.impress.co.jp/library/software/lhaplus/)
    + pass付きzipのブルートフォースアタックができる．
+ winRAR
    + pkcrackでこれで作ったzipファイルが必要になる[問題](https://github.com/takushooo/writeup/tree/master/2019/04-xctf/Misc/otaku)があったので
# 5. pdfファイル
画像ファイルのみを抽出したり，pdf自体を編集したりしたら出てきたりもする．
## ツール
+ peepdf
    + pythonで作られているpdf解析ツール
    + 解析するだけでなく，脆弱性を突くようなコードが埋め込まれていた場合はその脆弱性情報も合わせて表示する．
    + Kali Linuxにも同梱
+ [pdfstreamdumper](http://sandsprite.com/blogs/index.php?uid=7&pid=57)
    + オープンソースのpdf解析ツール
+ [pdfcrack](http://pdfcrack.sourceforge.net/)
    + pdfからパスワードとコンテンツを復元するツール
# 6. Officeファイル
例えば，xxxx.docx→xxxx.zipに拡張子を変えて，解凍するとメタデータが見れたりする．
## ツール
+ [OfficeMalScanner](http://www.reconstructer.org/)
+ [Vba2Graph](https://github.com/MalwareCantFly/Vba2Graph)
    + VBAの解析・可視化


# 7. ディスクイメージ
## CUIツール
+ mount
+ fdisc
+ testdisk
+ photorec
+ foremost
+ The Sleuth Kit
    + fls
    + icat
## GUIツール
+ Autopsy
# 8. QRコード
主にSECCON用
## CUIツール
+ [strong-qr-decoder](https://github.com/waidotto/strong-qr-decoder)
    + 強力
+ [Zxing](https://github.com/zxing/zxing)
# 9. メモリダンプ
実際にはマルウェアの解析などで必要な知識になるらしい．
## ツール
+ Volatility
    + プロセス一覧
    + 通信の接続状況
    + プロセスのダンプ
    + レジストリ etc.
# 10.その他
[－・・－・　・－－・－　－・－－・　－－－・－　－－・－・　・－・－・　－－－－　・・　・・－　](https://morse.ariafloat.com/)
# 参考サイト
+ [Forensics入門(CTF)](https://qiita.com/knqyf263/items/6ebf06e27be7c48aab2e)
+ [CTF Forensics](https://raintrees.net/projects/a-painter-and-a-black-cat/wiki/CTF_Forensic)
+ [CTFに使用するツール類まとめ](https://waidotto.hatenadiary.org/entry/20120820/1345477008)