# tiny_elves (fake) / HXPCTF2018

## まえがき

本レポジトリのdemoフォルダ内で`tiny_elves_fake.py`を実行したのち，解法以下の操作をすると出力は同様のものになる．

## 問題
[問題ページ](https://2018.ctf.link/internal/challenge/eb16fba4-025c-428b-8429-fa4c1aa52f3a.html)のリンクから[tiny_elves (fake)-ab1ec717a8568e56.tar.xz](https://2018.ctf.link/assets/files/tiny_elves%20(fake)-ab1ec717a8568e56.tar.xz)
をダウンロードして解凍すると，`tiny_elves_fake.py`が手に入る．

(`nc 116.203.19.166 34587`で接続すると，サーバ上でこのプログラムが実行されているようであった．)

```python3:tiny_elves_fake.py
#!/usr/bin/python3
import os, tempfile, subprocess

try:
    data = input(">").strip()
    if len(data) > 12: raise Exception("too large")

    with tempfile.TemporaryDirectory() as dirname:
        name = os.path.join(dirname, "user")
        with open(name, "w") as f: f.write(data)
        os.chmod(name, 0o500)
        print(subprocess.check_output(name))

except Exception as e:
    print("FAIL:", e)
    exit(1)
```

importされているモジュールを調べると，

### tempfile.TemporaryDirectory()
> 一時ディレクトリの作成．返されたオブジェクトは，コンテクスト管理者として使用することができる．

### subprocess.check_output(cmd)
> cmdの実行結果の出力をバイト列として返す．

というものである．

つまりこのプログラムは，

* 入力は最大12byteまで．
* 13byte以上は"too large"を出力して終了
* コマンドを書き込んだ一時ファイルが生成される
* subprocessでコマンドを実行する

という風に動作する．

要約すると，「12byte以下のコマンドを入力してflagを出力する」のがこの問題である．


## 方針
subprocessでコマンドの実行結果の出力をみることができるようなので，shebangを読み込んでインタプリタを指定してコマンドを実行する．

単純に`#!/bin/sh`でbashは読み込めるが，そのまま終了してしまう．

`#!/bin/ls .`でカレントディレクトリのファイルを見ると，
`flag.txt`があるのでこれを見れればよさそうだが，
`#!/bin/cat flag.txt`では長すぎるのでダメ．

そもそも"flag.txt"だけで8byteであるから，インタプリタの指定を同時に行うことはできないため，shebangでbashを読み込んでから，flagを出力するコマンドを打ち込めるようにしなければならない．

## bashのmanページを眺める
`#!/bin/sh`で9byteなので，残り3byteでなにかをしないといけない．

が，知らないのでbashのmanページを見てみると，
`-s`をオプションとして付けることで位置パラメータを設定できる対話的シェルを起動することができるようである．

対話的シェルがさえ起動できれば，あとは`cat flag.txt`でflagを出力すればいいだけとなる．

(ちなみに，ここで`/bin`を出力すれば使えるコマンドリストを得ることができる．"cat"は使えるようである．)

## 解法
上記をまとめると，
1. プログラムからインタプリタを指定してコマンドを実行することを考える．

2. `#!/bin/sh`だけでは何もできないのでオプションをつけて対話型にすることを考える．

3. `#!/bin/sh -s`で対話型シェルを起動する．

4. `cat flag.txt`

5. 終了するとflagが出力される．

`flag: hxp{#!_FTW__0k,_tH4t's_tO0_3aZy_4U!}`

## 雑感

スマブラが発売した夜，HXPCTFとも重なって研究室に人がいたので遅れていた実験をのんびり進めていたところ，
**「ちょっと面白いからやってみなよー」**
と声がかかり，実験結果を待つ間にこの問題に取り掛かかることになった．

そこで与えられた情報が，

* `#!/bin/sh -s`でコマンドが入力できる．
* `cat flag.txt`でflagが見れる，がダミーっぽい．

というものであった．

斯くして，すでに解かれた問題との戦いが幕を開けたのである.

とはいえ，脳停止でいろいろあそべたので，眠気覚ましにはとてもよかった．

## 参考サイト

* [bash: manページ](https://linuxjm.osdn.jp/html/GNU_bash/man1/bash.1.html)

* [忘れた時の pythonでシェルスクリプト実行](https://qiita.com/ego/items/3d23cda713f29f0dd141)

* [Pythonで一時ディレクトリを作って安全に後始末する](https://qiita.com/everylittle/items/aa7c6f612ff0a9db7f01)

* [11.6. tempfile — 一時ファイルやディレクトリの作成](https://docs.python.jp/3/library/tempfile.html)

* [Pythonでsubprocessを使ってコマンドを実行する方法](https://qiita.com/ssaito/items/cddd12dc762336484765)

* [17.5. subprocess — サブプロセス管理](https://docs.python.jp/3/library/subprocess.html)
