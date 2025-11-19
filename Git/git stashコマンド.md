# 【Git】git stash コマンド

Git のスタッシュに関するコマンドをまとめてみました。<br>
stash とは、現在のワークツリーの変更を一時的に保存(退避)させるコマンドです。
まだコミットしていない変更を中断し、別の作業に切り替える際に便利です。

---

## 1.一時保存

### 基本的な退避

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git stash save "メッセージ"
</div>
現在の変更作業を退避する。「git stash save」をよく使用する。
(save "メッセージ"はつけなくても可)

## 2.表示

### 一覧表示

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git stash list
</div>
退避した作業の一覧を表示する。

## 3.作業に戻る

### 退避した作業に戻る

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git stash apply
</div>
退避した作業に戻る。<br>
「git stash pop」は戻した作業が退避一覧から削除される。<br>
「git stash pop --index」はgit stashで退避し、ステージング状態を維持した状態で戻るためのコマンド。

### 削除

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git stash drop （<削除したい作業>はつけなくても可）
</div>
退避一覧から指定した作業を削除する。<br>
全削除は「git stash clear」

---

## 参考にしたサイト

- [https://tech-blog.rakus.co.jp/entry/20211012/git]
- [https://backlog.com/ja/git-tutorial/reference/stash/#section1]
