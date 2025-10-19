# 【Git】git diff コマンド

Gitのディフに関するコマンドをまとめてみました。<br>
git diff コマンドは指定した二つのファイルを比較してその違い(差分)を表示するコマンドです。<br> +マーク...追加された行<br> -マーク...削除された行

---

## 1.差分

### ワークツリーの差分

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git diff
</div>
ワークツリーとステージングエリアの差分を表示する。<br>
-wオプションをつけると空白や改行の変化を無視して表示する。

### HEAD との差分

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git diff HEAD
</div>
ワークツリーと現在ブランチの最新コミットとの変更内容を表示する。

### ステージングエリアの差分

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git diff --cached
</div>
ステージングエリアとHEADの差分を表示する。

### 指定したファイルの差分

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git diff <ファイル名>
</div>
指定したファイルの変更内容を表示する。

### コミット間の差分

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git diff <コミットID> <コミットID>
</div>
指定した2つのコミット間の変更内容を表示する。<br>
ブランチ間でも使える。

## 2.表示

### ファイル一覧表示

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git diff --name-only
</div>
差分のあるファイルの一覧を表示する。

---

## 参考にしたサイト

- [https://www.r-staffing.co.jp/engineer/entry/20200228_1]
- [https://qiita.com/kome1996/items/f6fb0671b633711fbbc3]
- [https://qiita.com/mamao/items/2e103c3fba9d1b058961]
