# 【Linux】cd・pwd・ls コマンド

Linux で使うコマンドについてまとめました。

# cd コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ディレクトリを変更する</span>

```bash
$ cd
```

`cd ［移動先のディレクトリ名］`

- 「Change directory」と言う意味。
- ディレクトリを指定しない時や「~」を指定したときは、  
  ホームディレクトリに移動する。
- 「-」を指定したときは、直前にいたディレクトリに移動する。
- 「..」を指定したときは、親ディレクトリに移動する。
- ファイル名は指定できない。

# pwd コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">現在使っているディレクトリ（カレントディレクトリ）の表示</span>

```bash
$ pwd
/home/user

```

`pwd ［オプション］ `

- 「print working directory」と言う意味。
- 絶対パスで表示される。

# ls コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルやディレクトリの一覧を取得する</span>

```bash

$ ls
ダウンロード デスクトップ ビデオ 画像
テンプレート ドキュメント 音楽 公開

```

`ls ［オプション］［ファイルまたはディレクトリ名］`

- 「list」と言う意味。

- ファイルやディレクトリ名を指定しないときは、カレントディレクトリが一覧表示される。

- $ ls /usr と指定したときは、  
  /usr ディレクトリ内を参照している。

- **よく使うオプション**  
  -a すべてのファイルを表示（隠しファイルを含む）  
  -l ファイルの詳細を表示  
  -R 指定したディレクトリ以下すべてを並べる(tree コマンドはツリー形式で表示)  
  -t 更新日時ごとにファイルを並べる  
  -h ファイルサイズを読みやすい形式で表示。「4.0K」などと表示される

☀︎ オプションはつなげて使うこともできる。順不同。 -la、-lh、-ltr など

<br>

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎-lオプションの詳細表示☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">

```bash
$ ls -l
-rw-r--r-- 1 root root   11 Dec 23 13:11 a.txt
drwxr-xr-x 2 root root 4096 Dec 23 13:14 test

```

「-」・・・ファイルタイプ<br>
「rw-r--r--」・・・パーミッション（アクセス権限） <br>
「1」・・・ハードリンクの数 <br>
「root」・・・所有者 <br>
「root」・・・グループ名 <br>
「11」・・・バイトサイズ <br>
「Dec 23 13:11」・・・タイムスタンプ(更新日時) <br>
「a.txt」・・・ファイル名 <br>

</div>

---

### 参考にしたサイト

- [https://eng-entrance.com/linux_command_ls]
- [https://qiita.com/chihiro/items/6e1404c41e1236a9efe1]
