# 🧠 NEURO-NAV

**[日本語](#-日本語) | [English](#-english)**

Cyberpunk-styled real-time NAV monitor for Japanese mutual funds — with dopamine.

![license](https://img.shields.io/badge/license-MIT-00f0ff) ![deps](https://img.shields.io/badge/dependencies-none-ff2a6d) ![hosting](https://img.shields.io/badge/hosting-GitHub%20Pages%20ready-00ff9f)

---

## 🇯🇵 日本語

### これは何?

投資信託の基準価額は1日1回しか更新されず退屈——なので、**連動する先物・指数と為替をリアルタイムに取得し、「次回基準価額のライブ予測」を常時表示**するダッシュボードです。史上最高値を更新すると全画面エフェクトと脳汁SEが炸裂します。

単一の `index.html` のみで動作。ビルド不要、API キー不要、サーバー不要。

### 主な機能

| 機能 | 説明 |
|---|---|
| リアルタイム推定基準価額 | `公式基準価額 × 指数変動率 × 為替変動率`。基準値は基準価額の算出基準日に日付一致させた終値 |
| 公式基準価額の自動取得 | eMAXIS Slim 全世界株式(オルカン)/米国株式(S&P500)/NASDAQ100 は三菱UFJアセットマネジメント公開APIから毎日自動再キャリブレーション |
| 資産クラス | 投資信託・仮想通貨(数量ベース)・現金(円) |
| チャート | 1H/1D/5D/1M/3M/6M/1Y。合計チャートは全銘柄の時刻和集合+休場中銘柄の直前値保持で合成 |
| 実質構成ヒートマップ | 保有投信を合成した実質個別株ポートフォリオ(finviz風ツリーマップ、月報ベース概算) |
| マーケット情報 | CNN Fear & Greed / VIX / 為替・金利・金・BTC / 世界指数のスライドパネル |
| 経済指標カレンダー | 週間重要指標バー(ForexFactory→TradingView→Myfxbook→FOMC静的日程の4段フォールバック) |
| ニュースティッカー | NHK経済 + CNBC |
| 脳汁システム | 史上最高値=全画面演出+シンセSE、セッション最高値、⚡連続上昇コンボ、キリ番マイルストーン、目標達成、NEXT ATHメーター、上昇ティックコイン音(SE:ON+) |
| 回線診断 | 各データ経路の生存確認。成功経路を記憶して自動優先 |
| 高速起動 | 前回値をlocalStorageにキャッシュし即描画→裏で更新 |

### 使い方

1. `index.html` をブラウザで開く(またはGitHub Pagesで公開)
2. **+銘柄追加** → かんたん登録から投信を選ぶと公式基準価額が自動入力される → 保有口数を入力
3. あとは眺めて脳汁を待つ。詳しい操作は画面上部の **ヘルプ** ボタンでツアー表示

### GitHub Pages での公開

```
リポジトリ作成 → index.html をアップ → Settings → Pages → Deploy from a branch (main / root)
```

数分で `https://<ユーザー名>.github.io/<リポジトリ名>/` で閲覧可能。スマホ対応済み。

### プライバシー

**保有口数・金額などの入力データは、使用中のブラウザの localStorage にのみ保存されます。** リポジトリやサーバーには一切送信・含有されません。端末間の移行は「保存/復元」ボタンのJSONバックアップで行います(このJSONには保有情報が含まれるため公開リポジトリにコミットしないこと)。

### 注意事項

- 表示は連動指数・為替からの**機械的な推定値**であり、実際の基準価額・評価額とは乖離します(TTM為替と終値の差、信託報酬、配当、先物と現物の乖離等で±0.3%程度)
- データソース(Yahoo Finance / 三菱UFJアセットマネジメント / Binance / CNN / ForexFactory / NHK / ExchangeRate-API)はすべて無保証・遅延あり
- ヒートマップの構成銘柄比率は月報ベースの静的概算(コード内 `CONSTITUENTS` で編集可)
- 投資判断は自己責任で。本ツールは娯楽・情報目的です

---

## 🇬🇧 English

### What is this?

Japanese mutual fund NAVs update only once a day — boring. NEURO-NAV fetches the underlying **futures/indices and FX in real time and continuously displays a live forecast of the next NAV**, in a cyberpunk dashboard. Break your all-time high and you get a full-screen effect with a dopamine-inducing synth SE.

A single `index.html`. No build, no API keys, no server.

### Features

| Feature | Description |
|---|---|
| Real-time estimated NAV | `official NAV × index ratio × FX ratio`, with base values date-matched to the NAV's valuation date |
| Auto official NAV | eMAXIS Slim All Country / S&P 500 / NASDAQ 100 recalibrate daily via Mitsubishi UFJ AM's public API |
| Asset classes | Mutual funds, crypto (quantity-based), and cash (JPY) |
| Charts | 1H/1D/5D/1M/3M/6M/1Y; the total chart merges all assets on a unified time grid with last-value hold for closed markets |
| Look-through heatmap | finviz-style treemap of the individual stocks you effectively hold across funds (approx., monthly-report based) |
| Market info panel | CNN Fear & Greed / VIX / macro (FX, US10Y, gold, BTC) / world indices, auto-sliding |
| Economic calendar | Weekly high-impact events bar with a 4-level source fallback (ForexFactory → TradingView → Myfxbook → static FOMC schedule) |
| News ticker | NHK Economy + CNBC |
| Dopamine system | All-time high = full-screen FX + synth SE, session highs, ⚡up-tick combos, round-number milestones, goal achievement, NEXT-ATH meter, coin sounds per up-tick (SE:ON+) |
| Diagnostics | Per-route health check; the working route is remembered and preferred |
| Fast boot | Last values cached in localStorage for instant paint, refreshed in the background |

### Getting started

1. Open `index.html` in a browser (or host it on GitHub Pages)
2. **+銘柄追加 (Add asset)** → pick a fund from quick-add (official NAV auto-fills) → enter your units
3. Watch and wait for dopamine. Press **ヘルプ (Help)** in the header for a guided tour

### Deploy to GitHub Pages

```
Create a repo → upload index.html → Settings → Pages → Deploy from a branch (main / root)
```

Live at `https://<username>.github.io/<repo>/` within minutes. Mobile-friendly.

### Privacy

**Your inputs (units, amounts) are stored only in your browser's localStorage.** Nothing is sent to or contained in the repository or any server. Use the backup (保存/復元) JSON to migrate between devices — do not commit that JSON to a public repo, as it contains your holdings.

### Disclaimers

- Values are **mechanical estimates** derived from linked indices/FX and will deviate from actual NAVs (TTM vs. closing FX, fees, dividends, futures basis; typically within ±0.3%)
- All data sources (Yahoo Finance / Mitsubishi UFJ AM / Binance / CNN / ForexFactory / NHK / ExchangeRate-API) are unofficial, delayed, and provided as-is
- Heatmap constituent weights are static approximations (editable in `CONSTITUENTS` in the code)
- For entertainment/informational purposes only. Invest at your own risk

---

*Built with vanilla HTML/CSS/JS. MIT License.*
