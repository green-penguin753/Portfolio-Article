# 【SQL】DCL 文(GRANT・REVOKE)

DCL 文(データ制御言語)とは、  
データベースへのアクセス制御や権限の管理を設定する SQL 文のこと。

- 「誰にどの操作を許可・禁止をすか」といった、データ操作(DML)やテーブル操作(DDL)を詳細に設定できる。
- データベース管理者(DBA)や権限を持ったユーザーだけが実行できる。
- 必要最小限の権限だけを付与するようにする（最小権限の原則）。

☀︎GRANT」「REVOKE」で設定できる主な権限 ☀︎

・SELECT・INSERT・UPDATE・DELETE の権限
・CREATE：データベース、テーブルを作成する権限
・EXECUTE：関数やストアドプロシージャなどの使用を許可する権限
・ALL PRIVILEGES：指定したスコープで付与できるすべての権限をまとめて許可する権限
・USAGE：権限がないことを指す。
☀︎ 割り当てられている権限を確認するには SHOW GRANTS を使う。

- 複数のロールやユーザーにまとめて設定するには、カンマで区切って指定する。

- テーブル名ではなくデータベース名のときは「mydb.\*」となる。
- 1 つの文で権限とロールを同時には設定できないため、それぞれ個別に GRANT 文や REVOKE 文を書く。

# 権限付与(GRANT)

###### 1.個別に権限を付与する方法

`GRANT 権限名 ON テーブル名 TO ユーザー名;`

```SQL
--ユーザーに権限付与
GRANT SELECT ON customers TO 'user1'@'localhost';
--ロールに権限付与
GRANT SELECT ON customers TO 'role1';
```

☀︎customers テーブルの SELECT 操作権限をつけている。

###### 2.ロール(役割)にユーザーを割り当てる方法

ロールをユーザーに付与してまとめて管理する。

`GRANT ロール名 TO ユーザー名;`

```SQL
GRANT 'role1' TO 'user1'@'localhost';
```

☀︎user1 にロール 1 の権限をつけている。

# 権限削除(REVOKE)

###### 1.個別に権限を削除する方法

`REVOKE 権限名 ON テーブル名 FROM ユーザー名;`

```SQL
--ユーザーから権限削除
REVOKE SELECT ON customers FROM 'user1'@'localhost';
--ロールから権限削除
REVOKE SELECT ON customers FROM 'role1';
```

☀︎customers テーブルの SELECT 操作の権限を削除している。

###### 2.ロール(役割)にユーザーを割り当てる方法

ユーザーからロールごと権限を削除する。

`REVOKE ロール名 FROM ユーザー名;`

```SQL
REVOKE 'role1' FROM 'user1'@'localhost';
```

☀︎user1 からロール 1 の権限を削除している。

---

### 参考にしたサイト

- https://appmaster.io/ja/glossary/detazhi-yu-yan-yu-dcl
- https://tech.kurojica.com/archives/59092/
- https://dev.mysql.com/doc/refman/8.0/ja/grant.html
