# pages-wrapper

GitHub Pages にホスティングして GAS の「このアプリケーションは Google Apps Script のユーザーによって作成されたものです」バナーを隠すための iframe ラッパー。

## デプロイ手順

1. GitHub で公開リポジトリを作成(例: `nerima13-reservations`)
2. このフォルダの `index.html` をリポジトリ直下にアップロード
3. `index.html` 内の `REPLACE_WITH_YOUR_GAS_WEBAPP_URL` を本番 GAS Web App URL に置換
   - 形式: `https://script.google.com/macros/s/{deploymentId}/exec`
4. リポジトリ Settings → Pages → Source = `main` branch, `/ (root)` → Save
5. 数分後、`https://<username>.github.io/<repo-name>/` でアクセス可能

## 仕組み

- iframe で GAS Web App を読み込むため、Google が付与するバナー(親フレーム)は読み込まれない
- GAS 側で `setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)` 済みなので埋め込み可能
- ローディング中はスピナー表示 → iframe の `load` イベントで非表示

## 注意

- 本番デプロイの URL が変わったら(新しいデプロイを作った場合)`index.html` の URL も更新する
- 既存デプロイをアップデートする場合は同じデプロイ ID なので URL は変わらない
