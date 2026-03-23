# カレンダーダッシュボード - GitHubへのアップロード手順

## 1. 事前準備

### 必要なもの
- GitHubアカウント
- Google Cloud Console で作成したOAuth 2.0 クライアントID
- Google Cloud Console で作成したAPIキー

---

## 2. Google Cloud Consoleでの設定

### APIキーの作成（まだの場合）
1. [Google Cloud Console](https://console.cloud.google.com/) にアクセス
2. 左メニュー「APIとサービス」→「認証情報」
3. 上部「+ 認証情報を作成」→「APIキー」
4. 作成されたAPIキーをコピーして保存

### OAuth 2.0設定の更新
1. 「認証情報」ページで作成したOAuth 2.0 クライアントIDをクリック
2. **承認済みのJavaScript生成元**に以下を追加:
   ```
   https://あなたのGitHubユーザー名.github.io
   ```
3. **承認済みのリダイレクトURI**に以下を追加:
   ```
   https://あなたのGitHubユーザー名.github.io/calendar-dashboard
   ```
4. 「保存」をクリック

---

## 3. HTMLファイルの編集

`calendar-dashboard.html` を開いて、以下の部分を編集します:

### 編集箇所（26行目付近）

```javascript
// ★★★ ここにあなたのGoogle Cloud Console OAuth 2.0 クライアントIDを入力 ★★★
const CLIENT_ID = 'YOUR_CLIENT_ID_HERE.apps.googleusercontent.com';
const API_KEY = 'YOUR_API_KEY_HERE'; // Google Cloud ConsoleでAPIキーも作成してください
```

↓ 実際の値に置き換え

```javascript
const CLIENT_ID = '123456789-abcdefg.apps.googleusercontent.com'; // あなたのクライアントID
const API_KEY = 'AIzaSyAbCdEfGhIjKlMnOpQrStUvWxYz1234567'; // あなたのAPIキー
```

---

## 4. GitHubリポジトリの作成

### 方法A: GitHubウェブサイトから作成

1. [GitHub](https://github.com/) にログイン
2. 右上の「+」→「New repository」
3. リポジトリ設定:
   - Repository name: `calendar-dashboard`
   - Public を選択
   - 「Add a README file」にチェック
4. 「Create repository」をクリック

### ファイルのアップロード

1. 作成したリポジトリページで「Add file」→「Upload files」
2. 編集した `calendar-dashboard.html` をドラッグ&ドロップ
3. 「Commit changes」をクリック

---

## 5. GitHub Pagesの有効化

1. リポジトリページで「Settings」タブをクリック
2. 左メニューから「Pages」を選択
3. **Source**の設定:
   - Branch: `main` を選択
   - Folder: `/ (root)` を選択
4. 「Save」をクリック
5. 数分待つと、ページ上部に以下のようなURLが表示されます:
   ```
   Your site is live at https://あなたのユーザー名.github.io/calendar-dashboard/
   ```

---

## 6. アクセス方法

公開されたら、以下のURLにアクセスします:

```
https://あなたのユーザー名.github.io/calendar-dashboard/calendar-dashboard.html
```

または、`calendar-dashboard.html` を `index.html` にリネームすると:

```
https://あなたのユーザー名.github.io/calendar-dashboard/
```

でアクセス可能になります。

---

## 7. トラブルシューティング

### 「認証エラー」が出る場合

1. **クライアントIDとAPIキーが正しいか確認**
   - HTMLファイル内の `CLIENT_ID` と `API_KEY` を再確認

2. **OAuth設定のURLが正しいか確認**
   - Google Cloud Consoleで「承認済みのJavaScript生成元」に正しいURLが入っているか
   - 大文字小文字、スペルミスに注意

3. **ブラウザのキャッシュをクリア**
   - Ctrl+Shift+Delete（Windows）または Cmd+Shift+Delete（Mac）
   - キャッシュをクリアして再度アクセス

### 「カレンダーが表示されない」場合

1. **Google Calendar APIが有効か確認**
   - Google Cloud Console → APIとサービス → ライブラリ
   - 「Google Calendar API」を検索して有効化

2. **ブラウザのコンソールを確認**
   - F12キーを押して開発者ツールを開く
   - Consoleタブでエラーメッセージを確認

---

## 8. 更新方法

HTMLファイルを編集した場合:

1. GitHubのリポジトリページで `calendar-dashboard.html` をクリック
2. 鉛筆アイコン（Edit this file）をクリック
3. 内容を編集
4. 下部の「Commit changes」をクリック
5. 数分でページに反映されます

---

## 9. セキュリティ上の注意

### APIキーの制限（推奨）

1. Google Cloud Console → 認証情報 → APIキーをクリック
2. 「アプリケーションの制限」で「HTTPリファラー」を選択
3. 以下を追加:
   ```
   https://あなたのユーザー名.github.io/*
   ```
4. 「APIの制限」で「キーを制限」を選択
5. 「Google Calendar API」のみにチェック
6. 保存

これにより、他のサイトからあなたのAPIキーが悪用されるのを防げます。

---

## 完了！

スマホのホーム画面に追加すれば、アプリのように使えます:

- **iPhone Safari**: 共有ボタン → ホーム画面に追加
- **Android Chrome**: メニュー → ホーム画面に追加
