# 【SQL】DDL 文(CREATE・ALTER・DROP)

DDL 文(データ定義言語)とは、  
データベースの構造を作成・変更・削除するための SQL 文のこと。  
テーブルやインデックス、ビューを操作する。

# 作成(CREATE)

```sql
CREATE TABLE テーブル名 (
 列名1 列名1のデータ型名,
 列名2 列名1のデータ型名
)
```

- テーブルに行(レコード)を追加するには、INSERT 文を使う。

```SQL
CREATE TABLE customers (
 id  INT,
 name VARCHAR(20) ,
 age  INT  DEFAULT 0
)
```

☀︎ テーブルを新規作成する。

☀︎ データの詳細設定 ☀︎

・**デフォルト値**
テーブル作成で列にデフォルト値を設定しておくと、 
INSERT 文でその列の値を省略したときは自動的にその値が入る。
デフォルト値を設定していないときは、NULL が入る。

・**NOT NULL **(非 NULL 制約)
「NOT NULL」・・・NULL を入力できない
「NULL」・・・NULL も入力できる

・**UNIQUE**(一意性制約)
そのカラムには同じ値を重複して登録できない。
・**PRIMARY KEY**(主キー制約) 
行を一意に識別するための列に設定する。  
 PRIMARY KEY を設定することで、自動的に UNIQUE と NOT NULL の制約が付く。

・**AUTO_INCREMENT**
自動採番 
その行の最大値＋ 1 を自動的にセットする。

# 削除(DROP)

`DROP TABLE テーブル名`

- DELETE 文はテーブルに登録されたデータの削除をする。
- テーブルの存在を確認してから作成・削除するには「IF EXISTS」を使う。

```SQL
DROP TABLE IF EXISTS customers;
```

☀︎ テーブルが存在するときのみ削除する。

# 変更(ALTER)

・列の追加
`ALTER TABLE テーブル名 ADD 列名 データ型`

・列の削除
`ALTER TABLE テーブル名 DROP 列名`

```SQL
ALTER TABLE customers ADD created_date DATETIME;
ALTER TABLE customers DROP created_date;
```

- 既存のテーブルに列を追加するときは、新しい列は一番後ろに挿入される。

# 全行の一括削除(TRUNCATE)

`TRUNCATE TABLE テーブル名`

- DELETE 文は指定した行だけ削除もできるが、TRUNVATE は必ずすべての行を削除する。
- 記録を残さず削除するので、高速に処理できる。

---

### 参考にしたサイト

- https://envader.plus/course/2/scenario/1051
- https://www.kogures.com/hitoshi/webtext/db-ddl-dml-dcl/index.html
- progate
