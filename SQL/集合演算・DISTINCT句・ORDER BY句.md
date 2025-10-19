# 【SQL】集合演算・DISTINCT 句・ORDER BY 句

集合演算は、検索結果を組み合わせる。  
DISTINCT 句は、SELECT 文の結果から重複した行を除く。  
ORDER BY 句は、取得したデータを指定した列名で並べ替える。

# 集合演算子

複数のテーブルの<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">SELECT 文の検索結果を 1 つにまとめる</span>。

- テーブル同士の検索結果の列数＆データ型を完全に一致させておくこと。
- 「(ALL)」をつけることで重複した行も含めて取得できる。  
  UNION(ALL), EXCEPT (ALL), INTERSECT (ALL)

### UNION・・・和集合

2 つの検索結果を<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">足し合わせた行</span>から重複を除いた集合。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
SELECT  列名1, 列名2<br>
 FROM  テーブル名1<br>
 UNION<br>
SELECT  列名1, 列名2<br>
 FROM  テーブル名2;<br>
</p>
</div>

- 項目の一覧を抽出するときなどに使う。

### EXCEPT・・・差集合

1 つ目の検索結果から、2 つ目の検索結果のデータを<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">差し引いた行</span>から重複を除いた集合。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
SELECT  列名1, 列名2<br>
 FROM  テーブル名1<br>
 EXCEPT<br>
SELECT  列名1, 列名2<br>
 FROM  テーブル名2;<br>
</p>
</div>

- 今月の新規顧客データを抽出するときなどに使う。

### INTERSECT・・・積集合

2 つの SELECT 文の検索結果に<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">共通して含まれる行</span>から重複を除いた集合。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
SELECT  列名1, 列名2<br>
 FROM  テーブル名1<br>
 INTERSECT<br>
SELECT  列名1, 列名2<br>
 FROM  テーブル名2;<br>
</p>
</div>
- 前月と今月の両方に存在する顧客データを抽出するときなどに使う。

# DISTINCT 句

SELECT 文の<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">検索結果から重複するデータを除く。</span>

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
SELECT DISTINCT 列名<br>
 FROM  テーブル名;
</p>
</div>

- 複数の列名を指定したときは、指定した列の組み合わせが重複しない行だけが抽出される。
- COUNT 関数と組み合わせて`SELECT COUNT(DISTINCT 列名) ` とすると、重複しない値の件数を数えられる。

# ORDER BY 句

SELECT 文から重複を除いた<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">検索結果のデータを並び替える。</span>

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
SELECT DISTINCT 列名<br>
 FROM  テーブル名<br>
 ORDER BY 列名 並べ方;
</p>
</div>

- 並べ方は<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">昇順なら「ASC」、降順なら「DESC」</span>と指定する。
- 複数の列名を指定したときは、  
  最初の列で並び替えが優先され、同じ値が複数あれば次の列で並び替える。
- 列ごとに並べ方を個別に指定できる。
- 列番号を指定して並び替えることもできる。  
  列番号とは SELECT 句で指定した列の順番を指し、記述した順に 1 から数える。
- ORDER BY 句を省略すると、  
  並び順が順序保証されず、実質的にランダムで表示される。

---

### 参考にしたサイト

- https://analytics-okinawa.jp/sql/1305/
- https://tech-blog.rakus.co.jp/entry/20220712/distinct
