# 【Security】HTTP ヘッダ・インジェクション+Laravel 実装

# 概要

ユーザーからの入力値の処理に脆弱性があると、  
攻撃者が<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">HTTP リクエストに罠を仕掛けてレスポンスを生成</span>し、  
ユーザーに偽の URL をクリックさせ、スクリプトを実行させたり情報を盗み取る攻撃。

改行コードが原因となることから「CRLF インジェクション」とも呼ぶ。

複数のレスポンスを作り出す攻撃を  
「HTTP レスポンス分割（HTTP Response Splitting） 攻撃」と呼ぶ。

<br>

###### 発生しうる脅威

- XSS 攻撃と同じ

  - <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">重要情報の漏洩</span>
  - Cookie 情報の漏洩
  - ブラウザに任意の Cookie を保存させられる
  - 偽情報の流布による混乱

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">キャッシュサーバのキャッシュ汚染</span>  
  HTTP レスポンス分割攻撃で、  
  悪意あるレスポンスをキャッシュサーバに保存されると、
  他のユーザーも偽ページや不正スクリプトを閲覧し続けてしまう。

# 原因

入力値のバリデーション不足

# 対策

ユーザーから入力される値から、空白コードや改行コードを削除する。

### 根本的解決

###### １.<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">ヘッダーの出力用 API を使う</span>

HTTP レスポンスヘッダーをプログラムで直接出力せず、  
実行環境や言語に用意されているヘッダ出力用の API を使う。

HTTP ヘッダの構造は複雑なため、実行環境によっては修正パッチや追加の対策も検討する。

###### ２.改行をできないように処理する

API を使えないときは、

- 改行の後に空白を入れることで継続行として処理する方法
- 改行コード以降の文字を削除する方法
- 改行が含まれていたら Web ページ生成の処理を中止する方法

### 保険的対策

###### ３.ユーザー入力から改行コードを削除する

ユーザーが入力した全ての値から改行コード（\r, \n など）や制御文字を削除する。

しかし、テキストエリアの入力データなど改行を含むかもしれない文字列からも、改行が削除されてしまう。

# Laravel での実装例

### 1. <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">Laravel の標準レスポンスを使う</span>

HTTP ヘッダの改行コードを自動で除去してくれる。

```php
return  response()->redirectTo($url);
```

☀︎response()は、改行文字（\r, \n）を自動的に削除する。  
☀︎redirectTo()は、リダイレクト先を動的に設定できる。

### 2.外部パラメータは必ずバリデーション処理

どうしても Location ヘッダに外部パラメータやユーザー入力を使用する場合は、  
URL 形式やスキームなどを必ずチェックする。

### 3.TrustHosts ミドルウェアを使う

Laravel の TrustHosts ミドルウェアを使って許可するホスト名(ドメイン)を指定しておき、  
それ以外の Host ヘッダーのリクエストを拒否する。

---

### 参考にしたサイト

- 安全な Web サイトの作り方 改定第 7 版
- https://mbp-japan.com/tokyo/itlaboj/column/5111664/
- https://office110.jp/security/knowledge/cyber-attack/http-header-injection-attack
- https://note.com/ipa713/n/n8dc3391793a6
- https://blog.dododori.com/create/program/laravel-host-header/
