# 【SQL】算術演算子と CASE 演算子

- SELECT 文の選択列リスト
- INSERT 文の VALUES 句
- UPDATE 文の SET 句  
  で値の代わりに使える演算子をまとめてみました。

# 算術演算子

算術演算子はよく値の計算に使われるが、  
日付の計算や文字列の連結にも使える(DBMS によって構文が異なる)。

| 構文               | 説明                       |
| :----------------- | :------------------------- |
| 数値 + 数値        | 数値同士で足し算           |
| 日付 + 数値        | 日付を数値の日数だけ進める |
| 数値 - 数値        | 数値同士で引き算           |
| 日付 - 数値        | 日付を数値の日数だけ戻す   |
| 日付 - 日付        | 日付の差の日数を得る       |
| 数値 \* 数値       | 数値同士で掛け算           |
| 数値 / 数値        | 数値同士で割り算           |
| 文字列 \|\| 文字列 | 文字列を連結する           |

# CASE 演算子

CASE 演算子は、  
列の値や条件式を計算し、その結果によって値を変換する。  
SQL での条件分岐ができる。

##### 単純 CASE 式

```sql
CASE  列名
 WHEN 値1 THEN 値1のときに返す値
（WHEN 値2 THEN 値2のときに返す値)
 •••
（ELSE デフォルト値)
END
```

```SQL
SELECT  gender,
 CASE gender
   WHEN ’M’  THEN '男性'
   WHEN ’F’  THEN '女性'
   ELSE '不明'
END
FROM customers;
```

☀︎customers テーブルの gender 列が、  
’M’なら「男性」、’F’なら「女性」、それ以外なら「不明」と表示される。

##### 検索 CASE 式

```sql
CASE
 WHEN 条件1 THEN 条件1のときに返す値
（WHEN 条件2 THEN 条件2のときに返す値)
 •••
（ELSE デフォルト値)
END
```

```SQL
SELECT name,
 CASE
   WHEN age < 18 THEN '未成年'
   WHEN age >= 18 AND age < 65 THEN '成人'
   ELSE '高齢者'
END AS age_label
FROM customers;
```

☀︎customers テーブルの age が、  
18 未満なら「未成年」、18〜64 なら「成人」、それ以外なら「高齢者」に変換され、  
name 列と CASE 式で判定したラベル列(age_label)が表示される。

---

### 参考にしたサイト

- https://techplay.jp/column/1733
