# サカモトラボ サイト

個人事業「サカモトラボ」の事業紹介・実績紹介サイト。

## 構成

```
sakamoto-lab-site/
├── public/
│   ├── index.html          ← サイト本体（1ファイル完結・外部依存なし）
│   └── demo/
│       └── kabu/
│           └── index.html  ← 高配当株アプリのデモ版（サンプル10銘柄入り）
├── wrangler.jsonc          ← Cloudflare の設定
├── README.md
└── .gitignore
```

編集するのは `public/index.html`。ビルド不要。

### 高配当株デモの更新方法

`public/demo/kabu/index.html` は kabu-tool の本体をコピーし、先頭に
デモ用ブートスクリプト（`<!-- デモモード ブートストラップ -->` のブロック）を
差し込んだもの。本体を更新したら、同じブロックを新しい本体の
`<meta name="viewport" ...>` の直後に貼り直す。

ブートスクリプトの役割:
- localStorage を sessionStorage に差し替え（タブを閉じるとデータが消える）
- サンプル10銘柄を初期投入
- 画面下のDEMO帯とリセットボタンを追加

## ローカルで確認する

`public/index.html` をダブルクリックしてブラウザで開くだけ。

## 公開（Cloudflare Workers 静的アセット / GitHub連携）

修正後は以下で反映される（1〜2分でビルド完了）:

```powershell
cd C:\Users\camvp\Documents\Claude\Projects\sakamoto-lab-site
git add .
git commit -m "変更内容"
git push
```

反映後はブラウザで `Ctrl + Shift + R`（強制リロード）で確認する。

## Cloudflare 側の設定値

| 項目 | 値 |
|---|---|
| Project name | `sakamoto-lab-site` |
| Build command | `exit 0` |
| Deploy command | `npx wrangler deploy` |

配信するフォルダは `wrangler.jsonc` の `assets.directory`（`./public`）で指定している。
ダッシュボードに Build output directory の欄がないのはこのため。

## よく直す箇所（public/index.html 内の目印）

| 直したいもの | 探す文字列 |
|---|---|
| キャッチコピー | `<h1 class="reveal">` |
| 実績の数値4つ | `class="stats reveal"` |
| 各実績カード | `<!-- WORK 01 -->` 〜 `<!-- WORK 04 -->` |
| デモを見るボタン | `class="demo"` |
| ご依頼の流れ | `<div class="flow">` |
| FAQ | `<div class="faq">` |
| メールアドレス | `camvp509@gmail.com` |
| 配色 | 先頭の `:root{ }` 内の `--accent` など |
