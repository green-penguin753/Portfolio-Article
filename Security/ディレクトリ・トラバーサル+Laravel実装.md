# 【Security】ディレクトリ・トラバーサル+Laravel 実装

# 概要

**ディレクトリ・トラバーサル攻撃**とは、  
外部からのパラメータをファイル名として直接指定している Web アプリケーションで、  
攻撃者が<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">相対パスを使ってファイル名を指定し、非公開ファイルへアクセスする</span>攻撃手法。

<br>

###### 発生しうる脅威

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">重要情報の漏洩</span>
  サーバーに格納されている重要な情報が盗まれる。企業の信頼を大きく損なうことにもつながる。

- サーバー内ファイルの改ざん、削除  
  ファイルやプログラムのソースコードの書き換え、作成、削除などをされ、サービスの信頼性が損なわれる。

<br>

```php
$file = '/var/app/files/' . $data;
↓
$file = '/var/app/files/' . ../../../etc/passwd;
```

☀︎$data に「../../../etc/passwd」と入力されることで、
上位ディレクトリに存在する「etc/passwd」ファイルを閲覧でき、パスワード情報などが盗まれる。

# 原因

ユーザーからの入力を<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">そのままファイル名に指定する</span>実装。

- 任意のディレクトリ名やファイル名を指定できる状態になっている。
- サーバー内にあるファイルへのアクセス権限を正しく管理していない。
- ユーザーが入力した内容をチェックしていない。(パス名パラメーターの未チェック)

# 対策

### 根本的対策

###### １.<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ファイル名を直接指定する実装自体を避ける</span>

仕様や設計から見直す。

###### ２.固定のディレクトリを指定&ファイル名にディレクトリ名を含まないように実装する<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">(basename 関数)</span>

```php
$dirname = '/var/app/files/';
$filename = '$_GET['filename']';
//ファイルを開く処理

fopen($filename);
↓
fopen($dirname.basename($filename), ’rb’);
```

☀︎$dirname で固定のディレクトリを指定、basename()でパス名からファイル名のみを取り出している。

- 相対パス「../」や、絶対パス「/etc/passwd」を入力しても非公開のファイルまで辿り着けない。

### 保険的対策

###### ３.ファイルのアクセス権限を適切に設定する

Web サーバー内のファイルやアプリケーション、ユーザーに、<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">必要最低限の権限のみ付与</span>する。  
そのため攻撃者が不正のリクエストを送っても、その権限の範囲を超えるアクセスが拒否されたり、被害を最小限に抑えることができる。

###### ４.ファイル名のチェックをする

- ホワイトリスト方式によるバリデーション  
  指定で許可する文字の組み合わせを決めておき、それ以外は許可しない方式。  
  「数字とアルファベットのみからなる文字列であること」をチェックする。

- エスケープ処理をする  
  特別な意味を持つ文字を変換や無害化(サニタイジング)、除外する。  
  （ /, .., \, |, <, > など）

- ディレクトリ指定文字列をチェック  
  ディレクトリ移動や指定をする文字列(.. , / など)が含まれていないかチェックし、含まれていればエラーとする。  
  URL のときは、「../」を URL エンコーディングすると、「%2e%2e%2f」となる。  
  さらにもう一度エンコーディングすると「%252e%252e%252f」となるため、  
  複数回デコードをして「../」が含まれていないかチェックする。

###### ５.WAF(Web Application Firewall)の導入

ディレクトリ・トラバーサルを含むさまざまな攻撃を検知して自動的にブロックする。  
しかし誤検知（False Positive）のリスクがあり、また多重エンコードなど検知の隙間を突いた攻撃や未知の攻撃手法に対しては完全に防げないため、  
他のセキュリティ対策も合わせて実施する。

###### ６.サーバー上に必要のない非公開情報を置かない。

もし攻撃されてもファイル自体がないため情報が漏洩しない。

# Laravel での実装例

### 1.basename 関数でファイル名のみ取得する

basename()は、引数のパスからファイル名だけを返してくれる PHP の関数。

### 2.バリデーション処理をする(<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">validate 関数</span>)

外部からファイル名を入力されるところに

```php
public function download (Request $request) {
    $request->validate([
        'filename' => ['required', 'regex:/^[a-zA-Z0-9_\-\.]+$/']
    ]);
}
```

☀︎ 英数字・アンダースコア・ハイフン・ピリオド以外があるときは通過できないようにする。

- required 属性で必須入力として、空欄であってもエラーとなる。

### 3.Storage ファザードでファイルを操作する

`Storage::get();`を使ってファイルを取得する。

---

### 参考にしたサイト

- https://cyber-insurance.jp/column/1385/#%E7%B5%B6%E5%AF%BE%E3%83%91%E3%82%B9%E3%81%A8%E7%9B%B8%E5%AF%BE%E3%83%91%E3%82%B9%E3%81%AE%E9%81%95%E3%81%8 https://www.gmo.jp/security/cybersecurity/cyberattack/blog/directory-traversal-attacks/
- https://hwdream.com/directory_traversal_attacks/
- https://www.ipa.go.jp/security/vuln/appgoat/ug65p900000198gm-att/000077212.pdf
- https://qiita.com/tani35web1/items/bae93769d6c30b9c5bc3.
- https://codelikes.com/laravel-storage/https://qiita.com/suzu12/items/9f43f9bddc735dbbfa07
