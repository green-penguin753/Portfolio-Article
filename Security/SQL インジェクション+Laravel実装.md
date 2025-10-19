# 【Security】SQL インジェクション+Laravel 実装

# 概要

Web アプリケーションのユーザーの入力領域に  
攻撃者が<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">不正な SQL 文を注入し、データベースに意図しない命令を実行させる</span>攻撃手法。

- ログインフォームや検索機能などを持つ Web サイトは特に注意する。

###### 発生しうる脅威

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">重要情報の漏洩</span>  
  データベースに格納されている重要な情報(パスワードやカード情報など)が盗まれる。  
  企業の信頼を大きく損なうことにもつながる。

- サイトの改ざん、削除  
  偽の情報を表示したり、情報を消去することができる。

- データベースの全消去・破壊  
  DELETE、DROP 文などを使い、データベースごと削除される

- システムの乗っ取りや、攻撃の踏み台にされる  
  管理者権限を奪われ、サーバーを他の攻撃に使われる。

```SQL
--脆弱性のあるコード
SELECT * FROM users WHERE id='$id' AND pass='$pass';
↓
--正常な入力　
SELECT * FROM users WHERE id='John' AND pass='123pass';

--攻撃者の入力　
 SELECT * FROM users WHERE id='' or 1=1; -- 'AND pass='123pass';

```

☀︎ 攻撃者が$id に「' or 1=1; --」と入力されると、

- $id は空文字または 1 は 1 に等しいという条件になり常に真となる。
- --以降はコメント扱いになるためパスワードの条件は無効になる。

→ そのため本来は通らないユーザー認証が成功してしまう。

# 原因

ユーザーからの入力値を<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">そのまま SQL 文に埋め込む</span>こと

# 対策

### 根本的解決

###### １.<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">プレースホルダーとプリペアドステートメントで実装する</span>

- プレースホルダーとは、

  - SQL 文の変数の部分を「?」や「:name」などの記号で置き換えたもの。
  - これにより SQL 構文と値が別々にデータベースに送信され、  
    悪意のある値であっても SQL として解釈されず安全に実行される。

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">静的プレースホルダー</span>
  - プリペアドステートメントは、  
    プレースホルダを含む SQL 文を先に準備し、後からデータベース側でバインドして実行する仕組み。
  - 同じ SQL 構文で何度も実行できるため、効率的に使える。

###### PDO でのプレースホルダー使用例

```php
//プレースホルダー付きSQL文を準備
$stmt = $PDO->prepare("SELECT * FROM users WHERE id = :id  AND  pass = :pass");

//値をバインド
$stmt->bindValue(':id', $id);　
$stmt->bindValue(':pass', $pass);

//実行
$stmt->execute();
```

###### ２.エスケープ処理

データベースに値を渡す前に、特殊文字を安全な形に変換する。  
「’」→「’’」、「￥」→「￥￥」など  
PHP では `$mysqli->real_escape_string($input)` を使うことができる。

###### ３.hidden パラメータで直接指定しない。(禁忌)

ユーザーからの入力を直接 SQL に組み込むのは避ける

### 保険的対策

###### ４.エラーメッセージ表示しない

攻撃者に内部構造（テーブル名など）の情報を与えないようにする。  
エラーメッセージは表示せず、ログファイルに記録する。

###### ５.データベースの権限を最小限に設定する

DB ユーザーには必要最小限の操作だけ許可する。  
SELECT 操作で十分であれは、INSERT や DELETE 文の権限までは付与しない。

# Laravel での実装例

### 1.Eloquent ORM を使う

- Laravel には、<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">「Eloquent ORM」</span>という PDO のプリペアドステートメントを利用した機能が搭載されている。

- モデルクラスとしてデータベースのテーブルと連携し、SQL 文を直接書かずにデータベースを操作できる。

- さらに詳細なクエリや条件を指定したいときは、「クエリビルダー」を使う。
- 生 SQL を使うときは、プリペアドステートメントを利用したり、入力値のバリデーションやエスケープ処理を徹底する。

**実装の流れ**

①**あらかじめモデルでデータベーステーブルと連携しておく**  
Post.php ファイルに

```php

//Postクラスの作成
class Post extends Model
{
　//テーブル名を指定
    protected $table = 'posts';
}
```

②**コントローラーで Post クラスを使う**  
PostController.php ファイルに

```php

class PostController extends Controller
{
	public function index() {
		//postsテーブルのデータを全件取得
		$posts=Post::all();
		return view('posts.index', compact('posts'));
		}
}

```

③**ビューで$posts を使い表示させる**  
posts/index.blade.php ファイルに

```php
@foreach($posts as $post)
  <div>
    <h2>{{ $post->title }}</h2>
    <p>{{ $post->body }}</p>
  </div>
@endforeach
```

---

### 参考にしたサイト

- https://webukatu.com/wordpress/blog/1638/
- https://fragile-archives.com/2024/06/28/php-pdo-05/#google_vignette.
