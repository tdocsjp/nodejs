---
title: DNS（概要）
source: https://nodejs.org/api/dns.html
---

# DNS（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:dns` モジュールは名前解決の機能を提供し、ホスト名から IP アドレスを調べたり、逆引き DNS クエリを行ったりできます。コールバック形式と Promise 形式の両方の API を提供します。

## よく使う関数

| 関数 | 概要 |
|---|---|
| `dns.lookup(hostname[, options], callback)` | OS の機能（`/etc/hosts` など）を使い、ホスト名を最初に見つかった A（IPv4）または AAAA（IPv6）レコードに解決する |
| `dns.resolve(hostname[, rrtype], callback)` | DNS プロトコルを使って、指定した種類（デフォルト `'A'`）のリソースレコードにホスト名を解決する |
| `dns.resolve4(hostname[, options], callback)` / `dns.resolve6(...)` | ホスト名の IPv4（A）／IPv6（AAAA）アドレスを解決する |
| `dns.reverse(ip, callback)` | IPv4/IPv6 アドレスからホスト名への逆引きを行う |
| `dns.resolveAny(hostname, callback)` | ホスト名に対して利用可能なすべての DNS レコード（ANY クエリ）を解決する |
| `dns.resolveMx()`・`dns.resolveCname()`・`dns.resolveTxt()` など | MX・CNAME・TXT・SOA・SRV・NS・PTR・CAA・NAPTR・TLSA といった特定のレコードタイプを解決する |

Promise 版は `dns.promises`（または `require('node:dns/promises')`）から同じ関数をコールバックなしで利用できます。

```js
const dnsPromises = require('node:dns/promises');
const addresses = await dnsPromises.resolve4('example.org');
```

## `dns.lookup()` と `dns.resolve*()`/`dns.reverse()` の違い

| 観点 | `dns.lookup()` | `dns.resolve*()`/`dns.reverse()` |
|---|---|---|
| プロトコル | OS の機能（getaddrinfo）を使う | 常にネットワーク経由の DNS プロトコルを使う |
| 設定ファイル | `/etc/hosts`・`nsswitch.conf`・`resolv.conf` を尊重する | DNS サーバーのみを使う |
| 性能 | スレッドプール上の同期呼び出し（ブロックする可能性がある） | 常に非同期で、スレッドプールに影響しない |
| 用途 | 汎用的な名前解決 | 直接的な DNS クエリ、ネットワーク通信 |

## 未翻訳

各関数の詳細な引数・オプション、`dns.setServers()`、`dns.Resolver` クラスなどは未翻訳。

---

本ページは [nodejs.org/api/dns](https://nodejs.org/api/dns.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/dns.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
