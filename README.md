# サカモトラボ サイト

個人事業「サカモトラボ」の事業紹介・実績紹介サイト。

## 構成

- `index.html` — サイト本体（1ファイル完結。CSS/JSすべて内包、外部依存なし）

## ローカルで確認する

`index.html` をダブルクリックしてブラウザで開くだけ。ビルド不要。

## 公開（Cloudflare Pages / GitHub連携）

このフォルダを GitHub リポジトリにして Cloudflare Pages に接続済み。
修正後は以下で反映される（約1〜2分でビルド完了）:

```powershell
cd C:\Users\camvp\Documents\Claude\Projects\sakamoto-lab-site
git add .
git commit -m "変更内容"
git push
```

反映後はブラウザで `Ctrl + Shift + R`（強制リロード）で確認する。

## Cloudflare Pages の設定値

| 項目 | 値 |
|---|---|
| Framework preset | None |
| Build command | （空欄） |
| Build output directory | `/` |

静的HTMLなのでビルドコマンドは不要。

## よく直す箇所（index.html 内の目印）

| 直したいもの | 探す文字列 |
|---|---|
| キャッチコピー | `<h1 class="reveal">` |
| 実績の数値4つ | `class="stats reveal"` |
| 各実績カード | `<!-- WORK 01 -->` 〜 `<!-- WORK 04 -->` |
| ご依頼の流れ | `<div class="flow">` |
| FAQ | `<div class="faq">` |
| メールアドレス | `camvp509@gmail.com` |
| 配色 | 先頭の `:root{ }` 内の `--accent` など |
