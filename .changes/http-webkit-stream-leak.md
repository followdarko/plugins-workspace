---
"http": patch
"http-js": patch
---

Fix a memory leak in WebKit webviews (measured in macOS WKWebView): every `fetch` response stayed alive for the life of the webview. The `clone` override on the returned `Response` was defined in the same scope as the body stream's callbacks, so the stream's source could reach its own `Response`, a cycle WebKit never collects. The overrides now live in a function of their own; behaviour is unchanged.
