# 【Git】git commit コマンド

Git のコミットに関するコマンドをまとめてみました。
commit とはステージングの後、ローカルディレクトリに保存するためのコマンドです。

---

## 1.記録

### 基本的なコミット

`git commit`

 ステージングしたファイルを保存する。これを実行するとエディタが開きコミットメッセージを入力し保存するとコミットが実行される。

### メッセージ付コミット

`git commit -m "コミットメッセージ”`

指定したコミットメッセージで、ステージングしたファイルを保存する。

### 全てのファイルをコミット

`git commit -a`

 git addコマンドによって履歴に追加されたことがあり、修正のある全てのファイルを、ステージングして保存する。

## 2.修正

### コミットの修正

`git commit --amend`

 直前のコミットを修正する。

## 3.削除

### コミットの取消

`git reset --soft HEAD^`

 直前のコミット(ローカルリポジトりへの変更)を取り消す。

---

## 参考にしたサイト

- https://ccg-wheads.jp/journal/article-438/
- https://www.atlassian.com/ja/git/tutorials/saving-changes/git-commit
- https://codelikes.com/git-commit/
