# HTTPについて

## 歴史を振り返る

### Internetの起源
- ARPANET
  - パケット交換方式による通信
  - 今日のInternetで使われている技術の元となるものが開発された
  - RFC 1(https://tools.ietf.org/html/rfc1)
    - 2019/4/7がRFC 1から50年
    - https://note.mu/usop/n/nf859078fd898
    - 少数のHOSTでパケット通信するプロトコル
- TCP/IP
  - ARPANETの登場以降、同じようなネットワーク(ハードウェアやプロトコル)が乱立してきた
  - 特定のものに依存しないようオープンなプロトコルを作る必要があった
  - RFC 675(https://tools.ietf.org/html/rfc675)
    - SPECIFICATION OF INTERNET TRANSMISSION CONTROL PROGRAM
    - TCPの元で、初めてInternetという言葉が出てきた
  - 以降周辺のプロトコルが策定されていった


### World Wide Webの起源
- Hypertextの構想は以前よりあったが、ティム・バーナーズ＝リーがHypertextとInternetを組み合わせるというブレイクスルーを起こした
- この過程でURIという現代のWebの根幹を担う技術が開発された
- ティム・バーナーズ＝リーが行った提案(Information Management: A Proposal)は1989/3/12に執筆されたため、2019年はWeb生誕30驟雨年
- https://blog.cloudflare.com/happy-birthday-to-the-web/


2019年はInternet生誕50周年、Web生誕30周年のAnniversary Year



## HTTPの誕生

- 1990/11/12にティム・バーナーズ＝リーがWorld Wide Webをより具体化した提案を行った(https://www.w3.org/Proposal)
- そして世界で最初のWebサーバとWebブラウザが誕生した
- このときに使っていたプロトコルが(当然のことながら)HTTP
- 1991年にHTTP/0.9として初めてドキュメント化された(1.0ができたらか0.9と呼ばれるようになった)
- 以降、このHTTPが如何に巨大な仕様になっていったかを説明


## HTTP/0.9

- ドキュメントをGETするだけのプロトコル(=GETメソッドしかない)
- GETリクエスト -> htmlドキュメントがレスポンスされる -> 切断 のみ
- ドキュメントをGETするためのものなので、検索機能(`<isindex>`タグ)もあった
  - isindexタグはすでに廃止されている


### HTTP/0.9の課題

- ダウンロードするコンテンツのフォーマットをサーバから伝える手段がない
- クライアント側からはシンプルなGETとそれに付随する検索しかリクエストを送れない
- データの送信、更新、削除などができない


## HTTP/0.9のアップグレード版

- HTTP/1.0が策定される前に、メールやニュースグループのプロトコルを取り込み大きなアップグレードがあった(バージョニングはされていない)
- https://www.w3.org/Protocols/HTTP/HTTP2.html


### 追加された内容

#### ヘッダ追加(リクエスト、レスポンスの両方)

- メールプロトコルが起源
- サーバ、クライアント間での追加情報や指示を事前に伝えることが目的
- User-Agent, Referer, Content-Type, Content-Length, Contetn-Encodingとか

#### ボディ
- メールプロトコルが起源
- ヘッダーが追加されたので、リクエスト/レスポンスの中身はボディになった

#### メソッド
- ニュースグループのプロトコルが起源
- GET, HEAD, POSTや、今では使われていないものも提案されている

#### レスポンスに3桁のステータスが追加された
- ニュースグループのプロトコルが起源

#### リダイレクト

#### URL
- Locationを表すURLの構造がRFCとして定義された


## HTTP/1.0

- HTTP/0.9のアップグレード版を経て、1996年に仕様策定された
- アップグレード版がほぼ1.0とも言っていい内容だが、フォームとキャッシュ周りが整理されている

### フォーム

- x-www-form-urlencoded
  - フォーム(POST)を使ってサーバにデータを送信するときはContent-Typeにapplication/x-www-form-urlencodedを設定する
  - ブラウザは区切り文字などを変換(URLエンコード)してデータを送信する
- multipart/form-data
  - ファイル送信を行うためのフォームオプション
  - HTTPの1リクエストで複数のデータを送るため、データの境界を表すboundaryオプションがつく

### キャッシュ

- 一つのページ表示に必要なファイルが増えてきたため、ダウンロード済みファイルは再取得しないという仕組み
- Last-Modified/If-Modified-Sinceヘッダ
  - ブラウザキャッシュ済みであればサーバは304を返す
- Expiresヘッダ
  - キャッシュ済みであればリクエストを出さない
- Pragma:no-cache
  - プロキシサーバに対して、オリジンまでデータを取りに行くことを支持するもの
  - HTTP/1.1のCache-Controlに置き換わった
- 確実にキャッシュさせないようにするの難しい


## HTTP/1.1

- HTTP/1.1はHTTP/1.0の翌年に最初のバージョンが策定された
- 現役のプロトコルであり、改定などが多く行われていた

### Keep-Alive

- HTTPというようりTCP/IPの通信を効率化する仕組み
- TCP/IP上の1つのコネクションを使いまわして複数回のHTTPの通信を行うようなもの
- Keep-Aliveがなければ、1回のHTTPリクエスト・レスポンス毎にTCPの接続が新しく行われてしまう
- 仕様上はブラウザ-サーバ間のコネクションは2つが推奨されているが、ブラウザ実装的に6つが一般的なはず
- HTTP/2はKeep~Aliveが前提のため、Keep-Aliveヘッダはない

### TLS(SSL)

- SSL3.0を元に標準化された通信路を暗号化する規格
- 暗号化自体はHTTPに依存するものではない(HTTP以外でも利用できる)
- TLSのバージョンは1.0〜1.3まであり、1.0、1.1は非推奨

### チャンク

- サーバから小さい単位でファイルを送る仕組み(multipartはブラウザ->サーバ)

### Upgrade

- HTTPのセッションが確立したあと別プロコトルのセッションに再利用するための機構
- TLS, WebSocket, HTTP/2とか

### その他

- 新しいメソッド(OPTIONS/TRACE/CONNECTION)
- Cache-Control
- Cookie


## HTTP/2

- HTTP/1.1とはちょっとレイヤーが違う。感覚的にTCPとHTTPの間にあるようなもの
- HTTP/2のベースはSPDYというGoogleが開発したプロトコル
- HTTP/2が策定されたことで、SPDYは役目を終えた
- 最初はHTTP/2.0だったが、次に変更があるときはHTTP/3だろう、ということで.0がなくなった(それだけ議論されたもの)

### SPDY(HTTP/2)が生まれた背景

- モチベーションはWebを早くすること
  - 1ドメインに対して6接続しか貼れないような状況ではつらい
- GoogleはYoutubeのような巨大なトラフィックを生むプラットフォームとChromeを持っている
- 新しいプロトコルの実験をできるのはGoogleぐらいしかいない

### ストリーム

- HTTP/2の一番大きな変更点はバイナリベースのプロトコルになったこと
- 1つのTCP接続の内部にストリームという仮想のTCPソケットを作って通信を行う
- このストリームにはハンドシェイクは不要で、TCPの通信容量が大丈夫であれば数万接続とかはれる
- 送られるデータはフレームという小さい単位に分割される(MACフレームとは違う)
- フレームにはIDがあるので、どのリクエストとレスポンスが対応しているかがわかるので、並列化・全重通信とかができる


### アプリケーション層

- HTTP/2は、TCP接続の中にもう一つTCP接続を作っているようなものなので、アプリケーション層的なものが必要
- このプロトコル(インターフェイスとでもいうか)がHTTP/1.1(を元にしたもの)
- ヘッダーはHEADERフレーム、ボディはBODYフレームのような形でフォーマットは変わっている
- HTTP/1.1では、ヘッダーの終端を見つけるには空行まで1バイトずつ先読みする必要があったが、HTTP/2ではバイナリプロコルになったので最初にフレームサイズが入っている

### フローコントロール

- TCPのフロー制御のような仕組みも、HTTP/2に定義されている
- パケットの順番や再送等はTCPのしごとなので、HTTP/2では輻輳(ネットワーク上に流すパケット量の制御)を担う
- https://qiita.com/Jxck_/items/622162ad8bcb69fa043d

### サーバプッシュ・プリロード

- 確立したストリーム内であればハンドシェイクは不要なので、リクエストを待たずにサーバからクライアントに送ることができる
- 以下のような記述でプリロードや優先度制御などもできる

```
<!-- DNSの名前解決だけを先に行う -->
<link rel="dns-prefetch" href="//api.example.com">

<!-- DNSの名前解決、TCPハンドシェイク、TLSハンドシェイクを先に行う -->
<link rel="preconnect" href="//cdn.example.com" crossorigin>
```

```
<meta charset="utf-8">
<title>JS and CSS preload example</title>
<!-- プリロード -->
<link rel="preload" href="style.css" as="style">
<link rel="preload" href="main.js" as="script">
<!-- CSSを実際に使う -->
<link rel="stylesheet" href="style.css">
```

### HPACK

- HTTPヘッダは同じような記述が多くなるため、圧縮することで通信容量を減らせる
- よく使われるヘッダー文字列は予め静的テーブルで予め定義されている


## QUIC

- HTTP/2はあくまでもTCP上で動くプロコトル
- TCPは大変誠実なプロコトル
  - 輻輳制御のために最初は少量のパケット(ウィンドウサイズ)を送る(スロースタート)
  - 接続をやり直すたびにウィンドウサイズをリセットする
  - 輻輳が発生したらウィンドウサイズを小さくする
- TCPはハンドシェイクのコストが高い
- TCPはOSのカーネルレベルの実装
  - カジュアルにいじれない
  - 変更できたとしても全デバイスに浸透するまでに相当な時間がかかる
- じゃあUDPでやろう => QUIC


## QUIC

- GoogleはUDP上で動くWebを実現するためにQUICを開発した
- QUICは再送処理、輻輳制御などを自前実装している
- すべての通信はTLS1.3で暗号されている
- QUICはハンドシェイクのコスト下げ、HTTP/2とTCPで競合していたフローコントロールの機能も統合している
- QUICはセッションの中に複数の疑似セッション(ストリーム)をはる
- ストリーム内部でのパケットの順序は保証するが、ストリーム間では保証しない
- QUICはコネクションIDというものを保持しているため、LTE -> Wifiのようにネットワークが変わってもコネクションは維持される

## HTTP/3

- 昨年HTTP over QUICが晴れてHTTP/3となるとアナウンスされた(https://daniel.haxx.se/blog/2018/11/11/http-3/)
- HTTP/3とはQUIC上で動かすHTTPのこと
- https://http3-explained.haxx.se/ja/h3-https.html
- HTTP/3の勉強はこれから...


## 参考

- https://www.oreilly.co.jp/books/9784873118789/
- http://jxck.hatenablog.com/entry/http2-rfc7540
- https://ja.wikipedia.org/wiki/%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%BC%E3%83%8D%E3%83%83%E3%83%88%E3%81%AE%E6%AD%B4%E5%8F%B2
- https://ja.wikipedia.org/wiki/World_Wide_Web
- https://ja.wikipedia.org/wiki/Hypertext_Transfer_Protocol
- https://www.nic.ad.jp/ja/newsletter/No66/0320.html
