# subutomo-site-kit — サイトキット同期スキル

Subutomo Dev 共通パーツ(サイトキット)を、テンプレ正本から各サイトへ
複製・同期するための手順。**正本は常に subutomo-template リポジトリ**。
各サイトのコピーは派生であり、ズレたらテンプレ正本に合わせる。

## サイトキットの構成

| ファイル | 役割 | 参照方式 |
|---|---|---|
| `assets/subutomo-badge.js` | サイト選択バッジ本体(ES5・依存ゼロ) | — |
| `common/assets/logo.png` | 公式ロゴ | バッジが logoPath で参照 |
| `config/subutomo-sites.json` | サイト台帳 | **各サイトのローカル参照**(後述) |
| `SUBUTOMO_BADGE_CONFIG` スニペット | index.html 内の設定 | `sitesJsonPath: 'config/subutomo-sites.json'` |
| `assets/favicon.svg` / `favicon-32.png` / `favicon-180.png` | ファビコン3点(全サイト共通) | `index.html` の `<head>` に link |

## 台帳の参照方式(重要)

- `sitesJsonPath` は **`'config/subutomo-sites.json'`(相対パス・ローカル参照)を正とする**
- **テンプレの Pages 上の台帳を実行時に fetch する方式は廃止**
  (テンプレの改名・削除・障害が全サイトに波及するため)
- 台帳の正本はテンプレに置き、本スキルで各サイトへ複製する運用は従来どおり

## 同期手順

1. テンプレ正本(C:\dev\subutomo-template)が最新か確認する(git pull)
2. 対象サイトへ以下をコピーする:
   - `assets/subutomo-badge.js`
   - `common/assets/logo.png`(無い場合のみ)
   - **`config/subutomo-sites.json` をテンプレ正本から各サイトへコピーする**
     (台帳を更新したときは全サイトに対してこのステップを必ず実施)
   - **ファビコン3点(`assets/favicon.svg` / `favicon-32.png` /
     `favicon-180.png`)を各サイトの `assets/` へコピーし、`index.html` の
     `<head>` に次の link を設定する:**

     ```html
     <link rel="icon" type="image/svg+xml" href="assets/favicon.svg">
     <link rel="icon" type="image/png" sizes="32x32" href="assets/favicon-32.png">
     <link rel="apple-touch-icon" href="assets/favicon-180.png">
     ```
3. 対象サイトの `SUBUTOMO_BADGE_CONFIG` を確認する:
   - `sitesJsonPath: 'config/subutomo-sites.json'`(ローカル参照)であること
   - `currentSiteId` / `theme` / `privacy` / `elementId` はサイト固有のまま維持
4. バッジパネルのリンク一覧が表示されることを確認する
5. 各サイトの流儀(SemVer・コミット規約)でコミット・push する

## 台帳更新時のフロー

1. テンプレ正本の `config/subutomo-sites.json` にエントリを追加・修正
2. テンプレをコミット・push(正本の記録)
3. 上記「同期手順」2〜5 を全サイトに対して実施
