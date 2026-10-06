---
title: このドキュメントについて
source: https://nodejs.org/api/documentation.html
---

# このドキュメントについて

<!--introduced_in=v0.10.0-->

<!-- type=misc -->

Node.js の公式 API リファレンスドキュメントです。

Node.js は [V8 JavaScript エンジン][] 上に構築された JavaScript ランタイムです。

## コントリビュート

このドキュメントの誤りは [issue tracker][] に報告してください。プルリクエストの送り方については [コントリビューションガイド][] を参照してください。

## Stability index（安定度指標）

<!--type=misc-->

ドキュメント全体を通して、各セクションの安定度が示されています。一部の API は十分に実績があり信頼されているため、今後まったく変更されない可能性が高いものです。その一方で、生まれたばかりで実験的なものや、危険であることが知られているものもあります。

安定度指標は次のとおりです。

> Stability: 0 - Deprecated（非推奨）。この機能は警告を発する場合があります。後方互換性は保証されません。

<!-- separator -->

> Stability: 1 - Experimental（実験的）。この機能は [semantic versioning][] のルールの対象外です。後方互換性のない変更や削除が、将来のどのリリースでも発生する可能性があります。本番環境でこの機能を使用することは推奨されません。
>
> 実験的機能は、さらに次の段階に分かれます。
>
> * 1.0 - Early development（初期開発）。この段階の実験的機能は未完成であり、大幅な変更の対象となります。
> * 1.1 - Active development（活発な開発）。この段階の実験的機能は、最小限の実用性を備える段階に近づいています。
> * 1.2 - Release candidate（リリース候補）。この段階の実験的機能は、安定版となる準備がおおむね整っています。さらなる破壊的変更は想定されていませんが、ユーザーからのフィードバックや機能の基盤となる仕様の開発に応じて発生する可能性があります。この機能が安定版としてマークされる準備が整ったことを確認するため、ユーザーによるテストとフィードバックを推奨します。
>
> 実験的機能が実験的ステータスを外れるのは、通常は安定版へ昇格する場合か、非推奨サイクルを経ずに削除される場合です。

<!-- separator -->

> Stability: 2 - Stable（安定版）。npm エコシステムとの互換性が高い優先度を持ちます。

<!-- separator -->

> Stability: 3 - Legacy（レガシー）。この機能が削除される可能性は低く、semantic versioning による保証も引き続き適用されますが、もはや積極的にメンテナンスされておらず、他の代替手段が利用可能です。

機能は、その使用が害をもたらさず、npm エコシステム内で広く依存されている場合、非推奨ではなくレガシーとしてマークされます。レガシー機能で見つかったバグが修正される可能性は低いです。

実験的機能を使用する際、特にライブラリを作成する場合は注意が必要です。ユーザーは実験的機能が使われていることに気づいていない場合があります。実験的な API に変更が加えられた際、バグや動作の変化がユーザーを驚かせる可能性があります。驚きを避けるため、実験的機能の使用にはコマンドラインフラグが必要になることがあります。実験的機能は [警告][] を発する場合もあります。

## Stability overview（安定度の概要）

<!-- STABILITY_OVERVIEW_SLOT_BEGIN -->

<!-- STABILITY_OVERVIEW_SLOT_END -->

## JSON 出力

<!-- YAML
added: v0.6.12
-->

すべての `.html` ドキュメントには、対応する `.json` ドキュメントがあります。これは、ドキュメントを利用する IDE やその他のツールのためのものです。

## システムコールと man ページ

システムコールをラップする Node.js の関数には、その旨が明記されています。ドキュメントは、そのシステムコールがどのように動作するかを説明する対応する man ページにリンクしています。

ほとんどの Unix のシステムコールには Windows の相当物があります。それでも、動作の違いが避けられない場合があります。

[V8 JavaScript エンジン]: https://v8.dev/
[semantic versioning]: https://semver.org/
[コントリビューションガイド]: https://github.com/nodejs/node/blob/HEAD/CONTRIBUTING.md
[issue tracker]: https://github.com/nodejs/node/issues/new
[警告]: process.md#event-warning

---

本ページは [nodejs.org/api/documentation](https://nodejs.org/api/documentation.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/documentation.md`）の非公式日本語訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
