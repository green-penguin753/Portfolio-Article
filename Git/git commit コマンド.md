# 【Git】git commit コマンド

Git のコミットに関するコマンドをまとめてみました。
commit とはステージングの後、ローカルディレクトリに保存するためのコマンドです。

---

## 1.記録</h2>

### 基本的なコミット

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git commit
</div>
 ステージングしたファイルを保存する。これを実行するとエディタが開きコミットメッセージを入力し保存するとコミットが実行される。

### メッセージ付コミット

git commit -m "コミットメッセージ”

指定したコミットメッセージで、ステージングしたファイルを保存する。

### 全てのファイルをコミット

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git commit -a
</div>
 git addコマンドによって履歴に追加されたことがあり、修正のある全てのファイルを、ステージングして保存する。

## 2.修正</h2>

### コミットの修正

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git commit --amend
</div>
 直前のコミットを修正する。

## 3.削除</h2>

### コミットの取消

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git reset --soft HEAD^
</div>
 直前のコミット(ローカルリポジトりへの変更)を取り消す。

---

## 参考にしたサイト</h2>

- [https://ccg-wheads.jp/journal/article-438/]
- [https://www.atlassian.com/ja/git/tutorials/saving-changes/git-commit]
- [https://codelikes.com/git-commit/]
