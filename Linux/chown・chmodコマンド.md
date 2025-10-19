# 【Linux】chown・chmod コマンド

Linux でアクセス権の変更に使うコマンドについてまとめました。
<br><br>

所有者(ユーザー)とグループの確認方法 →ls コマンド

# chown コマンド

###### <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイルの所有者を変更する</span>

```bash

$  chown user01 work01
```

`chown［オプション］[ユーザー名][:グループ名] [ファイル名またはディレクトリ]`

- 「change owner」という意味。
- work01 ファイルの所有者が user01 に変更された。

- 所有者と所有グループを変更するには、<br>
  $chown user01:group02 work01
- 所有グループを変更するのは、<br>
  $chown :group02 work01 または**chgrp ** group02 work01

- 一般ユーザーではユーザーやグループを変更できないため、  
  <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">sudo コマンドを使って root 権限で実行</span>する。

- **よく使うオプション**  
  -c 変更があった場合にメッセージを表示する。 <br>
  -v コマンドの実行状況を表示する。 <br>
  -R 指定したディレクトリと中身すべての所有者を変更する <br>

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
  -v コマンドの実行状況を表示する。 <br>
  -R 指定したディレクトリと中身すべてのアクセス権を変更する <br>

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎パーミッション設定☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">
[f:id:Greenpenguin:20250223092202p:plain]

<br>
☀︎パーミッションの指定方法は２通りある。<br>
①ユーザー種別ごとのパーミッション書式をカンマで区切って指定（例：g+w,o+w）<br>
②８進数３桁でまとめて指定（例：755）<br>
<br>
☀︎対象者<br>
「u」・・・所有ユーザーroot<br>
「g」・・・所有グループ<br>
「o」・・・その他のユーザー<br>
・全てに同じ権限付与のときはa と指定できる。
<br>
☀︎権限<br>
「r 」・・・ 読みとり：4<br>
「w」・・・書き込み：2<br>
「x 」・・・実行またはディレクトリの変更：1<br> 
<br>
☀︎動作<br>
「=」・・・設定する<br>
「+」・・・追加する<br>
「-」・・・取り消しする<br>

</div>
