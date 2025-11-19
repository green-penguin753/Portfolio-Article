# 【Git】でよく使う用語集

# Git について

Git とは、ファイルの分散型バージョン管理システムの一つで、複数人で開発をする際に便利なツールです。

- 新旧ファイルの一元管理ができる。
- ファイルの変更履歴を共有できる。
- 簡単に過去のファイルに戻せる。
- 複数人の修正を１つに統合できる
- ネットワーク接続なしでも開発作業ができる。

ユーザーはローカルリポジトリで作業を行い、作業を終えたらリモートリポジトリに反映します。

---

# 用語

#### リポジトリ(repository)

ファイルや変更履歴を保存しておく保管場所のこと。<br>
リモートリポジトリとローカルリポジトリの 2 種類がある。
・リモートリポジトリは、ネットワーク上に存在し、ファイルや変更履歴を共有する際に使う。<br>・ローカルリポジトリは、自分のコンピュータ上に存在し自分専用のリポジトリ。ここで作業を行う。

#### ブランチ(branch)

日本語で枝、分岐という意味。<br>
開発の本流のブランチから分岐させることにより、<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">他のブランチに影響を与えず開発を行える機能</span>のこと。複数人が同時並行で作業できる。git branch コマンドによって実行される。
本流のブランチは master ブランチと呼ばれ、プログラムの修正や機能の追加を行う際は、ブランチを追加しそれぞれブランチで作業をする。作業後は他のブランチに統合(merge）し、一つのブランチにまとめ直すことができる。
・統合ブランチとは、トピックブランチの分岐元として使用する本流のブランチ。通常、master ブランチを統合ブランチとして使用する。<br>・トピックブランチとは、作業を行うために追加したブランチのこと。通常、統合ブランチから分岐する形で作成する。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎その他の用語☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">
・「ブランチを切る」...ブランチを分岐・追加すること。</div>

#### ステージング(staging)

ローカルリポジトリに<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">コミットする前に、変更したファイルを選択して準備する作業</span>のこと。<br>
git add コマンドによって実行される。別名コミット予定。
ワークツリーで作業したファイルをステージングして、その後ローカルリポジトリにコミットする。

- コミットしたい特定の変更だけインデックスに追加できる。（一つのファイルの中の特定の行だけをステージングすることもできる。）
- コミット前の最終確認や、システムやソフトウェアのテストや検証を行うためにも使える。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎その他の用語☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">・ワークツリー(working tree)...作業中のファイルやフォルダのこと。別名作業ディレクトリ。<br>
・インデックス（index）...コミットするためのファイルを登録するスペースのこと。別名ステージングエリア</div>

#### コミット(commit)

新規作成したファイルや編集ファイルを<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">ローカルディレクトリに保存</span>すること。実行するとファイルの編集内容・日時・作業者・コミットメッセージを記録したファイルが保存される。
git commit コマンドによって実行される。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎関連☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">git tag...コミットに対しタグをつけられるコマンド</div>

#### プッシュ(push)

ローカルディレクトリから<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">リモートディレクトリにアップロードし保存</span>すること。
git push コマンドによって実行される。<br>
プッシュ前にプルを行い競合(コンフリクト)を解決してからプッシュが推奨される。

#### プル(pull)

リモートディレクトリからローカルディレクトリにダウンロードし反映させること。
git pull コマンドによって実行される。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">
☀︎その他の用語☀︎
</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">
・フェッチ(fetch)..リモートリポジトリの最新の履歴の取得のみ行う。<br>
・マージ(merge)...ブランチを統合する<br>
・クローン(clone)...リモートリポジトリをまるまる複製する。<br>
・リベース(rebase)...ブランチを統合する。コミット履歴を上書きする。
</div>

#### チェックアウト(checkout)

ブランチの切り替えやファイルの復元をする。

git checkout コマンドによって実行される。

#### ディフ(diff)

指定した二つのファイルを比較してその違い(差分)を表示する。
git diff コマンドによって実行される。

#### ログ(log)

リポジトリのコミットの履歴を表示をする。
git log コマンドによって実行される。

#### スタッシュ(stash)

一時保存する
git stash コマンドによって実行される。

#### チェリーピック(cherry-pick )

必要なコミットだけをコピーできる。
git cherry-pick コマンドによって実行される。
