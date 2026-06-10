# \<プロジェクト名\>

\<プロジェクトの概要を記入\>

## セットアップ

```bash
# 依存パッケージのインストール
npm install

# 開発サーバー起動
npm run dev
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
5. `STATUS.md` を起点に開発を開始する

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

5. 開発を開始する

## ライセンス

\<記入\>
