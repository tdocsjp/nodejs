---
title: Crypto（概要）
source: https://nodejs.org/api/crypto.html
---

# Crypto（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:crypto` モジュールは、OpenSSL のハッシュ・HMAC・暗号化・復号・署名・検証・鍵カプセル化（KEM）機能をラップした暗号機能を提供します。

## ハッシュ・メッセージ認証

| 関数 | 概要 |
|---|---|
| `crypto.createHash(algorithm)` | SHA-256・SHA-512・MD5 などのアルゴリズムでダイジェストを計算するハッシュオブジェクトを作成する |
| `crypto.createHmac(algorithm, key)` | 秘密鍵を使ってメッセージ認証コードを計算する HMAC オブジェクトを作成する |

## 乱数生成

| 関数 | 概要 |
|---|---|
| `crypto.randomBytes(size[, callback])` | 暗号学的に安全な乱数バイト列を生成する |
| `crypto.randomUUID([options])` | RFC 4122 準拠のランダムな UUID を生成する |
| `crypto.randomInt([min, ]max[, callback])` | 指定範囲内のランダムな整数を生成する |

## 暗号化・復号、署名

| 関数 | 概要 |
|---|---|
| `crypto.createCipheriv(algorithm, key, iv[, options])` / `crypto.createDecipheriv(...)` | 指定したアルゴリズム・鍵・初期化ベクトルでデータを暗号化／復号するオブジェクトを作成する |
| `crypto.createSign(algorithm)` / `crypto.createVerify(algorithm)` | デジタル署名を生成／検証するオブジェクトを作成する |

## 鍵管理・鍵導出

| 関数 | 概要 |
|---|---|
| `crypto.createPrivateKey()` / `crypto.createPublicKey()` / `crypto.createSecretKey()` | PEM・DER・JWK など各種形式から鍵オブジェクト（`KeyObject`）を作成する |
| `crypto.generateKeyPair()` / `crypto.generateKeyPairSync()` | RSA・EC・Ed25519 などの非対称鍵ペアを生成する |
| `crypto.pbkdf2()` / `crypto.scrypt()` / `crypto.hkdf()` | パスワードなどから鍵を導出する（PBKDF2、scrypt、HKDF） |

## 証明書・その他

| 項目 | 概要 |
|---|---|
| `X509Certificate` | X.509 デジタル証明書を扱うクラス（検証、フィンガープリント、証明書チェーンの確認など） |
| `DiffieHellman` / `ECDH` | Diffie-Hellman／楕円曲線 Diffie-Hellman 鍵交換を行うクラス |
| `crypto.subtle` / `crypto.webcrypto` | Web Crypto API 互換の SubtleCrypto インターフェース |
| `crypto.timingSafeEqual(a, b)` | タイミング攻撃を防ぐため、一定時間で2つのバッファを比較する |

## 基本的な使い方

```js
const { createHmac } = require('node:crypto');
const secret = 'abcdefg';
const hash = createHmac('sha256', secret)
  .update('I love cupcakes')
  .digest('hex');
console.log(hash);
```

## 未翻訳

各クラス・関数の詳細な引数・アルゴリズム一覧、FIPS モード、鍵カプセル化（KEM）の詳細などは未翻訳。

---

本ページは [nodejs.org/api/crypto](https://nodejs.org/api/crypto.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/crypto.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
