# Invoice Extractor

PDF請求書を複数アップロードして、AIが自動でデータ抽出 → テーブルに流し込むWebアプリ。

## ファイル構成

```
invoice-app/
├── public/
│   └── index.html          # フロントエンド
├── netlify/
│   └── functions/
│       └── extract.js      # Anthropic APIプロキシ（サーバーサイド）
├── netlify.toml            # Netlify設定
└── README.md
```

## デプロイ手順

### 1. GitHubリポジトリを作成

```bash
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/YOUR_USERNAME/invoice-app.git
git push -u origin main
```

### 2. Netlifyと連携

1. https://app.netlify.com にログイン
2. "Add new site" → "Import an existing project"
3. GitHubを選択して上記リポジトリを選択
4. Build settings はそのまま（netlify.toml が自動で読まれる）
5. "Deploy site" をクリック

### 3. 環境変数にAPIキーを設定

1. Netlifyのサイトダッシュボードを開く
2. Site configuration → Environment variables
3. "Add a variable" をクリック
4. Key: `ANTHROPIC_API_KEY`
5. Value: `sk-ant-...`（AnthropicのAPIキー）
6. "Save" → サイトを再デプロイ

### 4. 社内共有

デプロイ後に発行されるURL（例: `https://your-app.netlify.app`）を社内メンバーに共有するだけ。
アカウント不要、ブラウザだけで動作。

## APIキーの取得

https://console.anthropic.com/ にログイン → API Keys → Create Key

## 注意事項

- PDFの内容はAnthropicのAPIサーバーに送信されます
- 社内のセキュリティポリシーを確認の上ご利用ください
- APIの利用料金はAnthropicのアカウントに課金されます
