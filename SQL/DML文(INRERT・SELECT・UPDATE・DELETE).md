# 【SQL】DML 文(INRERT・SELECT・UPDATE・DELETE)

SQL ではデータの操作・定義・制御の 3 つができ、DML(データ操作言語)を使ってデータベースを操作する。

- CREATE(作成) ：INSERT 文
- READ(読み取り) ：SELECT 文
- UPDATE(更新） ：UPDATE 文
- DELETE(削除) ：DELATE 文

頭文字をとって「CRUD」や、「（SQL の)４大命令」とも呼ばれる。

# INSERT 文

INSERT 文はテーブルに行(レコード)を追加するとき使う。

```sql
INSERT INTO テーブル名(列名 1, 列名 2, …)
VALUES (値 1, 値 2, …);
```

- `INTO`と組み合わせて取得したいテーブル名を指定する。
- テーブル名の後の列名を省略することもできるが、VALUES 句では全ての列(カラム)の順番で値を指定する。
- VALUES 句をカンマ(,)で区切ると、複数の行を一括で追加できる。

```SQL
INSERT INTO customers (id, name, age)
VALUES (3, ’John’, 20);
```

# SELECT 文

SELECT 文はデータを取得するときに使う。

- **SELECT 文の記述順**

```
SELECT 列名 1, 列名 2, ・・・
FROM テーブル名
[WHERE］
[GROUP BY］
[HAVING］
[ORDER BY］
```

```SQL
SELECT  name, age
 FROM  customers
```

- SELECT の列名をアスタリスク(\*)にすると、全ての列を指定できる。
- SELECT の列名をカンマ(,)で区切ると、複数の列を指定できる。
- `FROM`句と組み合わせて取得したいテーブル名を指定する。

#### SELECT 文の実行順序

SQL は記述した上から順に実行されるのではなく、  
句ごとに決まった実行順序で処理される。

①FROM ：テーブルの読み込み**
②JOIN ：テーブル同士の結合**
③WHERE ：取得条件で絞り込み**
④GROUP BY ： グループ化**
⑤HAVING ：④ のグループから絞り込み**
⑥SELECT ：結果を表示するカラムを指定**
⑦DISTINCT ：⑥ の結果から重複する行を除外**
⑧ORDER BY ：⑦ の結果から並び替え**
⑨LIMIT ：⑧ の結果から取得する件数を指定する\*\*

# UPDATE 文

UPDATE 文はデータを書き換えるときに使う。

```sql
UPDATE テーブル名**
SET 列名=値**
WHERE 列名=値**
```

- WHERE で行を指定しないと、全件更新される。
- SET 句で列名=値を,(コンマ)で区切ると、複数の値を指定できる。
- 実行後は元に戻せない。→ トランザクション処理

```SQL
UPDATE customers
SET name=’Mike’ ,age=22
WHERE id=3;
```

# DELETE 文

DELETE 文は行(レコード)を削除するときに使う。

```sql
DELETE **
FROM テーブル名**
WHERE 列名=値;
```

- WHERE で行を指定しないと、全件更新される。
- 複数の行を指定する場合は、論理演算子（AND, OR, IN）を使う。
- 実行後は元に戻せない。→ トランザクション処理

```SQL
DELETE
FROM customers
WHERE id=3;
```

# FROM 句

テーブルを選択しデータの読み込みをする。

- JOIN 句を使うと複数のテーブルを指定できる。
- 副問い合わせを指定でき、一時的なテーブルとして扱うことができる。

# WHERE 句

テーブル全体から条件の絞り込みをする。  
検索する前に対象の行を絞る。

`WHERE 条件式`

- WHERE 句を指定しないと、テーブル全体が処理対象になる。  
  全ての行(レコード)の更新など。
- SELECT、UPDATE、DELETE 文で使える。
- 条件式は結果が必ず真か偽になるように指定する。

# LIMIT 句

結果から行数を制限する。

`LIMIT 取得したい行数`

- `OFFSET`句と組み合わせて、先頭から何行スキップするかを指定できる。  
  （LIMIT 句に 2 つの引数を渡すことで、OFFSET 句を省略も可能）

```SQL
SELECT  name
 FROM  customers
 LIMIT 10
 OFFSET  5;
```

☀︎6〜15 行目だけを取得できる。

# AS 句（エイリアス）

テーブル名やカラム名に一時的な別名をつけること。

- テーブル名が長いときや、複雑な結果に名前をつけたいときに使い、読みやすくできる。
- SELECT 文の実行順序によって使える範囲がある。  
  （エイリアスが定義された後の句であれば使える。）

---

### 参考にしたサイト

- https://zenn.dev/gorogoroumaru/articles/a30f63a3eef7f2.
- https://gihyo.jp/dev/serial/01/mysql-road-construction-news/0141
