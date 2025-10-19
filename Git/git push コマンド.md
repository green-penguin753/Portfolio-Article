# 【Git】git push コマンド

Gitのプッシュに関するコマンドをまとめてみました。
git push コマンドはローカルリポジトリからリモートリポジトリへ反映させるコマンドです。
基本的にリモートにある同名のブランチに push されます。競合が発生するような場合は、push が拒否されます。

---

## 1.プッシュ

### 基本的なプッシュ

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git push <リモート名> <ブランチ名>
</div>
ローカルリポジトリにある変更したブランチをリモートリポジトリに反映させる。

### 全てのブランチをプッシュ

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git push --all <リモート名>
</div>
ローカルリポジトリにある全てのブランチを反映させる。

### 強制的にプッシュ

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git push -f <リモート名> <ブランチ名> (--forceでも可)
</div>
強制的にブランチを反映させる。競合が発生していても上書き可能なため注意が必要。「git push origin main --force」は禁忌。

## 2.削除

### ブランチを削除

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git push --delete <ブランチ名>
</div>
リモートリポジトリから、指定したリモートブランチを削除する。<br>
<a href="#">プルリクエスト</a>後、マージができたらpushしたブランチを削除するときにも使える。

## 3.表示

### シュミレーションする

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git push --dry-run <リモート名> <ブランチ名>
</div>
ドライラン。実際にはプッシュせずに、何が起こるかを確認できる。

## 4.その他

### push 操作の簡略化

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git push -u <リモート名> <ブランチ名>
</div>
ローカルブランチをリモートブランチに反映すると同時に、追跡関係を設定する。<br>
以降のpush操作でブランチ名を指定不要になり、効率的・操作の簡素化が可能。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎プルリクエスト☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">プルリクは自分の行った変更をリポジトリに取り込んでもらうために行う機能。<br>
レビューが返ってきたらmergeをする。<br>
「git push <リモート名> <リクエストを出すブランチ名>」
</div>

---

## 参考にしたサイト

- [https://yama-weblog.com/how-to-delete-remote-branch-in-git-command/]
- [https://www-creators.com/archives/1472]
