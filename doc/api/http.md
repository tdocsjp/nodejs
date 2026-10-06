---
title: HTTP（概要）
source: https://nodejs.org/api/http.html
---

# HTTP（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:http` モジュールは、HTTP のクライアント・サーバー両方のインターフェースを提供します。メッセージ全体をバッファせずにストリーミング処理できるよう、意図的に低レベルな API として設計されています。

## 主なクラス・関数

| 名前 | 概要 |
|---|---|
| `http.createServer([options][, requestListener])` | リクエストを待ち受ける HTTP サーバーを作成する |
| `http.request(options[, callback])` | 外部への HTTP リクエストを送信し、`ClientRequest` を返す |
| `http.get(url[, options][, callback])` | GET リクエスト用の簡易メソッド。自動的に `request.end()` を呼ぶ |
| `http.Server` | 受信した HTTP 接続を処理するサーバークラス。`'request'`・`'connect'`・`'upgrade'` などのイベントを発火する |
| `http.ClientRequest` | 送信中の HTTP リクエストを表す。最初のデータ送信または `end()` 呼び出しまではヘッダーを変更できる |
| `http.ServerResponse` | クライアントに送るレスポンスオブジェクト。`setHeader()` でヘッダー設定、`write()` で本文送信、`end()` で終了する |
| `http.IncomingMessage` | 受信した HTTP メッセージ（サーバー側ではリクエスト、クライアント側ではレスポンス）を表す。ヘッダー・本文・HTTP バージョン・ステータスコードにアクセスできる |
| `http.Agent` | HTTP クライアントの接続維持・ソケット再利用を管理する。`keepAlive`・`maxSockets`・`maxFreeSockets` などで設定可能 |

## 補足

HTTP の各インターフェースは意図的に低レベルであり、ヘッダーと本文の解析をユーザー側で分離して扱えるようになっている。これにより、巨大なメッセージやチャンク転送されるメッセージを、全体をバッファすることなくメモリ効率よく処理できる。

## 未翻訳

各クラス・メソッドの詳細な引数・イベント仕様、HTTP/1.1 のキープアライブやチャンク転送の挙動、エラーハンドリングの詳細などは未翻訳。

---

本ページは [nodejs.org/api/http](https://nodejs.org/api/http.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/http.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
