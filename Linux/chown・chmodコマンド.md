# 【Linux】chown・chmod コマンド

Linux でアクセス権の変更に使うコマンドについてまとめました。


所有者(ユーザー)とグループの確認方法 →ls コマンド

# chown コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルの所有者を変更する</span>

```bash

$  chown user01 work01
```

`chown［オプション］[ユーザー名][:グループ名] [ファイル名またはディレクトリ]`

- 「change owner」という意味。
- work01 ファイルの所有者が user01 に変更された。

- 所有者と所有グループを変更するには、
  $chown user01:group02 work01
- 所有グループを変更するのは、
  $chown :group02 work01 または**chgrp ** group02 work01

- 一般ユーザーではユーザーやグループを変更できないため、  
  <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">sudo コマンドを使って root 権限で実行</span>する。

- **よく使うオプション**  
  -c 変更があった場合にメッセージを表示する。 
  -v コマンドの実行状況を表示する。 
  -R 指定したディレクトリと中身すべての所有者を変更する 

# chmod コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルのアクセス権を変更する</span>

```bash

$  chmod g+w work01
```

`chmod パーミッション  [ファイル名]`

- 「change mode」という意味。
- work01 ファイルに所有グループの書き込み権限が追加された。
- 自分の所有するファイルであれば、sudo コマンドは使わず実行できる。

- **よく使うオプション**  
  -v コマンドの実行状況を表示する。 
  -R 指定したディレクトリと中身すべてのアクセス権を変更する 

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎パーミッション設定☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">



☀︎パーミッションの指定方法は２通りある。
①ユーザー種別ごとのパーミッション書式をカンマで区切って指定（例：g+w,o+w）
②８進数３桁でまとめて指定（例：755）

☀︎対象者
「u」・・・所有ユーザーroot
「g」・・・所有グループ
「o」・・・その他のユーザー
・全てに同じ権限付与のときはa と指定できる。

☀︎権限
「r 」・・・ 読みとり：4
「w」・・・書き込み：2
「x 」・・・実行またはディレクトリの変更：1 

☀︎動作
「=」・・・設定する
「+」・・・追加する
「-」・・・取り消しする

</div>
