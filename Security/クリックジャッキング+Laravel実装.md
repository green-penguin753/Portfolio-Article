# 【Security】クリックジャッキング+Laravel 実装

# 概要

正規サイトにログインした状態で、  
攻撃者が罠サイトにユーザーを誘導しiframe や透明なレイヤーを使ってリンクやボタンを重ねて配置し、ユーザーに意図しない操作をさせる攻撃手法。

ユーザーが一見無害に見えるサイトのボタンをクリックすると、  
実際には背後にある iframe 内のボタンをクリックさせられている。

###### 発生しうる脅威

- 金銭的被害 
  不正送金やクレジットカードの不正利用、EC サイトで意図しない商品購入など

- 登録情報の漏洩・改ざん  
  利用者情報の公開範囲の変更や退会処理

- SNS やサービスの不正利用  
  SNS での「いいね」やフォロー、投稿などの不正操作をさせられ、情報拡散やアカウントの悪用

- プライバシー侵害  
  カメラやマイクへのアクセス許可をユーザーに気づかれずに ON にさせる

# 原因

- ログイン後の重要な操作や設定を、クリック操作のみで実行可能にしている仕様

- iframe で埋め込めるページに、重要な操作の処理ができる機能の実装

# 対策

### 根本的解決

###### １.frame や iframe によるページの読み込みを制限する

HTTP レスポンスヘッダに`X-Frame-Options: DENY`(または`SAMEORIGIN`)と設定すると、  
X-Frame-Option に対応したブラウザでは、frame 要素や iframe 要素によるページの埋め込みができなくなる。  
IE7 など対応していないブラウザもあるため、CSP とあわせて対策するといい。

☀︎X-Frame-Optionsヘッダの設定値☀︎

DENY 　　　　・・・すべてのウェブページでフレーム内の表示を禁止
SAMEORIGIN ・・・同一オリジンのときのみ表示を許可する
ALLOW-FROM・・・指定したオリジンのみ表示を許可する

☀︎オリジンとは、
URLのスキーム、ホストドメイン、ポート番号が同じ組み合わせのこと


###### ２.処理の直前に再度パスワードを入力させる

重要な操作の直前のページでユーザーに再度パスワードを入力させ、 そのパスワードが正しい場合のみ処理をする。  
ただし画面設計の仕様変更が必要となる。

### 保険的対策

###### ３.重要な処理はクリックのみで実行できないような仕様にする

ユーザーに複雑な操作をさせることは難しいため、  
重要な操作にキーボード操作や複数の確認ステップを挟む仕様にすることで、攻撃の成功率を下げることができる。

# Lalavel での実装例

### 1.自作ミドルウェアで X-Frame-Options を追加する

レスポンスヘッダに X-Frame-Options オプションを指定する。

AddXFrameOptions.php ファイルに

```php
class AddXFrameOptions　//AddXFrameOptionsクラスを作成
{
  public function handle($request, Closure $next)
  {
    $response = $next($request);
    $response->headers->set('X-Frame-Options', 'deny'); //すべてのウェブページでフレーム内の表示を禁止
      return $response;
    }
}
```

☀︎ 全リクエスト(全ページ)でフレーム内の表示が禁止になる。

---

### 参考にしたサイト

- https://www.hammock.jp/assetview/media/clickjacking-countermeasures.html
- https://qiita.com/mejileben/items/39d897757d5c3a904721
- https://qiita.com/teru0x1/items/c622fa814809061bfcad
