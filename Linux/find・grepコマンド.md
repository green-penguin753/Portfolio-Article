# 【Linux】find・grep コマンド

Linux で検索に使うコマンドについてまとめました。

# find コマンド

###### ファイルがどこのディレクトリにあるか検索する

`find［検索ディレクトリ］［オプション］［条件式］［アクション］`

- **検索ディレクトリの指定** 
  $ find ~ ・・・ホームディレクトリを検索
  $ find . ・・・カレントディレクトリを検索
  $ find / ・・・ルートディレクトリを検索

- **よく使うオプション**

#### 検索の深さを制限する

- mindepth オプション・・・どの深さから探すか（最小）
- maxdepth オプション・・・どこまでの深さまでで探すか（最大）

```bash
$ find /var/log -maxdepth 1 -name "*.log"
```

- /var/log ディレクトリの直下にある.log で終わるファイルを探して表示すると言う意味。
- mindepth と maxdepth を組み合わせて使うと、検索範囲を制限できる。

#### <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">名前から検索</span>

-name オプション

```bash
$ find /etc -name "config.conf"
```

- /etc ディレクトリ内で”config.conf”ファイルを探すと言う意味。
- -name は完全に一致するファイル名を検索するが、  
  -iname は大文字と小文字を区別せずに検索する。
- $ find /etc -name "\*.conf" なら、.conf で終わるファイルを検索する。
- $ find /etc -name "\*php\*" なら、php を含むファイルを検索する。

#### <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">ファイルタイプから検索</span>

-type オプション

```bash
$ find . -type f
```

- カレントディレクトリ内でファイルのみを探すと言う意味。
- type の値
  - f：通常のファイル
  - d：ディレクトリ
  - l：シンボリックファイル

#### ファイルサイズから検索

-size オプション

```bash
$ find /etc -size +1G
```

- /etc ディレクトリ内で 1GB 以上のファイルを探すと言う意味。
- ディスク容量を圧迫している大きなファイルを見つけたいときなどに使う。
- size の単位
  - k：キロバイト（KB）
  - M：メガバイト（MB）
  - G：ギガバイト（GB）

#### 日時から検索

- mtime オプション・・・最終更新日を基準にする
- atime オプション・・・最終アクセス日を基準にする

```bash
$ find /etc -mtime -7
$ find /etc -atime +30
```

- 1 行目は、/etc ディレクトリ内で過去 7 日以内に更新されたファイルを探すと言う意味。
- 2 行目は、/etc ディレクトリ内で 30 日以上アクセスされていないファイルを探すと言う意味。
- 最近更新されたファイルを確認したいときなどに使う。

#### パーミッションから検索

-perm オプション

```bash
$ find /etc -perm 755
```

- /etc ディレクトリ内で 755 のパーミッションを持つファイルを探すと言う意味。

#### ユーザーやグループから検索

-user / -group オプション

```bash
$ find /etc -user username
```

- /etc ディレクトリ内で特定のユーザーが管理しているファイルを探すと言う意味。



- **条件式**  
  名前、種類、サイズ、更新時間、パーミッションなど。  
  検索に使用する条件を指定できる。

- **アクション**  
  検索結果に対して何を行うのかを指定する。表示、削除、移動など。
  - -print・・・表示する。よく使う。省略できる。
  - -ls・・・詳細情報も表示する。
  - -exec コマンド・・・検索結果に指定したコマンドを実行する。

# grep コマンド

###### ファイル内容の文字列を検索する

```bash
$ grep -i "Error" logfile.txt
```

`$ grep [オプション] 検索キーワード ［ファイル名］`

- 検索条件は文字列か正規表記で検索する。
- 「Global Regular Expression Print」の略。  
  ファイル全体から・正規表現で・表示するという意味。

- **よく使うオプション**.  
  -n 行番号つけて表示する。
  -i 大文字と小文字を区別せずに検索する。
  -e 複数の検索文字列を検索できる。
  -v 検索キーワードに一致しない行を表示する。
  -r ディレクトリ内も再帰的に検索する。

---

### 参考にしたサイト

- https://linuc.spa-miz.com/2021/01/05/exhaust-find-command/
- https://www.infra-manual.com/findcommand-details/
- https://eng-entrance.com/linux-command-grep
- https://blog.qbist.co.jp/?p=1919
