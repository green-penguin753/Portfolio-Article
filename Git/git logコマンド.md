# 【Git】git log コマンド

Git のログに関するコマンドをまとめてみました。<br>
git log コマンドはコミットの履歴を表示し、確認・分析できるコマンドです。

---

## 1.表示

### 基本的な表示

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git log
</div>
コミットの履歴を表示する。

### 簡潔な形式で表示

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git log --oneline
</div>
コミット履歴を一行を表示する。

### 特定のファイルで表示

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git log <ファイル名>
</div>

指定したファイルのコミット履歴を表示する。

### 表示するコミット数を指定

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git log -n
</div>
検索・表示するコミット履歴の数を指定し表示する。

### キーワードを含むコミット履歴表示

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
git log --grep='キーワード'
</div>
指定した文字列が含まれるコミット履歴を抽出・表示する。

---

## 参考にしたサイト

- [https://www.kagoya.jp/howto/rentalserver/webtrend/gitlog/]
