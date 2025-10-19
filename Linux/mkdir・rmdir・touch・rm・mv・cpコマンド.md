# 【Linux】mkdir・rmdir・touch・rm・mv・cp コマンド

Linux で基本的なファイル操作に使うコマンドについてまとめました。

# mkdir コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ディレクトリを新規作成する</span>

```bash

$ mkdir work01
```

`mkdir［オプション］［作成するディレクトリ名］`

- 「make directory」という意味。

- **よく使うオプション**  
  -m パーミッションを指定しディレクトリを作成する。  
   $ mkdir -m 666 work02<br><br>
  -p 親ディレクトリが存在しないときでも、<br>
  自動的に親ディレクトリと子ディレクトリを作成する。  
   $ mkdir -p work01/work02<br><br>
  -v ディレクトリ作成時に詳細を表示する。  
   $ mkdir -v work01  
   mkdir: ディレクトリ 'work01' を作成しました

# rmdir コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ディレクトリを削除する</span>

```bash
$ rmdir work01
```

`rmdir ［オプション］［ディレクトリ名］`

- 「remove directory」という意味。
- ディレクトリ内にファイルがあるときは、削除できない。
- ディレクトリ内のファイルもすべて削除するには、rm-r コマンドを使う。

- **よく使うオプション**  
  -p 指定したディレクトリすべてを削除する。<br>
  $ rmdir -p work01/work02 なら、work01 と work02 の両方が削除される。<br><br>
  -v ディレクトリを削除するときに詳細を表示する。<br>
  $ rmdir -v work01 <br>
  rmdir: ディレクトリ 'work01' を削除しています<br><br>
  --ignore-fail-on-non-empty<br>
  ディレクトリが空ではないときに出るエラーを表示しない。<br>
  削除もされていない。<br>

# touch コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルのタイムスタンプの更新、ファイルの新規作成する</span>

```bash
$ touch a.dat

```

`touch ［オプション］ファイル名 `

- 存在するファイルを指定したときは、  
  タイムスタンプ(更新日時と変更日時)を更新する。
- 存在しないファイルの場合は、  
  ファイルサイズが 0 バイトの空のファイルを新規作成する。

- **よく使うオプション**  
  -d 日時を指定する。  
   $ touch -d "2016-9-20 20:30" a.dat<br><br>
  -r 他のファイルのタイムスタンプと同一にする。  
   $ touch -r 既存のファイル名 対象ファイル名<br><br>
  -c ファイルを新規作成しない。<br>
  オプションなしの場合、存在しないファイルを指定したら新規作成される。  
   $ touch -c ファイル名

# rm コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルやディレクトリを削除する</span>

```bash
$ rm a.dat

```

`rm ［オプション］ファイル名 `

- 「remove」という意味。
- 基本的にはファイルを対象としている。
- 複数のファイルを削除したいときは、ファイル名を並べる。
- すべてのファイルを消したいときは、$ rm \*

- **よく使うオプション**  
  -i ファイルの削除前に確認する。「y」または「n」を入力すると削除される。<br>
  -f エラー表示せず、ファイルを強制的に削除する。<br>
  -r ディレクトリも削除の対象とする。 <br>
  -v ファイルを削除するときに詳細を表示する。<br>
  $ rm -v work01<br>
  'work01' を削除しました

# mv コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルやディレクトリの移動、名称を変更する。</span>

```bash
$ mv test01.txt test
$ mv test01.txt test02.txt

```

移動：`mv 元ファイル［オプション］移動するディレクトリ `  
名称変更：`mv 元ファイル［オプション］変更後のファイル名 `

- 「move」という意味。
- ディレクトリでも同じ。
- 複数のファイルを移動したいときは、元ファイル名を並べる。

- **よく使うオプション**  
  -i ファイルの移動・上書きする前に確認する。<br>
  「y」または「n」を入力すると実行される。<br>
  -n 移動先に同名のファイルがあるときは、ファイルを上書きしない。<br>
  -v 移動・上書きしたときに詳細を表示する。<br>
  -u 元のファイルが新しいときにのみ移動する。<br>
  -b 上書きするときにバックアップを作成する。

# cp コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルやディレクトリをコピーする</span>

```bash

$ cp test01.txt test02.txt
```

`cp［オプション］［コピー元］［コピー先］`

- 「copy」という意味。
- 複数のファイルをコピーしたいときは、ファイル名を並べる
- すべてのファイルをコピーしたいときは、$ cp file\* ディレクトリ名

- **よく使うオプション**  
  -r ディレクトリごと再帰的にコピーする。<br>
  -i ファイルをコピーする前に確認する。<br>
  「y」または「n」を入力すると実行される。<br>
  -v コピーしたときに詳細を表示する。<br>
  -u 元のファイルが新しいときにのみコピーする。<br>
  -b 上書きされるファイルのバックアップを作成する

---

### 参考にしたサイト

- [https://eng-entrance.com/linux-command-mkdir]
- [https://uxmilk.jp/8318]
- [https://eng-entrance.com/linux-command-rmdir]
- [https://eng-entrance.com/linux-command-touch]
- [https://apidog.com/jp/blog/linux-file-management-mv-cp-rm-commands/]
