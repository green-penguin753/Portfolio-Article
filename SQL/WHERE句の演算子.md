# 【SQL】WHERE 句の演算子

WHERE 句で条件の絞り込みに使う演算子をまとめました。

# 比較演算子

| 基本の比較演算子 | 意味                                 |
| :--------------- | :----------------------------------- |
| =                | 左右の値が等しい                     |
| <                | 右の値より小さい                     |
| >                | 右の値より大きい                     |
| <=               | 以下                                 |
| >=               | 以上                                 |
| <>               | 左右の値が等しくない。「!=」でも可能 |

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 条件1 = 条件2
</p>
</div>
☀︎条件1と条件2が等しい。

# NULL 演算子

指定した列の値が<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">NULL である行</span>を取得する。

- NULL とは、どのような値も格納されていない状態のこと。  
  データが不明(unknown)のときと、無意味(not applicable)のときがある。

- NULL の判定に比較演算子は使えないため、<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">IS 演算子</span>を使う。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 列名  IS NULL
</p>
</div>
☀︎指定した列の値がNULLである行のみ取得する。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 列名  IS NOT NULL
</p>
</div>
☀︎指定した列の値がNULLではない行のみ取得する。

# 論理演算子

**AND 演算子**・・・かつ

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 条件1 AND 条件2
</p>
</div>
☀︎両方の条件を満たす行を取得する。

```SQL
SELECT *
FROM  customers
WHERE name=’John’ AND age>=20;
```

20 歳以上の'John'の行(レコード)を取得する。
<br><br>

**OR 演算子**・・・または

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 条件1 OR 条件2
</p>
</div>

☀︎ どちらかの条件を満たす行を取得する。

**NOT 演算子**・・・否定

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE NOT 条件
</p>
</div>
☀︎両方の条件に当てはまらない行を取得する。

##### 論理演算子の優先度

NOT → AND → OR の順に評価されるが、
カッコ()でくくると優先順位が上がる。

# LIKE 演算子

<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">指定した文字列を含んでいる行</span>を取得する。  
パターンマッチング。

- パターン文字列に使うワイルドカード  
  「<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">%</span>」・・・任意の 0 文字以上の文字列  
  「\_(アンダースコア)」・・・任意の 1 文字
  - 前方一致、後方一致も可能
  - 単なる文字として％や\_を使いたいときは、ESCAPE 句($)を使う。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 列名 LIKE ’%パターン文字列%’
</p>
</div>
☀︎指定した列名でパターン文字列を含んでいる行のみ取得する

# BETWEEN 演算子

<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">指定した範囲に値が収まっている行</span>を取得する。

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 列名 BETWEEN 値1 AND 値2
</p>
</div>
☀︎指定した列名で値1〜値2の範囲にある行のみ取得する。

# IN／NOT IN 演算子

<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">指定した複数の値と一致した行</span>を取得する。

**IN 演算子**

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 列名 IN(値1, 値2, 値3…)
</p>
</div>
☀︎いずれかの値に一致する行を取得する。

**NOT IN 演算子**

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE 列名 NOT IN(値1, 値2, 値3…)
</p>
</div>
☀︎すべての値に一致しない行を取得する。

# ANY／ALL 演算子

<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">指定した複数の値と比較し真である行</span>を取得する。

- 必ず基本の比較演算子（=、<、>など）をつける。
- 計算式や[副問い合わせ](https://greenpenguin.hatenablog.jp/entry/2025/05/26/054727)と組み合わせて使う。

**ANY 演算子**

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE  列名 基本の比較演算子  ANY(値1, 値2, 値3…)
</p>
</div>
☀︎いずれかの値が基本比較演算子で真となる行を取得する。

**ALL 演算子**

<div style="background: #f5f5f5;  border-radius: 5px; padding: 10px; margin: 10px;">
<p style="margin: 0;">
WHERE  列名 基本の比較演算子  ALL(値1, 値2, 値3…)
</p>
</div>
☀︎すべての値が基本比較演算子で真となる行を取得する。

---

### 参考にしたサイト

- progate
- https://zenn.dev/progate_users/articles/aaabbb666387f0
