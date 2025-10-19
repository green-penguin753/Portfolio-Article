【Security】バッファオーバーフロー+Laravel 実装

# 概要

ユーザーの入力領域に  
攻撃者が悪意あるコードを含んだ大量のデータを送信してバッファを溢れさせる。  
<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">リターンアドレスが悪意のあるコードで上書き</span>され、処理されることにより
システムに異常動作を発生させる攻撃手法。

「バッファ」・・・プログラムが一時的にデータを保存するためのメモリ領域  
「リターンアドレス」・・・関数処理後に実行するべきプログラムの位置情報

<br>

###### 発生しうる脅威

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">プログラムの異常終了</span>  
  意図しないシステム停止により多額の損害賠償や企業の信頼を大きく損なうことにもつながる。

- 重要情報の漏洩やサイトの改ざん

- 遠隔操作が可能となる悪質なコードを送られ、管理者権限を奪われる。

- 攻撃の踏み台にされる  
  DDoS 攻撃などに悪用される

# 原因

ミスによる不適切なメモリ管理

- 入力値の長さをチェックしてから使っていない
- 入力値のバリデーション不足

# 対策

### 根本的解決

###### １.<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">直接メモリ操作ができない言語で記述する</span>

PHP、Perl、Java など、メモリ管理を自動で行ってくれる言語を使う。

###### ２.直接メモリ操作ができる言語で記述する部分を最小限にする

C、C++、アセンブラなどの言語のときは、その部分をできるだけ少なくして集中的にチェックをする。

###### ３.脆弱性が修正されたバージョンを使用する

最新のバージョンのライブラリを使用する。

# Laravel での実装例

### 1.ほぼ発生しない

Laravel では PHP を使っており、メモリ管理を自動で行っている言語のため。

### 2.入力値のバリデーション

ユーザー入力には必ずバリデーションをかけておく。

```php
$validated = $request->validate([
    'name' => 'required|string|max:255',
]);
```

☀︎255 文字以下の文字列のみ通過できる。

---

### 参考にしたサイト

- 安全なウェブサイトの作り方　改定第 7 版
- https://www.nttpc.co.jp/column/security/bof.html.
- https://www.lanscope.jp/blogs/cyber_attack_pfs_blog/20240130_18380/
- https://cybersecurity-jp.com/column/18488
- https://zenn.dev/kei_dev/articles/09ac185edcbb96
