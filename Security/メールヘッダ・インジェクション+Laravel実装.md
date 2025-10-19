# 【Security】メールヘッダ・インジェクション+Laravel 実装

# 概要

メール送信機能を持つ Web アプリケーションで出力処理に脆弱性があると、  
攻撃者が<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">メールのヘッダ情報に不正なデータを差し込む</span>ことで、不正な操作を実行する攻撃手法。

- お問い合わせページやアンケートなどのサイトで特に注意が必要。

<br>

###### 発生しうる脅威

- 攻撃の踏み台として<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">迷惑メールの送信に悪用</span>される
- メールの内容の改ざん

```mail
//脆弱性のあるコード
To: info@□□.□□
From: $email
Subject: お問い合わせ
Content-Type: text/plain: charset="ISO-2022-JP"

本文

//Fromの$emailに差し込む
support@△△.△△%0d%0aBcc%3a%20○○○○@○○.○○

↓
//生成されるメール
To:＜info@□□.□□＞
From:＜support@△△.△△＞
Bcc:＜○○○○@○○.○○＞
Subject: お問い合わせ

本文

```

☀︎BCC を追加されて、○○○○@○○.○○ にも送信される。  
「%0d%0a」は改行コード、「%3a」はコロン、「%20」は空白

- メール文の終わりを示すヌル「％00」を使って、以降の文を削除もできる。

# 原因

メールヘッダ出力の実装

# 対策

### 根本的解決

###### １.<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">メールヘッダを固定値にする</span>

メールヘッダにユーザーからの入力された値をそのまま使わない実装をする。

###### ２.メールヘッダーの出力用 API を使う

メールヘッダを固定値にできないときは、
実行環境や言語に用意されているメール送信用の API を使う。  
(PHPMailer、SendGrid、Mailgun など)

###### ３.HTML で宛先を指定しない(禁忌)

宛先のメールアドレスを HTML の hidden パラメータなどで指定しない。

### 保険的対策

###### ４.ユーザー入力から改行コードを削除する

ユーザーが入力した値から改行コード（\r, \n など）や制御文字の削除や含まれていたら処理を中止させる。

全ての入力値から改行コードを削除してしまうとメール本文の改行からも削除され、  
エラーの原因となるため用途に応じて適切な処理を行う。

# Laravel での実装例

### 1.Laravel の標準メール送信機能を使う

Mail ファザード(Mail::to)または、Mailable クラス(extends Mailable)を使う。

```php
Mail::to($request->input('email'))->send(new ContactFormMail($data));
```

☀︎ メールヘッダの改行コードが自動的に除去される。

### エスケープ処理

```php
// メールアドレスのサニタイズ
$email = filter_var($request->input('email'), FILTER_SANITIZE_EMAIL);
// 件名の改行コードの除去
$subject = str_replace(["\r", "\n", "%0A", "%0D"], "", $request->input('subject')
```

☀︎PHP 関数の filter_var()や str_replace()で改行コードを除去している。

### バリデーション処理

To, Cc, Subject, From などにユーザー入力を使うときは必ずバリデーションをする

---

### 参考にしたサイト

- [安全なウェブサイトの作り方 改定第 7 版](https://www.ipa.go.jp/security/vuln/websecurity/ug65p900000196e2-att/000017316.pdf)
- https://www.lanscope.jp/blogs/cyber_attack_pfs_blog/20250130_24713/
- https://shukapin.com/security/mail-header-injection
- https://zenn.dev/kei_dev/articles/09ac185edcbb96
