# STATUS.md — 作業状況

## 現在のバージョン
`1.3.0`

## 最終更新
2026-06-28

## 状態
- [x] リポジトリ初期化
- [x] GitHub 公開・Template repository 設定(0.3.0 で Public 化)
- [x] サイト台帳 config/subutomo-sites.json の正を本リポジトリに設置(Pages 配信)
- [x] Subutomo バッジ(assets/subutomo-badge.js + logo.png)を同梱
- [ ] プロジェクト基本情報の記入 (CLAUDE.md)
- [ ] 機能実装開始

## 直近の変更
- `1.3.0`: 台帳 `description` をバイリンガル `{en, ja}` オブジェクトに正準化(subuta先行データを正本へ昇格・全7件日本語入り)。badge.js を堅牢化し title/description が「文字列 / {en,ja} / *_ja」のいずれでも安全表示(`[object Object]` 再発防止)。READMEスキーマも更新。全サイトへ badge.js+台帳を配布する
- `1.2.0`: subutomo-badge.js の設計方針を「英語のみ」→「`<html lang>` で日英自動切替」に変更。パネルUI文言(プライバシー宣言/読込・失敗・空メッセージ)を i18n 化し、台帳に `title_ja`/`description_ja` があれば日本語サイトで表示(無ければ英語フォールバック)。ブランド名と © は不訳。READMEの方針記述も更新。全サイトへ同期スキルで配布予定
- `1.1.0`: 統一フォーマットの footer を実装(subu-mnym と同形)。リンク付きコピーライト `© 2026 Subutomo Dev.`、版を `ver. X.Y.Z` 形式で APP_VERSION から動的注入、支援リンク(☕チップ/❤️Sponsors)・ご意見ご要望(📣・ポップ演出)、日英切替トグル、背景透過でテーマトークン追従。他7サイトへ配布予定
- `0.6.1`: 台帳参照をローカル方式に統一(実行時のテンプレPages fetch廃止)。同期スキル subutomo-site-kit を新設し台帳コピー手順を明記
- `0.6.0`: バッジに privacy 宣言機能を追加(パネル下部に localStorage / analytics の英文表示、全falseまたは未指定なら非表示)
- `0.5.0`: バッジに elementId 設定と Shift+クリック素通しを追加(既存サイトの隠し機能[管理者認証等]と共存するためのホスト統合口)
- `0.4.0`: index.html 雛形を追加(バッジ配線済み・バージョン表示・<記入>プレースホルダ)。READMEを配線済み前提の手順に更新
- `0.3.0`: Public化+Pages有効化。サイト台帳の正を設置、Subutomoバッジ3点セットを同梱、READMEに登録・組み込み手順を追記
- `0.2.0`: スキルパック導入(env-guard/dev-prep-checklist有効、commit-guard/session-handoff草稿)
- `0.1.2`: 認証方針を追加(デフォルト認証なし・必要時に脅威モデルで選定)
- `0.1.1`: GitHub公開・テンプレート設定・README手順更新
- `0.1.0`: テンプレートリポジトリとして初期化
