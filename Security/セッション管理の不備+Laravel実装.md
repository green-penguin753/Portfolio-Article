# 【Security】セッション管理の不備+Laravel 実装

# 概要

Web システムでは、  
Cookie やセッション ID を使いアクセスしてきたユーザーがログイン済みかどうかを判定している。

攻撃者に<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">Cookie の中身やセッション ID を知られてしまう</span>と、  
ユーザー ID やパスワードを知らなくてもログイン済みのユーザーとして、  
<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">許可されている操作を不正に実行</span>される攻撃。

<br>

- セッション管理の不備を狙う攻撃手法は２種類ある。

  - **セッションハイジャック**  
    利用者のセッション ID を<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">推測・盗用</span>によって不正に取得する。

  - **セッション ID の<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">固定化</span>**(Session Fixation)  
    攻撃者が事前に用意したセッション ID をユーザーに使わせ、 ユーザーがログインした後、そのセッション ID を使ってなりすます。

<br>

###### 発生しうる脅威

攻撃が成功した場合は、  
攻撃者はユーザーに<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">なりすまし</span>、ユーザーに許可されている操作を不正に実行できる。

- 個人情報の漏洩

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">金銭的被害</span>  
  不正送金やクレジットカードの不正利用、EC サイトで意図しない商品購入など
- 登録情報の漏洩・改ざん  
  アカウント情報など各種設定の変更や退会処理、掲示板への不適切な書き込みなど

# 原因

セッション ID の管理の不備

- セッション ID の生成方法が単純(推測)
- 通信を暗号化していない(盗聴)
- ログイン後、新しいセッションで管理していない(固定化)

# 対策

### 根本的対策

###### １.<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">推測困難なセッション ID を生成する</span>(推測)

- セッション ID を連番や時刻情報など単純なアルゴリズムで生成すると、推測や総当たり攻撃(ブルートフォース)で簡単に予測されてしまう。
- 暗号論的疑似乱数生成機などを使って、長くランダムなセッション ID を生成する。

###### ２.セッション ID を URL パラメータに格納しない(盗聴)

- ユーザーが他のサイトに遷移したとき、Referer 送信機能によりセッション ID の含まれた URL が送信されてしまい、攻撃者に URL を入手されると悪用される。
- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">セッション I D は、Cookie</span> もしくは POST メソッドの hidden パラメータに格納して受け渡しをする。

###### ３.HTTPS 通信での Cookie には<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">必ず secure 属性</span>を付与する。(盗聴)

- secure 属性により HTTPS 通信でのみ送信されるようになる。

###### ４.ログイン後に新しいセッション ID を発行する(固定化)

- ログイン後に新しいセッションを発行し、古いセッション ID は無効化する。

###### ５.ログイン成功後に、秘密情報を作成して確認する(盗用)

- ログイン成功したときに秘密情報を生成し、Cookie に格納する。
- サーバー側に保持している秘密情報と Cookie の秘密情報が一致することをリクエストごとに確認する。

### 保険的対策

###### ６.セッション ID を固定値にしない(固定化)

- セッション ID はユーザーのログインごとに新しく発行する。

###### ７.Cookie の<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">有効期限を設定</span>する(盗聴・固定化)

- セッション ID を含む Cookie の有効期限は必要最小限の期間に設定する。
- 有効期限の設定(expires 属性)を省略することで、ブラウザを閉じると自動的にセッションは破棄される。

# Laravel での実装例

### 1.設定ファイルで secure 属性を付与する

セッションを設定する`config/session.php`ファイルで

```php
return [
 'secure' => env('SESSION_SECURE_COOKIE', true), //secure属性付与

 'http_only' => true,           // JavaScript経由ではアクセス不可
 'lifetime' => 120,             // Cookie(Session)の有効期限(分)
 'expire_on_close' => true,     // ブラウザ終了で破棄
];

```

☀︎env 関数で secure を設定する。

- 第 2 引数はデフォルト値で.env ファイルがない場合に適用される。

`.env`ファイルで

```
SESSION_SECURE_COOKIE=true
```

☀︎secure は true となる。

### 2.デフォルトでセッション管理機能が搭載

- セッション ID を URL パラメータに格納せず Cookie で管理する。
- 推測困難なセッション ID を自動で生成する。

### 3.標準認証機能の Auth を使ってログインする

- ログイン成功したときに自動的にセッション ID が再生成される。

```php
if (Auth::attempt($credentials)) {
    $request->session()->regenerate(); // セッションを再生成

    return redirect()->intended('dashboard'); //マイページへ
}
```

- ログアウトのときは自動的にセッションが破棄される。

```
Auth::logout();

$request->session()->invalidate(); // セッションを無効化

$request->session()->regenerateToken();　// CSRFトークンを再生成

return redirect('/'); //トップページへ
```

---

### 参考にしたサイト

- 安全なウェブサイトの作り方 改定第 7 版
- https://www.lanscope.jp/blogs/cyber_attack_pfs_blog/20231225_17585/
- https://qiita.com/yutaka_pg/items/f0103c3171b75146c28a
- https://taraoblog.com/laravel-session/.
