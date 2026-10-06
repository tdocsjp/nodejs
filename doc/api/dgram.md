---
title: UDP/datagram（概要）
source: https://nodejs.org/api/dgram.html
---

# UDP/datagram（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:dgram` モジュールは UDP データグラムソケットの実装を提供し、コネクションレスなメッセージベースのネットワーク通信を実現します。

## ソケットの作成

| 関数 | 概要 |
|---|---|
| `dgram.createSocket(options[, callback])` | オプション（type、reuseAddr、reusePort、ipv6Only、バッファサイズ、カスタム DNS lookup など）を指定して UDP ソケットを作成する |
| `dgram.createSocket(type[, callback])` | ソケットタイプ（`'udp4'` または `'udp6'`）を指定して UDP ソケットを作成する |

## `dgram.Socket` の主なメソッド

| メソッド | 概要 |
|---|---|
| `socket.bind([port][, address][, callback])` | 指定したポート・アドレスにバインドし、データグラムの受信を開始する |
| `socket.send(msg[, offset, length][, port][, address][, callback])` | 指定した宛先ポート・アドレスへデータグラムを送信する |
| `socket.close([callback])` | ソケットを閉じ、データの受信を停止する |
| `socket.address()` | バインドされたアドレス情報（address、family、port）を返す |
| `socket.connect(port[, address][, callback])` | ソケットをリモートアドレスに関連付ける（コネクト済みソケット） |
| `socket.disconnect()` | コネクト済みソケットをリモートアドレスから切断する |
| `socket.setBroadcast(flag)` | ブロードキャストパケットを許可する `SO_BROADCAST` オプションを設定する |
| `socket.setTTL(ttl)` / `socket.setMulticastTTL(ttl)` | パケットの TTL（ホップ数）を設定する |
| `socket.addMembership(multicastAddress[, multicastInterface])` / `socket.dropMembership(...)` | マルチキャストグループへの参加／離脱 |
| `socket.ref()` / `socket.unref()` | ソケットをプロセスの参照カウントに含める／除外する |

## 主なイベント

| イベント | 概要 |
|---|---|
| `'listening'` | ソケットがバインドされ、受信可能になったときに発火 |
| `'message'` | データグラムを受信したときに発火（メッセージの Buffer とリモート情報を渡す） |
| `'error'` | エラーが発生したときに発火 |
| `'close'` | ソケットが閉じられた後に発火 |
| `'connect'` | ソケットがリモートアドレスへの接続に成功したときに発火 |

## 未翻訳

各メソッドの詳細な引数仕様、ソースアドレス指定マルチキャスト、送受信バッファサイズの取得・設定などは未翻訳。

---

本ページは [nodejs.org/api/dgram](https://nodejs.org/api/dgram.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/dgram.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
