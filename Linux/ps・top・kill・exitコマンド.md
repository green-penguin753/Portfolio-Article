# 【Linux】ps・top・kill・exit コマンド

Linux で実行中のプロセス(アプリケーション)に使うコマンドについてまとめました。

# ps コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">動作しているプロセスを確認する</span>

```bash

$ ps
```

`ps［オプション］`

- 「process status」という意味。
- 現在ユーザーが起動しているプロセスのみ表示する。
- **プロセス ID（PID）**とは、  
  各プロセスごとに割り当てられる管理用の番号（４桁の数字）のこと。

- **よく使うオプション**  
  -a 他の端末を含めた制御端末のある、すべてのプロセスを表示する。  
  -u CPU、メモリ使用率、実行ユーザー名なども表示する。  
  -x バックグラウンドで動作しているプロセスも含めて表示する。デーモンプロセスなど。  
  -f ツリー形式で表示する。pstree コマンド の方が表示が見やすい。

- 制御端末のないバックグラウンドで動作しているプロセスは、  
  $ps x を実行すると、TTY の列の項目が「?」になっている。

# top コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">プロセスの状態を確認する</span>

```bash

$ top
```

`top［オプション］`

- 「table of processes」という意味。
- 実行中のプロセスの情報をリアルタイムに更新(スペースキー)して表示する。
- 終了には「q キー」を入力する。

- **よく使うオプション** <br>
  -n 実行する回数を指定する。<br>
  $ top -n 3 なら、3 回実行した後に自動で終了する。  
  -u 特定のユーザーのプロセスのみ表示する。<br>
  $ top -u root なら、root ユーザーのプロセスのみ表示する。
  <br>
  -d 指定した間隔で更新する。<br>
  $ top -d 5 なら、5 秒間隔で更新する。

# kill コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">シグナルを送信してプロセスを制御する</span>

```bash

$ kill 22385
```

`kill［オプション］プロセスID`

- プロセスにシグナルを送信する方法は２通りある。<br>
  ① 端末でキーを入力する。Ctrl+c や Ctrl+z など。<br>
  ②kill コマンドを入力する。<br>

- **よく使うオプション**  
  -l 利用できるシグナルの一覧を表示する<br> -シグナル番号

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎代表的なシグナル番号☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">

「1」・・・HUP (SIGHUP)端末が制御不能もしくは切断による終了<br>
「2」・・・INT (SIGINT)キーボードからの割り込み。Ctrl+C と同じ<br>
「9」・・・KILL (SIGKILL)強制終了<br>
「15」・・・TERM (SIGTERM)デフォルトの終了<br>
「18」・・・CONT (SIGCONT)プロセスの再開<br>
「19」・・・STOP (SIGSTOP)一時停止
<br>

</div>

- オプションでシグナルを指定しないときは、15 番の TERM が送信される。
- 制御できなくなったプロセスを強制的に終了するときは、 9 番の KILL を送信する。

# exit コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ログアウトする</span>

```bash

$ exit
```

`exit [オプション] [終了コード]`

- ショートカットキーでは、Ctrl+D
- ログインは su コマンド。
- 終了コードは 0~255 の範囲で任意でつけることができる。<br>
  一般的に「０」は正常終了、「1」はエラー終了を表す。

---

### 参考にしたサイト

- [https://eng-entrance.com/linux-command-ps]
- [https://www.sejuku.net/blog/50251]
- [https://eng-entrance.com/linux-command-exit]
