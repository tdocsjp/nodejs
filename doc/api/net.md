---
title: Net（概要）
source: https://nodejs.org/api/net.html
---

# Net（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:net` モジュールは、ストリームベースの TCP または IPC（プロセス間通信）のサーバー・クライアントを作成するための非同期 API を提供します。

## 主な関数

| 関数 | 概要 |
|---|---|
| `net.createServer([options][, connectionListener])` | 接続を待ち受ける TCP または IPC サーバーを作成する |
| `net.createConnection()` / `net.connect()` | サーバーへの接続を確立し、`net.Socket` インスタンスを返す |

## 主なクラス

| クラス | 概要 |
|---|---|
| `net.Server` | 接続を受け付け、接続済みの `net.Socket` を伴う `'connection'` イベントを発火する TCP/IPC サーバー |
| `net.Socket` | TCP ソケットまたは IPC のエンドポイントを表す。`stream.Duplex` を継承し、双方向のデータ通信を扱う（`'connect'`・`'data'`・`'error'`・`'close'` などのイベントを持つ） |
| `net.BlockList` | `addAddress()`・`addRange()`・`addSubnet()`・`check()` などのメソッドで、受信・送信の IP アドレスのブロックルールを管理する |
| `net.SocketAddress` | `address`・`port`・`family`・`flowlabel` などのプロパティを持つソケットアドレスを表す |

## 未翻訳

各クラス・メソッドの詳細な引数仕様、Unix ソケットの扱い、`net.BoundSocket` の詳細などは未翻訳。

---

本ページは [nodejs.org/api/net](https://nodejs.org/api/net.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/net.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
