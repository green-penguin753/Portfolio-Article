# 【Git】git pull コマンド

Gitのプルに関するコマンドをまとめてみました。<br>
pull とは、リモートディレクトリからローカルディレクトリにダウンロードし反映させるコマンドです。<br>(正確にはリモートブランチからリモート追跡ブランチ(origin/master)へ反映された後に、そのリモート追跡ブランチからローカルブランチへ統合されているという流れで、fetch と merge を行っています。)
他のユーザーが行った変更を取り込み常に最新の状況を保つことは、競合を避けスムーズな開発ができます。

---

## 1.プル

### 基本的なプル

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git pull <リモート名> <ブランチ名>
</div>
リモートブランチからローカルブランチに変更を反映させる。

### マージの代わりにリベースしてプル

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git pull --rebase (<リモート名> <ブランチ名>はつけなくても可)
</div>
リモートブランチからローカルブランチに変更を反映させる。<br>
マージコミットを残さないので履歴が複雑にならないが、あまり使わない。

### プルの前にスタッシュ

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git pull --autoshash
</div>
自動的に現在の変更を一時保存してから、プルを行う。

## 2.取消

### マージの取消

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git revert commitID
</div>
打ち消すようなコミットを新しく作成する。コミットと打ち消した履歴の両方が残る。

### マージ前の状態に戻す

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git merge --abort
</div>
merge操作で競合が発生したので、mergeする前の状態に戻すコマンド。

## 3.表示

### 基本的なフェッチ

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git fetch <リモート名> (<ブランチ名>はつけなくても可)
</div>
指定したリモートリポジトリから、すべてのブランチの最新の状態を取得できる。作業ディレクトリには影響を与えない。

### 詳細の表示

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git pull -v (または--verbose)
</div>
fetch操作やmerge操作、競合の詳細情報等が詳細に表示され、問題解決のときに便利。

---

## 参考にしたサイト

- [https://tech-blog.rakus.co.jp/entry/20220805/git]
- [https://backlog.com/ja/git-tutorial/stepup/14/]
