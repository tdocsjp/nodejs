# tdocsjp/nodejs

Node.js 公式 API リファレンス（[nodejs.org/api](https://nodejs.org/api/)、ソースは [nodejs/node](https://github.com/nodejs/node) の `doc/api/`）の非公式日本語訳。[tdocsjp/website](https://github.com/tdocsjp/website) の submodule として取り込まれる想定。

ページは nodejs.org の URL パスをそのままミラーする（`doc/api/path.md` → `nodejs.org/api/path.html` → このリポジトリの `doc/api/path.md`）。`index.md` はトップページ（翻訳済みページへの目次）。

- 原文: https://github.com/nodejs/node の `doc/api/`
- ライセンス: 原文（コード・ドキュメントともに）は MIT License。著作権は Node.js contributors に帰属する
- 本訳は非公式であり、Node.js プロジェクトによる承認を受けたものではない

## 翻訳済み

### 全文翻訳

原文の段落・コード例をそのまま翻訳したもの。

- `doc/api/documentation.md` — [nodejs.org/api/documentation](https://nodejs.org/api/documentation.html)
- `doc/api/index.md` — [nodejs.org/api/index](https://nodejs.org/api/index.html)（API 索引）
- `doc/api/path.md` — [nodejs.org/api/path](https://nodejs.org/api/path.html)
- `doc/api/querystring.md` — [nodejs.org/api/querystring](https://nodejs.org/api/querystring.html)
- `doc/api/string_decoder.md` — [nodejs.org/api/string_decoder](https://nodejs.org/api/string_decoder.html)
- `doc/api/environment_variables.md` — [nodejs.org/api/environment_variables](https://nodejs.org/api/environment_variables.html)

### 概要・要約

原文が大きいモジュールについて、主要なクラス・メソッドを表形式で日本語にまとめたもの。各メソッドの詳細な引数・エッジケースの説明はまだない。

| ページ | 原文 |
|---|---|
| `doc/api/events.md` | [events](https://nodejs.org/api/events.html) |
| `doc/api/process.md` | [process](https://nodejs.org/api/process.html) |
| `doc/api/http.md` | [http](https://nodejs.org/api/http.html) |
| `doc/api/util.md` | [util](https://nodejs.org/api/util.html) |
| `doc/api/buffer.md` | [buffer](https://nodejs.org/api/buffer.html) |
| `doc/api/fs.md` | [fs](https://nodejs.org/api/fs.html)（原文は約300KB・数千行規模のため冒頭概要のみ） |
| `doc/api/assert.md` | [assert](https://nodejs.org/api/assert.html) |
| `doc/api/url.md` | [url](https://nodejs.org/api/url.html) |
| `doc/api/errors.md` | [errors](https://nodejs.org/api/errors.html) |
| `doc/api/child_process.md` | [child_process](https://nodejs.org/api/child_process.html) |
| `doc/api/stream.md` | [stream](https://nodejs.org/api/stream.html) |
| `doc/api/net.md` | [net](https://nodejs.org/api/net.html) |
| `doc/api/dns.md` | [dns](https://nodejs.org/api/dns.html) |
| `doc/api/crypto.md` | [crypto](https://nodejs.org/api/crypto.html) |
| `doc/api/zlib.md` | [zlib](https://nodejs.org/api/zlib.html) |
| `doc/api/readline.md` | [readline](https://nodejs.org/api/readline.html) |
| `doc/api/worker_threads.md` | [worker_threads](https://nodejs.org/api/worker_threads.html) |
| `doc/api/vm.md` | [vm](https://nodejs.org/api/vm.html) |
| `doc/api/perf_hooks.md` | [perf_hooks](https://nodejs.org/api/perf_hooks.html) |
| `doc/api/timers.md` | [timers](https://nodejs.org/api/timers.html) |
| `doc/api/console.md` | [console](https://nodejs.org/api/console.html) |
| `doc/api/tty.md` | [tty](https://nodejs.org/api/tty.html) |
| `doc/api/os.md` | [os](https://nodejs.org/api/os.html) |
| `doc/api/globals.md` | [globals](https://nodejs.org/api/globals.html) |
| `doc/api/dgram.md` | [dgram](https://nodejs.org/api/dgram.html) |

## 未翻訳

`doc/api/` の残り（約40ファイル）は未着手。特に優先度が高いもの:

- 上記「概要・要約」ページの各メソッド単位の詳細翻訳（深掘り）
- `cli`、`modules`/`esm`/`module`/`packages`（CommonJS/ESM/パッケージ）、`cluster`
- `n-api`、`addons`（C/C++ アドオン）、`deprecations`
- `diagnostics_channel`、`inspector`、`async_hooks`、`async_context`
- `https`、`http2`、`tls`、`repl`、`report`、`test`（テストランナー）
- `v8`、`wasi`、`webcrypto`、`webstreams`、`stream_iter`
- `intl`、`permissions`、`punycode`、`sqlite`、`single-executable-applications`、`tracing`、`vfs`、`ffi`、`bench`、`domain`、`embedding`

必要になったページ・深さから追加していく。
