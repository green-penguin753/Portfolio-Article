# 【Git】git checkout コマンド

Gitのチェックアウトに関するコマンドをまとめてみました。
git checkout コマンドは作業するブランチを切り替え、ファイルの復元、特定コミットへの移動など多機能なコマンドです。

---

## 1.切り替え

### ブランチ切り替え

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git checkout <ブランチ名>
</div>
現在のブランチから、指定したブランチに切り替える。

### ブランチ新規作成&切り替え</h3>

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git checkout -b <新しいブランチ名> 　
</div>
現在のブランチから、新しいブランチを作成し切り替える。<br>
特定のコミットからブランチを作成したい場合<コミット名>も追加する。

### リモートブランチから新規作成&切り替え

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git checkout -b <新しいブランチ名> origin/<リモートブランチ名>
</div>
指定したリモートブランチの最新の状態を基にして、新しいローカルブランチを作成し、切り替える。

### 履歴のないブランチを作成

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git checkout --orphan <新しいブランチ名>
</div>
既存の履歴に影響を与えず作業できるブランチを新規作成する。

## ファイル復元

### コミット時の状態に戻す

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git checkout <コミットID>（<ファイル名>はつけなくても可）
</div>
指定したコミット時点のファイルの状態に、作業ディレクトリを戻す。

### 特定のブランチからファイルを復元

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git checkout <ブランチ名> <ファイル名>
</div>
他のブランチの特定のファイルの状態を、現在のブランチにコピーする

---

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎コミットID（コミットハッシュ）とは☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">コミットごとにつけられた英数40桁のIDのことで「git log」コマンドで確認できる。<br>
先頭７桁をショートコミットハッシュといい「git log --oneline」で確認できる。通常こちらを使う。</div>

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎コマンド機能分割☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">・git switchコマンド...ブランチの切り替えや新規作成。<br>
- git restoreコマンド...作業ディレクトリやステージングエリアのファイルの変更や復元</div>

---

## 参考にしたサイト

- [https://backlog.com/ja/git-tutorial/stepup/08/]
- [https://envader.plus/article/300]
- [https://qiita.com/mamao/items/2e103c3fba9d1b058961]
