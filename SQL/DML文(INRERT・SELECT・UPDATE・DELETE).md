# 【SQL】DML 文(INRERT・SELECT・UPDATE・DELETE)

SQL ではデータの操作・定義・制御の 3 つができ、DML(データ操作言語)を使ってデータベースを操作する。

- CREATE(作成) ：INSERT 文
- READ(読み取り) ：SELECT 文
- UPDATE(更新） ：UPDATE 文
- DELETE(削除) ：DELATE 文

頭文字をとって「CRUD」や、「（SQL の)４大命令」とも呼ばれる。

# INSERT 文

INSERT 文はテーブルに<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">行(レコード)を追加</span>するとき使う。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">

INSERT INTO テーブル名(列名 1, 列名 2, …)<br>
VALUES (値 1, 値 2, …);<br>

</p>
</div>

- `INTO`と組み合わせて取得したいテーブル名を指定する。
- テーブル名の後の列名を省略することもできるが、VALUES 句では全ての列(カラム)の順番で値を指定する。
- VALUES 句をカンマ(,)で区切ると、複数の行を一括で追加できる。

```SQL
INSERT INTO customers (id, name, age)
VALUES (3, ’John’, 20);

```

# SELECT 文

SELECT 文は<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">データを取得</span>するときに使う。

- **SELECT 文の記述順**
<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">

SELECT 列名 1, 列名 2, ・・・<br>
FROM テーブル名<br>
[WHERE］<br>
[GROUP BY］<br>
[HAVING］<br>
[ORDER BY］<br>

</p>
</div>

```SQL
SELECT  name, age
 FROM  customers
```

- SELECT の列名をアスタリスク(\*)にすると、全ての列を指定できる。
- SELECT の列名をカンマ(,)で区切ると、複数の列を指定できる。
- `FROM`句と組み合わせて取得したいテーブル名を指定する。

#### SELECT 文の実行順序

SQL は記述した上から順に実行されるのではなく、  
<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">句ごとに決まった実行順序</span>で処理される。

①FROM ：テーブルの読み込み<br>
②JOIN ：テーブル同士の結合<br>
③WHERE ：取得条件で絞り込み<br>
④GROUP BY ： グループ化<br>
⑤HAVING ：④ のグループから絞り込み<br>
⑥SELECT ：結果を表示するカラムを指定<br>
⑦DISTINCT ：⑥ の結果から重複する行を除外<br>
⑧ORDER BY ：⑦ の結果から並び替え<br>
⑨LIMIT ：⑧ の結果から取得する件数を指定する<br>

# UPDATE 文

UPDATE 文は<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">データを書き換える</span>ときに使う。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">

UPDATE テーブル名<br>
SET 列名=値<br>
WHERE 列名=値<br>

</p>
</div>

- WHERE で行を指定しないと、全件更新される。
- SET 句で列名=値を,(コンマ)で区切ると、複数の値を指定できる。
- 実行後は元に戻せない。→[トランザクション処理](https://greenpenguin.hatenablog.jp/entry/2025/05/25/022222)

```SQL
UPDATE customers
SET name=’Mike’ ,age=22
WHERE id=3;
```

# DELETE 文

DELETE 文は<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">行(レコード)を削除する</span>ときに使う。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">

DELETE <br>
FROM テーブル名<br>
WHERE 列名=値;

</p>
</div>

- WHERE で行を指定しないと、全件更新される。
- 複数の行を指定する場合は、論理演算子（AND, OR, IN）を使う。
- 実行後は元に戻せない。→[トランザクション処理](https://greenpenguin.hatenablog.jp/entry/2025/05/25/022222)

```SQL
DELETE
FROM customers
WHERE id=3;
```

# FROM 句

<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">テーブルを選択しデータの読み込み</span>をする。

- JOIN 句を使うと複数のテーブルを指定できる。
- 副問い合わせを指定でき、一時的なテーブルとして扱うことができる。

# WHERE 句

<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">テーブル全体から条件の絞り込み</span>をする。  
検索する前に対象の行を絞る。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 条件式
</p>
</div>

- WHERE 句を指定しないと、テーブル全体が処理対象になる。  
  全ての行(レコード)の更新など。
- SELECT、UPDATE、DELETE 文で使える。
- 条件式は結果が必ず真か偽になるように指定する。

- [WHERE 句の演算子](https://greenpenguin.hatenablog.jp/entry/2025/05/19/005656)

# LIMIT 句

<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">結果から行数を制限</span>する。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
LIMIT 取得したい行数
</p>
</div>

- `OFFSET`句と組み合わせて、先頭から何行スキップするかを指定できる。  
  (LIMIT 句に 2 つの引数を渡すことで、OFFSET 句を省略も可能）

```SQL
SELECT  name
 FROM  customers
 LIMIT 10
 OFFSET  5;
```

☀︎6〜15 行目だけを取得できる。

# AS 句（エイリアス）

テーブル名やカラム名に<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">一時的な別名をつける</span>こと。

- テーブル名が長いときや、複雑な結果に名前をつけたいときに使い、読みやすくできる。
- SELECT 文の実行順序によって使える範囲がある。  
  （エイリアスが定義された後の句であれば使える。）

---

### 参考にしたサイト

- https://zenn.dev/gorogoroumaru/articles/a30f63a3eef7f2.
- https://gihyo.jp/dev/serial/01/mysql-road-construction-news/0141
