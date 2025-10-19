# 【Docker】Docker の用語とコマンド

# Docker の用語

#### docker(ドッカー)とは

環境(開発・本番など)の<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">設定を簡単に構築</span>でき、  
また、<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">環境が違っても同じように動作させることができるツール</span>。

- コンテナと呼ばれる隔離された環境で作業ができる。

- 複数のコンテナを作れるため、  
  作業を分散して開発ができたりサーバーへのアクセスを分散できる。

- 軽量で高速に起動ができ、仮想マシンよりも効率的に使用できる。

- docker-compose も使用することで、  
  複数のコンテナを同時に管理・連携させることができる。

#### images(イメージ)とは

アプリケーションの実行に<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">必要な設定ファイルをまとめたテンプレート</span>。  
（アプリケーション本体、ライブラリ、フレームワーク、基本コマンドなど）

- Docker コンテナを作成するための設計図。
- イメージが１つあれば同じコンテナを量産することができる。

#### container(コンテナ)とは

一つの OS 上で、CPU・メモリ・プロセス空間などが<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">独立した仮想環境</span>のこと。

- Docker イメージをもとに作成される。

#### volume(ボリューム)とは

コンテナが作ったデータを保存する場所。

- コンテナが消えてもデータを残すことができる。

#### service(サービス)とは

作業ごとの<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">環境(コンテナ)の集まり</span>のこと。

- Docker Compose などを使い複数のコンテナを連携させることで、サービスを構築する。  
  （アプリケーション開発しながら、データベース環境からデータを取得するなど）

# Docker コマンド

## 1.コンテナ管理

##### コンテナの起動

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
docker-compose up
</div>
複数のコンテナを一斉に起動する。   
コンテナ1つだけのときは`docker container start`でも可能。

##### コンテナの停止

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
docker-compose down
</div>
複数のコンテナを一斉に停止する。   
コンテナ1つだけのときは`docker stop コンテナ名` でも可能。

##### コンテナを表示

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
docker ps -a
</div>
全てのコンテナを表示する。(停止中も含む).   
詳細表示は`docker container inspect コンテナ名`

##### コンテナを削除

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
docker rm コンテナ名
</div>
コンテナを削除する。(停止中のものしか削除できない)

## 2.イメージ管理

##### イメージをダウンロード

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
docker image pull [オプション]　イメージ名
</div>
Docker Hubなどからイメージをダウンロードする。

##### イメージを組み立てる

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
docker build -t イメージ名 .
</div>
Dockerfileを使用してイメージをビルドする。   
`docker container run `はコンテナを新規作成して起動する。

##### イメージを表示

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
docker image ls [オプション]
</div>
ローカル(ダウンロード済み)のイメージを一覧表示する。

##### イメージを削除

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
docker image rmi [オプション]　イメージ名
</div>
イメージを削除する。

## 3.その他

##### Docker のバージョン確認

<div style="border: 2px solid #ccc; padding: 10px; box-shadow: 2px 2px 4px rgba(0,0,0,0.3);">
docker -v
</div>

Docker システム全体の情報を表示したいときは`docker info`

---

### 参考にしたサイト

- https://qiita.com/Sicut_study/items/4f301d000ecee98e78c9
- https://di-acc2.com/system/23034/
- コマンドhttps://qiita.com/JK447/items/bed378680eee49c5f600
- 公式のコマンドhttps://matsuand.github.io/docs.docker.jp.onthefly/engine/reference/commandline/docker/.
- Docker&仮想サーバー完全入門　リブロワークス著
