# 【SQL】DDL 文(CREATE・ALTER・DROP)

DDL 文(データ定義言語)とは、  
<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">データベースの構造を作成・変更・削除する</span>ための SQL 文のこと。  
テーブルやインデックス、ビューを操作する。

# 作成(CREATE)

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
CREATE TABLE テーブル名 （<br>
 列名1 列名1のデータ型名,<br>
 列名2 列名1のデータ型名<br>
)
</p>
</div>

- テーブルに行(レコード)を追加するには、INSERT 文を使う。

```SQL
CREATE TABLE customers (
 id  INT,
 name VARCHAR(20) ,
 age  INT  DEFAULT 0
)
```

☀︎ テーブルを新規作成する。

<br>

☀︎ データの詳細設定 ☀︎

・<b>デフォルト値</b><br>
テーブル作成で列にデフォルト値を設定しておくと、 <br>
INSERT 文でその列の値を省略したときは自動的にその値が入る。<br>
デフォルト値を設定していないときは、NULL が入る。<br>

・<b>NOT NULL </b>(非 NULL 制約)<br>
「NOT NULL」・・・NULL を入力できない<br>
「NULL」・・・NULL も入力できる<br>

・<b>UNIQUE</b>(一意性制約)<br>
そのカラムには同じ値を重複して登録できない。<br>
・<b>PRIMARY KEY</b>(主キー制約) <br>
行を一意に識別するための列に設定する。<br>  
 PRIMARY KEY を設定することで、自動的に UNIQUE と NOT NULL の制約が付く。<br>

・<b>AUTO_INCREMENT</b><br>
自動採番 <br>
その行の最大値＋ 1 を自動的にセットする。<br>

</div>

# 削除(DROP)

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
DROP TABLE テーブル名
</p>
</div>

- [DELETE 文](https://greenpenguin.hatenablog.jp/entry/2025/05/19/005459)はテーブルに登録されたデータの削除をする。
- テーブルの存在を確認してから作成・削除するには「IF EXISTS」を使う。

```SQL
DROP TABLE IF EXISTS customers;
```

☀︎ テーブルが存在するときのみ削除する。

# 変更(ALTER)

・列の追加<br>

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
ALTER TABLE テーブル名 ADD 列名 データ型
</p>
</div>
・列の削除<br>
<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
ALTER TABLE テーブル名 DROP 列名
</p>
</div>

```SQL
ALTER TABLE customers ADD created_date DATETIME;
ALTER TABLE customers DROP created_date;

```

- 既存のテーブルに列を追加するときは、新しい列は一番後ろに挿入される。

# 全行の一括削除(TRUNCATE)

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
TRUNCATE TABLE テーブル名
</p>
</div>

- DELETE 文は指定した行だけ削除もできるが、TRUNVATE は必ずすべての行を削除する。
- 記録を残さず削除するので、高速に処理できる。

---

### 参考にしたサイト

- https://envader.plus/course/2/scenario/1051
- https://www.kogures.com/hitoshi/webtext/db-ddl-dml-dcl/index.html
- progate
