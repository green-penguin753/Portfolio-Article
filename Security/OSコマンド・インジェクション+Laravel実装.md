# 【Security】OS コマンド・インジェクション+Laravel 実装

# 概要

脆弱性のある Web アプリケーションの入力領域(入力フォーム等)に、  
攻撃者が<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">悪意のある OS コマンドを紛れ込ませ、Web サーバー上で不正に実行する</span>攻撃手法。

###### 発生しうる脅威

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">重要情報の漏洩</span>  
  サーバーに格納されている重要な情報が盗まれる。企業の信頼を大きく損なうことにもつながる。

- ファイルの改ざん  
  ファイルの書き換え、作成、削除などをされることにより、サービスの信頼性が損なわれる。

- 不正なシステム操作  
  意図しない OS のシャットダウンやユーザーアカウントの追加や削除をされる。

- 不正なプログラム(マルウェア)への感染  
  ウイルスの感染やバックドア、ランサムウェアなどにつながる。
- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">攻撃の踏み台にされる</span>  
  サーバー自体を乗っ取られ、他サイトへ大量のリクエストを送信するなど、さまざまな攻撃に悪用される。

<br>

```
/opt/myapp/bin/add_user $data
↓
/opt/myapp/bin/add_user yamada; rm -rf /
```

☀︎$data に「yamada; rm -rf /」と入力されることで、  
「add_user yamada;」コマンドを実行した後、「rm -rf /」でルート以下のディレクトリ(システム全体)の強制削除ができ、壊滅的な被害が発生する。

- ls、cat、rm、chmod、mv、echo コマンドなどファイル操作系や、ファイルのダウンロード機能を持つ curl コマンドにも悪用できる。「cat /etc/passwd」でパスワード閲覧できる。

# 原因

ユーザーからの入力を<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">そのまま OS コマンドに受け渡す</span>実装。

- 外部プログラムを呼び出し可能な関数を使っている。
- ユーザーが入力した内容をチェックしていない。

# 対策

### 根本的対策

###### １.<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">OS コマンド(シェル)を実行する機能を持つ関数の利用を避ける</span>

そもそも関数が OS コマンドを直接実行する機能を持っていなければ、攻撃は成立しない。

ファイルの名称を変更したいときは、  
exec()ではなく OS コマンドを実行しない rename()など代替の関数を利用する。

### 保険的対策

どうしても OS コマンドを実行する機能を持つ関数を利用したい場合

###### ２.その引数を構成する全ての変数に対してチェックを行い、あらかじめ許可した処理のみ実行する

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">**バリデーション処理**</span>を使う  
  ホワイトリスト方式とはその引数に許可する文字の組み合わせを決めておき、それ以外は許可しない方式。  
  数字以外を入力することのない引数であれば、「数字のみからなる文字列であること」をチェックする。

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">**エスケープ処理**</span>をする  
  escapeshellarg()などを使って特別な意味を持つ文字を変換し、無害化(サニタイジング)する。

###### ３.WAF(Web Application Firewall)の導入

OS コマンド・インジェクションを含むさまざまな攻撃を検知して自動的にブロックする。  
しかし誤検知（False Positive）のリスクがあり、また多重エンコードなど検知の隙間を突いた攻撃や未知の攻撃手法に対しては完全に防げないため、他のセキュリティ対策も合わせて実施する。

###### ４.定期的な脆弱性診断の実施

Web アプリケーションの脆弱性を早期に発見・修正する。

```php
# 脆弱性が含まれているコード
exec("rename " . $oldFileName . " " . $newFileName);

// １.代替の関数を使う方法
rename($oldFileName , $newFileName);

// ２.エスケープ処理を使う方法
exec("rename " . escapeshellarg($oldFileName). " " . escapeshellarg($newFileName));

```

# Laravel での実装例

### 1.Storage ファサードなど直接実行しない関数を使う

Laravel では、Storage ファサードを使うとファイル操作を OS コマンドなしで実行できる。

```php
Storage::move($oldFileName , $newFileName);
```

☀︎ ファイル名を変更できる。

---

### 2.バリデーションとエスケープ処理をする

どうしても OS コマンドを実行する機能を持つ関数を利用したいときは、

- **バリデーション処理(<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">validate 関数</span>)**

PostController.php ファイルで

```php
public function store (Request $request) {
	$validated = $request->validate([
		'title' => 'required|max:20',
		'body' => 'required|max:400',
	]);
}
```

☀︎ タイトルが 20 文字以下、本文が 400 文字以下であることを確認し、  
指定する値以外はエラーとなり通過できないようにする。  
 required 属性で必須入力として、空欄であってもエラーとなる。

- **エスケープ処理(<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">escapeshellarg 関数</span>)**

escapeshellarg()は、  
引数の特殊文字などを安全な文字列として自動的に変換してくれる PHP の関数。

---

### 参考にしたサイト

- 安全なウェブサイトの作り方 改定第 7 版
- https://www.qbook.jp/column/1897.html
- https://www.gmo.jp/security/cybersecurity/cyberattack/blog/os-command-injection/
- https://aisinkakura-datascientist.hatenablog.com/entry/2023/02/23/215205
