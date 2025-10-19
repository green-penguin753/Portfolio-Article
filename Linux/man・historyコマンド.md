# 【Linux】man・history コマンド

Linux で使うコマンドについてまとめました。

# man コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">オンラインマニュアルを表示する</span>

```bash
$ man passwd
PASSWD (1)
(説明)
```

`man ［セクション番号］調べる語句`

- 「manual」と言う意味。
- LinuxOS で使うコマンド、プログラム、機能に関する重要なドキュメントと情報を表示する。<br>
  コマンドの使用法と機能についてのヒントを得ることができる。
- 終了には「q キー」を入力する。

- **よく使うオプション**  
  -a 指定したコマンドに関連するすべてのマニュアルを表示する。  
  -k 指定したキーワードに関連するすべてのマニュアルを表示する。

- man ページ内（内部検索）で、<br>
  特定の文字列を検索したいときは、 / 検索したい語句を入力する。

- セクションを指定したマニュアルの表示
  - passwd のマニュアルの先頭の「PASSWD(1) 」とは、  
    セクション 1 に分類されている、ということ。
  - セクション５のマニュアルを表示したいときは、  
    $ man 5 passwd と入力する。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎マニュアルのセクション☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">
1 ・・・ユーザーコマンド<br>
2・・・システムコール<br>
3・・・システムライブラリや関数<br>
4・・・デバイスやデバイスドライバ<br>
5・・・ファイルの形式<br>
6・・・ゲームやデモなど<br>
7・・・その他<br>
8・・・システム管理系のコマンド<br>
9・・・カーネルなどの情報<br>

</div>

# history コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">過去に実行したコマンドの一覧を表示する</span>

```bash
$ history
1  ls -l
2  cd ~
3  pwd
(省略)
```

`history ［オプション］`

- 「! + 管理番号」と入力すると、その番号が割り振られているコマンドが再実行される。$!5
- キーボードの上下矢印キー（↑↓）で過去のコマンドを呼び出すこともできる。

- 表示する数を指定したいときは、数字を指定する。  
  $ history 3

- コマンド履歴の中から検索したい文字列を含むコマンドのみを抽出したいときは、パイプでつなぐ。  
  $ history | grep [検索したい文字列]
- 修正して実行したいときは、  
  内部検索（Ctrl + R）で、  
  (reverse-i-search)`':検索したい文字列を入力して、  
  左右矢印キー（←→）を入力すると、コマンドが修正できるようになる。

- **よく使うオプション**  
  -c 端末に記録されているコマンド履歴を消去する。  
  -w コマンド履歴をファイルに書き込む。  
  -a コマンド履歴をファイルに追記する。  
  -d 管理番号 指定した管理番号のコマンド履歴を削除する

---

### 参考にしたサイト

- [https://eng-entrance.com/linux-command-man]
- [https://www.bioerrorlog.work/entry/how-to-man-command]
- [https://qiita.com/suzuko24/items/f3852f76922ae98227aa]
- [https://eng-entrance.com/linux-command-history]
