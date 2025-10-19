# 【SQL】SQL の関数

# よく使う関数

### LENGTH()・・・文字列の長さ

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
LENGTH(列名)
</p>
</div>

```SQL
SELECT  LENGTH(email)
FROM customers;
```

☀︎ メールアドレスが何バイトなのか。  
名前などの文字数を数えたいときは`CHAR_LENGTH()`を推奨

### TRIM()・・・空白の除去

- CHAR 型の列の空白を取り除くときに使う。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
TRIM(列名)
</p>
</div>

```SQL
SELECT  TRIM(name)
FROM customers;
```

☀︎ 文字列の左右から空白を取り除く。「 あいう 」→「あいう」

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎空白を除去する関数☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">
・TRIM()・・・・左右から空白を除去<br>
・LTRIM() ・・・左側から空白を除去<br>
・RTRIM()・・・右側から空白を除去
</div>

### REPLACE()・・・指定した文字を置換

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
REPLACE(列名, '置換前', '置換後')
</p>
</div>

```SQL
UPDATE  items
SET item_name = REPLACE(item_name, 'abc', 'xyz');
```

☀︎ 文字列の一部を書き換える。「12abc34」→「12xyz34」

### SUBSTRING()・・・文字列の一部を抽出する

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
SUBSTRING(列名, 開始位置, 文字数)
</p>
</div>

```SQL
SELECT SUBSTRING(item_name, 1, 5)
FROM  items;
```

☀︎ 指定した列の 1〜5 文字目だけを抽出する.

- WHERE 句で条件を追加して使うことが多い。
  `WHERE SUBSTRING(item_name, 1, 5) = 'apple'`

### ROUND()・・・四捨五入

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
ROUND(数値型の列名, 有効桁数)
</p>
</div>

```SQL
SELECT ROUND(price, -2)
FROM  items;
```

☀︎-2 なので下 2 桁(10 の位)で四捨五入する。「380」円 →「400」円

### TRUNC()・・・切り捨て

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
TRUNC(数値型の列名, 有効桁数)
</p>
</div>

```SQL
SELECT TRUNC(price, -2)
FROM  items;
```

☀︎-2 なので下 2 桁(10 の位)で切り捨てる。「380」円 →「300」円

### POWER()・・・べき乗を計算

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
POWER(数値型の列名または数値, 何乗かを指定する数値)
</p>
</div>

```SQL
SELECT POWER(2, 3);
```

☀︎2 の 3 乗(2×2×2)を計算し、結果は「8」となる。

### CURRENT_DATE・・・現在の日時を取得

データベースの追加や更新した日時を記録しておくことが多い。

- CURRENT_TIMESTAMP・・・現在の日時(年、月、日、時、分、秒)
- CURRENT_DATE ・・・現在の日付(年、月、日)
- CURRENT_TIME ・・・現在の時刻(時、分、秒)

```SQL
INSERT INTO customers (id, name, age, created_date)
VALUES  (3, ’John’, 20, CURRENT_DATE);
```

☀︎created_date (登録日)に今日の日付が自動的に入る。

### CAST()・・・データ型の変換

- あるデータ型を別のデータ型に変換するための関数。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
CAST(変換したい値や列名 AS 変換後のデータ型)
</p>
</div>

```SQL
SELECT id, CAST(created_date AS CHAR)
FROM customers;
```

☀︎DATETIME 型から文字列型に変換する

# ストアドプログラム

SQL にはデータベースへの複数の命令をまとめて RDBMS に保存する機能がある。

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">**ストアドファンクション**</span>(ユーザー定義関数)

  - 必要な処理を自分で関数として作成して保存する。
  - 必ず戻り値を返す。
  - CREATE FUNCTION で定義、SELECT 文で呼び出し
  - SQL 内で複雑な計算や値の加工をしたいときに便利。

- <span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">**ストアドプロシージャ**</span>
  - 複数の SQL 処理をまとめて保存する。
  - 戻り値は返さない。
  - CREATE PROCEDURE で定義、CALL で呼び出し
  - SELECT 文などの SQL で直接使えない。
  - SQL インジェクション対策の一つとして使える。

---

### 参考にしたサイト

- スッキリわかる SQL 入門 第４版 ドリル２５６問付き！
- https://qiita.com/RyutoYoda/items/180ca7c560b22c4fe6b5
- http://note.com/tokyobang/n/n1fc791cf9078
- https://products.sint.co.jp/siob/blog/storedprocedure
