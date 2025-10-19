# 【Security】アクセス制御や認可制御の欠落+Laravel 実装

# 概要

アクセス制御や認可制御の欠落とは、  
<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">認証や認可が不十分</span>なために、攻撃者やユーザーが本来アクセスできないページに入り、情報を閲覧したり操作できてしまう状態のこと。

ログインできた(認証)後、ユーザーを識別して適切な権限を与える(認可)。  
認証・認可を組み合わせて対策をする。

###### 認証と認可の違い

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">**認証**(Authentication)</span>とは

  - ユーザーが本人であるかを確認する仕組み  
    (パスワード認証、指紋認証、多要素認証(MFA)など)
  - 「アクセス制御の欠落」・・・認証(ログイン)しなくてもアクセスできてしまう状態。直接 URL を指定すると誰でもログインした後のページに入れるなど。

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">**認可**(Authorization)</span>とは
  - 認証済みのユーザーに、なにをどこまで許可するかの権限を付与する。  
    (ファイルの閲覧や端末の制限など)
  - 「認可制御の欠落」・・・本来許可されていないページにアクセスできてしまう状態。他人のデータを閲覧・編集できてしまうなど。

<br>

##### 発生しうる脅威

**アクセス制御の欠落による脅威**

- 情報漏洩、不正操作、データ改ざん
- 本来権限を持たないユーザーによる不正ログイン
- 認証を経ずに直接 URL を指定することで、誰でもログイン後のページにアクセスできる

**認可制御の欠落による脅威**

- 他人の情報を参照・操作(クエリパラメータ改ざんによる IDOR)
- 低権限ユーザーが本来できない操作を実行できる(権限昇格)

☀︎IDOR（Insecure Direct Object Reference）とは、  
ユーザー ID などを URL に直接指定することで、他人のリソースにアクセスできてしまう脆弱性のこと。

# 原因

認証・認可の実装や設計の不足

# 対策

### 根本的解決

###### １.ユーザー入力値のバリデーションは<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">必ずサーバー側</span>で行う。

クライアント側だけでなく、サーバー側で厳格にバリデーションして不正なデータや攻撃を防ぐ

###### ２.認証にパスワードなどの入力を必要とする

メールアドレスなど公開されやすい情報だけではなく、秘密情報を使って本人確認をする。

###### ３.利用者 ID を URL や POST パラメータに埋め込まない

他のユーザーに ID を推測されるため、ID を推測困難な値にする。  
サーバー側で「そのユーザーがそのリソースにアクセスする権限があるか」を必ず認可チェックする。

###### ４.メニューの表示/非表示だけで制御しない

クライアント側の画面上でメニューを非表示にしても、URL やパラメータを知っていれば権限がなくても操作できてしまう。  
サーバー側での認可チェックが必須。

# Laravel 実装例

### 1.**Laravel Breeze などの**パッケージ**を使う**(認証)

Laravel が提供しているパッケージ使って、  
ユーザー登録やログイン、パスワードリセットなどの機能を設定する。

```php
composer require laravel/breeze --dev
php artisan breeze:install
npm install && npm run dev
php artisan migrate
```

### 2.パスワードを暗号化する(認証)

Laravel ではデフォルトでパスワードを暗号化し、ハッシュ化して保存する。

```php

//パスワードを暗号化してDBに保存
$password = Hash::make('your-password')　

//ログイン時にハッシュファザードで認証
if (Hash::check('your-password', $storedPassword)) {　
　// パスワードが一致しているときの処理
}
```

### 3.ポリシーやゲートを使う(認可)

ポリシー(Policy)で、  
そのユーザーがそのリソースにアクセスできる権限を持っているか確認する。

モデルのファイルでポリシーを定義する

```php
public function update(User $user, Post $post) {
　　// ユーザーが投稿のオーナーなら編集可能とする処理
   return $user->id === $post->user_id;
}
```

コントローラーのファイルでポリシーを使用する

```php
class PostController extends Controller
{
$this->authorize('update', $post);
}
```

- ゲート(Gate)は、シンプルな認可制御。管理者ページではない個人のページへの権限を確認する。
- ポリシーやゲートで認可したあと、authorize メソッドで判定(認可確認)をする。

---

### 参考にしたサイト

- https://solution.kamome-e.com/blog/archive/blog-security-20211021/
- https://blog.flatt.tech/entry/authorization_control_security.
- https://zenn.dev/kei_dev/articles/09ac185edcbb96
