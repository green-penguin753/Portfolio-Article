# 【MySQL】TCL 文（トランザクション）

データベース管理システム(DBMS)には、  
安全で確実なデータ操作とデータ管理を保証するため
<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">トランザクションという仕組みがあり、それを操作・制御する SQL 文</span>を TCL 文という。

- DBMS によるデータの整合性を保つ方法は主に２つあり、  
  予期しない処理中断に対しては「トランザクション」、  
  トランザクションの同時操作に対しては「ロック」で対処する。

# トランザクションとは

<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">1 つ以上の SQL 文を 1 つのまとまり</span>として扱う。  
処理が正常に完了したときのみデータベースに反映<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">(コミット)</span>し、  
途中で問題が発生したときは、すべての処理を取り消して元の状態に戻す<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">(ロールバック)</span>仕組みのこと。

- SQL 文をトランザクション開始・終了の文で囲むことで実行される。
- 処理が中断されたら、`ROLLBACK;`を明示していなくても自動的にロールバックされる。

- 切り離すことのできない一連の処理をトランザクション処理といい、ACID 特性を持つ。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎トランザクションのACID特性☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">
<b>原子性</b>(Atomicity)・・・トランザクション処理が、すべて成功かすべて失敗かで終了すること。<br>
<b>一貫性</b>(Consistency)・・・トランザクション実行の前後でデータベースの内容に矛盾がないこと。<br>
<b>独立性</b>(Isolation)・・・複数のトランザクションを同時に実行したとき、他のトランザクションの影響を受けないこと。分離性。<br>
<b>耐久性</b>(Durability)・・・トランザクションが正常終了すると、コミットした結果は障害が発生しても消失しないこと。<br>
</div>

# トランザクション指示

##### START TRANSACTION・・・トランザクション開始

- または`BEGIN;` (BEGIN はストアドプログラムで使う。)

- デフォルトの自動コミットが一時的に無効になる。
- トランザクション中の SQL 文は「仮の状態」で管理される。

##### COMMIT・・・<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">処理を確定</span>し、トランザクション終了

- トランザクション中では手動でコミット(終了の文)が必要

##### ROLLBACK・・・<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">処理を全消去</span>し、トランザクション終了

- トランザクション中では手動でロールバック(終了の文)が必要。
- 途中で処理が中断されたときだけでなく、意図的に元に戻したいときにも使える。
- DDL 文は暗黙的にコミットされるため、ロールバックできないので注意する。

```SQL
START TRANSACTION;

INSERT INTO orders_archive
SELECT *
FROM orders
WHERE purchase_date <= '2024-01-31';

DELETE
FROM orders
WHERE purchase_date <= '2024-01-31';

COMMIT;
```

☀︎ データをアーカイブに移動して、元のデータを削除している。

```SQL
START TRANSACTION;

DELETE
FROM orders
WHERE purchase_date <= '2024-01-31';

ROLLBACK;
```

☀︎ 元のデータの削除を取り消している。

- ROLLBACK;より先に`COMMIT;`と書いてしまうと確定されてしまい取り消せない。

# トランザクションの排他制御(ロック)

ロックとは、データベースの更新中にデータの不整合が発生しないように  
<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">一時的にアクセス制限をかけて他のトランザクションから更新できないようにする仕組み</span>のこと。

- トランザクションの独立性を守る。
- トランザクションの開始によりロックをかけることができ、その間は他のトランザクションでは<span style="background: linear-gradient(transparent 40%, #F9C1CF 100%);">「ロック開放待ち」の状態</span>になる。  
  終了の文(COMMIT/ROLLBACK)でロックが解放される。
- **排他ロック**・・・更新(INSERT/UPDATE/DELETE)するときに使う。他からは参照も更新もできない。
- **共有ロック**・・・参照(SELECT)するときに使う。他からは参照はできるが、更新はできない。
- デットロックとは、お互いにロック開放待ちになる状態のこと。
- ロックはできるだけ最小の範囲に留めておくことが推奨される。

---

### 参考にしたサイト

- https://zenn.dev/umi_mori/books/331c0c9ef9e5f0/viewer/aba691
- https://dev.mysql.com/doc/refman/8.0/ja/commit.html
- https://yttm-work.jp/lang/mysql/mysql_0004.html
- https://qiita.com/simoyama2323/items/4e82a1b516a219a4bfd6
- スッキリわかる SQL 入門 第４版 ドリル２５６問付き！
