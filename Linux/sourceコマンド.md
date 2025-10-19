# 【Linux】source コマンド

シェルの csh や bash で利用できる「source コマンド」についてまとめました。

# source コマンド

source コマンドとは、  
ファイルに書かれたコマンドを<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">現在のシェル環境で実行する</span>

```bash
$ source sample.sh

```

`source ファイル名 [引数1] [引数2‥]`

・実行権(x)がなくても、読み取り権(r)があれば実行できる。  
・if 文など制御コマンドと組み合わせると複雑な処理ができて便利。

###### 引数を指定した source コマンド

```bash
#!/bin/bash

VAR=氏名:$1  #VAR変数に引数を指定する
echo $1
```

```bash
$ source sample.sh 佐藤
氏名:佐藤
```

###### source コマンドでの変数の保持

```bash
$ echo $VAR
氏名:佐藤
```

- source コマンドでは、実行したファイルで扱われた変数「氏名:佐藤」が保持されている。
- $ source sample.sh 〇〇 とすると上書きされる。

# bash コマンドとの使い分け

- source コマンドは、  
  設定ファイル(~/.bashrc)などの変更をすぐに反映させたいときに使う。

- bash コマンドは、  
  元のプロセスとは完全に独立したプロセスなので、  
  元のシェル環境を変えたくないとき(スクリプトのテストなど)に使う。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎サブシェルとは☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">
・シェル実行環境のコピー。<br>
・子プロセスを作成するとは限らない。<br>
・サブシェル内で変数を変更しても、元のシェル環境には影響しない。
</div>

---

### 参考にしたサイト

- [https://eng-entrance.com/linux-command-source]
- [https://qiita.com/YumaInaura/items/00437e6ab14d96adb71f]
- [https://eng-entrance.com/linux-command-source#source-3]
- サブシェル[https://qiita.com/ko1nksm/items/19d300c4cb812b0fde1e]
