# 【Git】git stash コマンド

Git のスタッシュに関するコマンドをまとめてみました。
stash とは、現在のワークツリーの変更を一時的に保存(退避)させるコマンドです。
まだコミットしていない変更を中断し、別の作業に切り替える際に便利です。

---

## 1.一時保存

### 基本的な退避

`git stash save "メッセージ"`

現在の変更作業を退避する。「git stash save」をよく使用する。
(save "メッセージ"はつけなくても可)

## 2.表示

### 一覧表示

`git stash list`

退避した作業の一覧を表示する。

## 3.作業に戻る

### 退避した作業に戻る

`git stash apply`

退避した作業に戻る。
「git stash pop」は戻した作業が退避一覧から削除される。
「git stash pop --index」は git stash で退避し、ステージング状態を維持した状態で戻るためのコマンド。

### 削除

`git stash drop <削除したい作業>`

退避一覧から指定した作業を削除する。
全削除は「git stash clear」
<削除したい作業>はつけなくても可

---

## 参考にしたサイト

- [https://tech-blog.rakus.co.jp/entry/20211012/git]
- [https://backlog.com/ja/git-tutorial/reference/stash/#section1]
