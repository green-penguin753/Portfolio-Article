# 【Shell Script】シェル関数と return 文

シェルスクリプトの  
関数についてまとめました。

# シェル関数とは

シェル関数とは、  
シェルスクリプト内で使用する、機能ごとに処理をまとめたもの

- 同じ処理を複数回実行するときに便利。  
  コードの重複を減らし見やすさと作業効率が上がる。
- メインルーチンの前に定義され、必要に応じて呼び出される。

# 定義

```bash
関数名() {
  処理
  return 終了ステータス
}
```

# 呼び出し

```bash
関数名 引数
```

function 関数名() {処理}と記述もできる。

- 関数は２種類に分けられる。

  - メインルーチン・・・プログラムを開始する関数。主軸。
  - サブルーチン・・・・プログラム内で繰り返し使われる処理をまとめたもの.

- メソッドとは、  
  関数の一種で、特定のオブジェクトやクラスの動作や機能の処理をまとめたもの。

- 引数とは、  
  関数やメソッドに渡される値や変数のこと。  
  入力データ。パラメーターとも呼ばれる。

- 戻り値とは、  
  関数が処理結果を返す出力データ。  
  「変数=関数(引数)」とすると戻り値を変数に代入できる。  
  return 文を使い、戻り値を指定することもできる。

```bash
hello() {
  echo "Hello, $1 and $2 !"
}

hello John Mike
```

のように引数を指定すると

```bash
$ ./スクリプトファイル名
Hello, John and Mike !
```

と出力される。

# return 文とは

return 文とは、シェル関数を終了するコマンド。

- 終了ステータスが「0」なら正常終了。  
  0 以外なら異常終了とみなされる。
- シェル関数の return では、終了ステータス（0〜255 までの数値）のみしか返せない。

- exit コマンドは、呼び出されたその場でシェルスクリプトを終了する。  
  return 文は、呼び出し元の関数に戻り値を返しその関数を終了する。

```bash
func() {
  if [ "$1" = "success" ]; then  #引数が”success”と同じなら
   return 0
  else            #それ以外なら
   return 1
 fi
}

func "success"          #引数を変更すると終了ステータスが変わり
  if [ $? -eq 0 ]; then         #0と同じなら
    echo "成功"
  else                #0以外なら
    echo "失敗"
  fi
```

```bash
  $ ./スクリプトファイル名
  成功
```

---

### 参考にしたサイト

- https://eng-entrance.com/linux-shellscript-function
- https://qiita.com/kaw/items/034bc4221c4526fe8866
- https://zenn.dev/suiudou/articles/1cfecfc41261fc
- https://qiita.com/ko1nksm/items/2c5543744cebd4fb1e61
- https://labex.io/ja/tutorials/shell-bash-function-return-values-391153
