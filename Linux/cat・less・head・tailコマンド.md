# 【Linux】cat・less・head・tail コマンド

Linux で使うファイルの内容を表示するコマンドについてまとめました。

# cat コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルの内容を表示する</span>

```bash

$ cat work01
```

`cat ［ファイル名］`

- 「concatenate」連結という意味  
   cat コマンドの本来の意味は「ファイルを連結して標準出力に出力する」
- 複数ファイルを指定すると、連結して出力できる。
- 引数なし、または＄ cat -のときは、キーボードで入力した同じ文字列が表示される。ctrl+D で終了
- リダイレクトでファイルの新規作成(>)や追記(>>)ができる。

- **よく使うオプション**  
  -n 行番号つけて表示する。<br>
  -p 2 行以上の空行を 1 行の空行にして表示する。<br>
  -E 行末に$を表示<br>

# less コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルを閲覧する</span>

```bash

$ less work01
```

`less ［ファイル名］`

- ファイルの内容を 1 画面ずつ表示する。（ペーシング機能）
- 部分的な読み込みを行うため、大きなファイルでも迅速に開くことができる。ログファイルなど。
- 他のコマンドの出力結果を less で閲覧できる。  
  $ コマンド | less

- **よく使うオプション**  
  -N 行番号つけて表示する。<br>
  -s 2 行以上の空行を 1 行の空行にして表示する。<br>
  -p 指定した文字列にハイライトをかける。検索に便利。<br>

# head コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">データの先頭のみ表示する</span>

```bash

$ head work01
```

`head［オプション］ ［ファイル名］`

- 複数のファイルを表示したいときは、ファイル名を並べる。
- オプションを指定しないときは、先頭 10 行を表示する。

- **よく使うオプション**  
  -c 出力する文字数を指定する。<br>
  -n 出力する行数を指定する。<br>

# tail コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">データの終わり部分のみ表示する</span>

```bash

$ tail work01
```

`tail［オプション］［ファイル名］`

- 複数のファイルを表示したいときは、ファイル名を並べる。
- オプションを指定しないときは、末尾 10 行を表示する。

- **よく使うオプション**  
  -f 指定されたファイルの末尾をリアルタイムで監視し、更新内容を表示する。<br>
  ctrl+c で終了するまで実行し続ける。<br>
  ログファイルの監視やデバッグ作業に使う。<br>
  -c 出力する文字数を指定する。<br>
  -n 出力する行数を指定する。<br>

---

### 参考にしたサイト

- [https://eng-entrance.com/linux_command_cat]
- [https://linuc.spa-miz.com/2021/02/03/extremes-the-cat-command-to-display-file-contents/]
- [https://qiita.com/ine1127/items/64b5b6cf52471c3fe59c] -[https://www.kakiro-web.com/tail-command/]
