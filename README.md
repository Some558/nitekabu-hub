# nitekabu hub

`@kabueng55` が作っている nitekabu 周辺アプリの一覧ページ（リンクハブ）。
X プロフィールの URL 先として使う、静的 1 ファイル構成のサイト。

## 構成

- `public/index.html` — 本体（HTML / CSS / Google Fonts 1 ファイル完結 / 公開対象）
- `wrangler.toml` — Cloudflare Workers Static Assets 設定（`./public` を配信）
- `docs/skills/frontend-design/` — デザイン基準として参照した [Anthropic 公式 frontend-design スキル](https://github.com/anthropics/skills/tree/main/skills/frontend-design)

## デザイン方針

- **Editorial × Financial Terminal** — 落ち着いた dark slate（`#0a0d12` 基調）に、Fraunces serif と JetBrains Mono の対比
- アクセントは TradingView 系ブルー（`#5a9eff`）と キャンドルゴールド（`#f0b429`）— nitekabu 本体の配色と接続
- 薄いチャートグリッドの背景、ロウソク足を思わせる斜めパターン、控えめなステージドリビール

`docs/skills/frontend-design/SKILL.md` の指針に従って「AI 臭い汎用デザイン」を避ける構成。

## ローカル確認

```bash
# どれか好きなやつで
open public/index.html                                # macOS で直接開く
python3 -m http.server 5500 -d public                 # http://localhost:5500/
npx -y serve public                                   # http://localhost:3000/
npx wrangler dev                                      # wrangler 経由で本番に近い形で確認
```

## デプロイ

GitHub の `main` に push すると Cloudflare Workers Builds が `npx wrangler deploy` を自動実行し、`hub.nitekabu.com` (custom domain 設定後) に反映される。

## 編集ポイント

- 載せるアプリを増減: `index.html` の `<section class="apps">` 内の `.app-card` を追加・削除
- 公開 / 準備中の差別化: `<span class="app-status live">live</span>` を `<span class="app-status upcoming">soon</span>` 等に切り替え（CSS は `live` のみ用意済 — 必要時に追加）
- `last updated` 日付: `index.html` フッターの該当行を直接編集

## デプロイ候補

| 候補 | コスト | 備考 |
|---|---|---|
| `hub.nitekabu.com` (KAGOYA VPS 同居) | 0 円 | 既存 nginx に追加。ドメイン管理が一元化できる |
| Cloudflare Pages | 0 円 | GitHub push で自動デプロイ。CDN が速い |
| GitHub Pages | 0 円 | 設定が一番楽。プロジェクト Pages or `username.github.io/nitekabu-hub` |

将来 X 以外（note プロフィール等）からもリンクするので、独自ドメイン（`hub.nitekabu.com`）を当てる方針。
