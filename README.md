# \<プロジェクト名\>

\<プロジェクトの概要を記入\>

> 認証モジュールは同梱しない。必要時は CLAUDE.md の認証方針を参照。

## セットアップ(ローカル確認)

静的サイト構成(単一HTML + ES モジュール)のため、ローカルサーバーで確認する。

```bash
# Node.js
npx serve .

# Python
python -m http.server 8080
```

## 使い方

このリポジトリは新規プロジェクト開始用のテンプレートです。以下のいずれかの方法で利用してください。

### 方法A(推奨): GitHub の「Use this template」を使う

1. GitHub で [t-sumita/subutomo-template](https://github.com/t-sumita/subutomo-template) を開き、**Use this template → Create a new repository** をクリック
2. リポジトリ名を `t-sumita/<新プロジェクト名>` として作成
3. `C:\dev` に clone する

   ```powershell
   cd C:\dev
   gh repo clone t-sumita/<新プロジェクト名>
   ```

4. `CLAUDE.md` の記入欄(プロジェクト名・目的・リポジトリ・公開URL)を埋める
5. `index.html` の `<記入>` を埋める(タイトル、`SUBUTOMO_BADGE_CONFIG` の
   `currentSiteId`・`theme`。バッジは配線済みなのでこれだけで動く)
6. `STATUS.md` を起点に開発を開始する
7. サイトを GitHub Pages で公開したら、**本リポジトリの台帳に登録する**
   (下記「サイト台帳への登録」参照)

### 方法B: ローカルでコピーする

1. テンプレートを `C:\dev\<新プロジェクト名>` にコピーする(**`.git` は含めない**)

   ```powershell
   robocopy C:\dev\subutomo-template C:\dev\<新プロジェクト名> /E /XD .git
   ```

2. `CLAUDE.md` の記入欄を埋める
3. git を初期化する

   ```powershell
   cd C:\dev\<新プロジェクト名>
   git init -b main
   ```

4. GitHub に新規リポジトリを作成して push する

   ```powershell
   git add -A
   git commit -m "feat: プロジェクト初期化"
   gh repo create t-sumita/<新プロジェクト名> --private --source . --remote origin --push
   ```

5. `index.html` の `<記入>` を埋めて開発を開始する(バッジは配線済み)
6. サイト公開後、本リポジトリの台帳に登録する

## Subutomo 共通パーツ(サイト台帳とバッジ)

### サイト台帳 — 正本は本リポジトリ、参照は各サイトのローカル

全 Subutomo Dev サイトの台帳は **`config/subutomo-sites.json`(本リポジトリが唯一の正本)** で管理する。
各サイトは同期スキル(`subutomo-site-kit`)で複製された**自リポジトリ内のコピーをローカル参照**する
(`sitesJsonPath: 'config/subutomo-sites.json'`)。

> **実行時に本リポジトリの Pages 上の台帳を fetch する方式は廃止。**
> 理由: テンプレの改名・削除・障害が全サイトに波及するため。
> 正本をテンプレに置き、同期スキルで各サイトへ複製する運用は従来どおり。

- スキーマ: `{ id, title, description, url, thumb, size, status }`
  - `description` は **`{ "en": "...", "ja": "..." }` オブジェクト**を正準とする
    (バッジパネルが `<html lang>` に応じて出し分け。`ja` 無指定時は `en` にフォールバック)
  - 後方互換: `description` が**文字列**(英語)でも可。その場合 `description_ja` を併記すれば
    日本語サイトで日本語表示になる。`title` も同様に文字列 / `{en,ja}` / `title_ja` を許容
- `status: "visible"` のもののみ各サイトで表示される
- バッジのサイト一覧に出るのは **id が `-site` で終わるもののみ**(それ以外は作品扱い)
- `thumb` の正典は `https://club.subutomo.dev/contents/<id>/thumb.png`
  (画像を用意する場合は spctrl-site/contents に置く)

### サイト台帳への登録(新サイト公開時)

1. 本リポジトリの `config/subutomo-sites.json` にエントリを1件追加する
   (`description` は `{ "en": "...", "ja": "..." }` で記載。英語のみの場合は `ja` を省略可)
2. 同期スキル(`subutomo-site-kit`)で台帳を各サイトの
   `config/subutomo-sites.json` へ複製し、各サイトを push する

### Subutomo バッジの組み込み(3点セット)

**本テンプレートから作ったサイトには配線済み**(`index.html` の `<記入>` を
埋めるだけでよい)。以下はテンプレ由来でない**既存サイトへ後付けする場合**の手順。
次の4点をコピー・追記する。

1. `assets/subutomo-badge.js`(ES5・依存なし・単一ファイル)
2. `common/assets/logo.png`(公式ロゴ)
3. `config/subutomo-sites.json`(台帳。テンプレ正本からコピー)
4. `index.html` の `</body>` 直前にスニペットを追記:

```html
<script>
  window.SUBUTOMO_BADGE_CONFIG = {
    currentSiteId: '<新プロジェクト名>',
    sitesJsonPath: 'config/subutomo-sites.json',
    logoPath: './common/assets/logo.png',
    theme: 'light-bg',   // 明るい背景なら 'light-bg'、暗い背景なら 'dark-bg'
    version: '1.0.0',    // 任意: © の右に "(v1.0.0)" を表示(省略で非表示)
    privacy: {           // 任意: パネル下部にプライバシー宣言を表示(日英自動切替)
      localStorage: false,   // 設定をブラウザに保存するサイトは true
      analytics: false       // Cloudflare Web Analytics を入れたサイトは true
    },
    onSecretAction: null
  };
</script>
<script src="./assets/subutomo-badge.js"></script>
```

> 版を別ソース(例:`config.js` の `APP_VERSION`)で持つサイトは、`version` を直書きせず
> `window.SUBUTOMO_FOOTER_VERSION = APP_VERSION;` を設定し
> `window.__suBadgeApplyVersion && window.__suBadgeApplyVersion();` を呼べばよい
> (badge.js は後から渡された版にもフック/短時間ポーリングで追従する)。

- 左下に共通フッターと同じ見た目(ロゴ+© Subutomo Dev)が表示され、
  クリックで他サイトへのリンク一覧パネルが開く
- **版表示は © の右隣**:`version`(または `window.SUBUTOMO_FOOTER_VERSION`)を渡すと
  `© 2026 Subutomo Dev (vX.Y.Z)` の形で表示。**© と版はバッジが担い、フッターには © を置かない**
- パネルのUI文言(プライバシー宣言・読込/失敗/空メッセージ)は `<html lang>` に
  応じて日英自動切替(`ja*` → 日本語 / それ以外 → 英語)。ブランド名と © は不訳
  - **読み込み後に言語を変えても追従する**:JP/EN トグル等で `<html lang>` を
    書き換えればパネルが自動再描画(MutationObserver)。`<html lang>` を変えない
    実装の場合は `document.dispatchEvent(new Event('subu:langchange'))` を発火すれば
    再描画される(パネルが開いていれば即時)
- 台帳の取得に失敗してもパネルはローカライズ済みメッセージを出して静かに縮小する
- `privacy` のフラグが全て false または未指定なら宣言セクションは表示されない
- Shift+クリックはパネルを開かず素通しする(隠し機能などホスト側の統合用。
  `elementId` でバッジ要素に id を付ければ既存スクリプトからバインドできる)
- canvas 全面でポインタイベントを取るサイトでは、`.su-badge, .su-panel` への
  クリック/タッチをドラッグ処理より先に素通しさせること(subuta-site の実装参照)

### ファビコンの組み込み(全サイト共通アセット)

ファビコン3点(`assets/favicon.svg` / `assets/favicon-32.png` /
`assets/favicon-180.png`)は **Subutomo Dev 共通アセット**。正本は本リポジトリの
`assets/` に置き、同期スキル(`subutomo-site-kit`)で各サイトへ配布する。

**本テンプレートから作ったサイトには配線済み**(`index.html` の `<head>` に
下記 link が入っている)。以下はテンプレ由来でない**既存サイトへ後付けする場合**の手順。

1. 次の3点を各サイトの `assets/` へコピーする:
   - `assets/favicon.svg`(本体・拡大に強い SVG)
   - `assets/favicon-32.png`(32×32 PNG・SVG 非対応環境向け)
   - `assets/favicon-180.png`(180×180 PNG・iOS ホーム画面用)
2. `index.html` の `<head>` に次の link を追記する:

```html
<link rel="icon" type="image/svg+xml" href="assets/favicon.svg">
<link rel="icon" type="image/png" sizes="32x32" href="assets/favicon-32.png">
<link rel="apple-touch-icon" href="assets/favicon-180.png">
```

## ライセンス

\<記入\>
