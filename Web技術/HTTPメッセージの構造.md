# 【Web】HTTP メッセージの構造

HTTP リクエストと HTTP レスポンスをまとめて、HTTP メッセージという。

# HTTP リクエスト

HTTP リクエストとは、Web ブラウザから Web サーバーへの要求のこと。
URL の形式で送信される。

#### ① リクエスト行・・・一行目

Web サーバーに対してどのような処理を依頼するのかを伝える情報が含まれている。  
例：GET /index.html HTTP1.1

- <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">HTTP メソッド</span>とは、Web ブラウザが Web サーバーに要求する処理の種類を表す。
  - **GET メソッド**・・・HTML ファイルなどコンテンツを取得したい場合。検索機能。
  - **POST メソッド**・・・データを Web サーバーに送信する場合。個人情報を含むフォームの送信。
  - HEAD メソッド・・・HTTP ヘッダーの情報のみ取得したい場合。
  - その他「PUT」「DELETE」「CONNECT」などがあるが、サーバー側で利用制限されていることが多い。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎「GET」と「POST」はデータの送り方が異なる☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">
GETメソッドでは、  
URLの末尾に「?パラメーター＝値」をつけて送信するため、Webブラウザの閲覧履歴にユーザー名やパスワードが残ってしまう。<br>
POSTメソッドでは、  
情報をメッセージボディ内に記録して送信する履歴に残らないので機密性が高い。</div>

- <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">パス名</span>とは、サーバー上にあるリクエスト対象のデータのこと。

- <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">HTTP プロトコルのバージョン</span>
  例：HTTP1.1

<br>

#### ② メッセージヘッダー・・・二行目以降

HTTP リクエストの詳細情報が表示される。

- ヘッダーフィールドは、フィールド名、コロン(:)、１文字空白、フィールド値で構成される。  
  例：Date: Sun, 01 Jan 2017 00:00:00 GMT
- メッセージヘッダーは、複数のヘッダーフィールドと呼ばれる行から成り立っており、どのヘッダーフィールドを使うかは状況に応じて選択される。

- 大きく 4 種類に分けられる。
  - **一般ヘッダーフィールド**・・・HTTP メッセージ全体に対しての付加情報を示す。「Date」
  - **リクエストヘッダーフィールド**・・・HTTP リクエストのみに含まれるヘッダーフィールド。「Referer」「User-Agent」
  - **レスポンスヘッダーフィールド**・・・HTTP レスポンスのみに含まれるヘッダーフィールド。「Server」
  - **エンティティヘッダーフィールド**・・・メッセージボディに含まれるデータの付加情報を示す。「Content-Type」

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎代表的なヘッダーフィールド☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">
「Date」・・・HTTPメッセージが作成された日付を示す。<br>
<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">「Referer」</span>・・・直前に見ていたWebページのURLを示す。どこからそのページに要求が来たのかを知ることができるので、マーケティングやセキュリティ対策に利用される。<br>
「User-Agent」・・・Webブラウザの固有情報(プロダクト名・バージョンなど)を示す。<br>
「Server」・・・Webサーバーの固有情報を示す。<br>
<span style="background: linear-gradient(transparent 60%, #ffff00 60%);">「Content-Type」</span>・・・コンテンツの種類を指定する。
ボディにあるデータがHTMLなのか画像なのかや、文字エンコードなどの情報を示す。
</div>

<br>

#### ③ 空白行

1 行空けることで、メッセージヘッダーとリクエストボディを分けている。

<br>

#### ④ リクエストボディ

補足のメモ書きスペース。  
データ送信を伴うリクエスト（例：POST メソッドのとき）などで利用される。  
GET メソッドのときなど空の場合もある。

# HTTP レスポンス

HTTP レスポンスとは、
Web サーバーが受け取った HTTP リクエストを処理して、その結果を Web ブラウザに返すこと。

#### ① ステータス行・・・一行目

Web サーバー内での処理の結果情報を伝えている。  
例：HTTP1.1 200 OK

- <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">HTTP プロトコルのバージョン</span>
  例：HTTP1.1

- <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">HTTP ステータスコード</span>とは、
  HTTP リクエストに対する Web サーバー内での処理結果。３桁の数字からなる。

  - 1xx・・・処理中。リクエストの継続中。
  - 2xx・・・成功
  - 3xx・・・リダイレクト。転送など追加の処理が必要。
  - 4xx・・・クライアントエラー
  - 5xx・・・サーバーエラー

- <span style="background: linear-gradient(transparent 60%, #ffff00 60%);">テキストフレーズ</span>とは、
  ステータスコードに対応した語句のこと。

<div style="height: 12px;"><span style="margin-left: 8px; padding: 6px 10px; background:#FBB161 ; color: #ffffff; font-weight: bold; border-radius: 5px;">☀︎代表的なステータスコード☀︎</span></div>
<div style="border: 2px solid#FBB161 ; padding: 25px 12px 10px; font-size: 1em; border-radius: 5px;">

「200」・・・OK 　リクエストが正常に受理されました。<br>
「404」・・・Not Found 　ページが見つかりません。<br>
「503」・・・Service Unavailable 　 Web サーバーに負荷がかかり表示できない。

</div>

<br>

#### ② メッセージヘッダー・・・二行目以降

HTTP レスポンスの詳細情報が表示される。  
HTTP リクエストと同じ。

<br>

#### ③ 空白行

1 行空けることで、メッセージヘッダーとレスポンスボディを分けている。  
HTTP リクエストと同じ。

<br>

#### ④ レスポンスボディ

HTML や画像等のデータが格納される。
