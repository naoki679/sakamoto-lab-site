# サカモトラボ サイト

個人事業「サカモトラボ」の事業紹介サイト。

**主事業はホームページ制作・リニューアル**。アプリ開発は「中身の仕組みまで自分でつくれる」
という技術力の裏付けとして、ページ下部の「つくったもの」で紹介している。

## ページの構成（上から順）

| セクション | id | 内容 |
|---|---|---|
| ヒーロー | — | キャッチコピー・数値4つ |
| できること | `#service` | 新規制作 / 作り直し / 仕組みを足す |
| 料金 | `#price` | 10万円〜（税別）・含まれるもの / 別途かかるもの |
| 引用帯 | — | 「立派なサイトは、つくりません」 |
| ご依頼の流れ | `#flow` | 5ステップ |
| つくったもの | `#works` | アプリ4本（デモ付き） |
| サカモトラボについて | `#about` | 屋号の説明 |
| よくあるご質問 | `#faq` | 8問 |
| お問い合わせ | `#contact` | Formspreeフォーム |
| プライバシーポリシー | `#privacy` | |

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
公開URL: https://sakamoto-lab-site.camvp509.workers.dev

## Cloudflare 側の設定値

| 項目 | 値 |
|---|---|
| Project name | `sakamoto-lab-site` |
| Build command | `exit 0` |
| Deploy command | `npx wrangler deploy` |

配信するフォルダは `wrangler.jsonc` の `assets.directory`（`./public`）で指定している。
ダッシュボードに Build output directory の欄がないのはこのため。

## お問い合わせフォーム（Formspree）

設定済み。`public/index.html` 末尾の

```js
var FORMSPREE_ID = "xljrvvlj";
```

が送信先。無料枠は月50件。変更するときは Formspree で新しいフォームを作り、
エンドポイント `https://formspree.io/f/○○○○○○○○` の**末尾8文字**を差し替える。

メールアドレスはページ上に一切書いていない。
Formspreeが落ちたときのフォールバックとして、スクリプト内の `MAIL_TO`
（文字列を実行時に組み立てている）からメールソフトが立ち上がる。

## よく直す箇所（public/index.html 内の目印）

| 直したいもの | 探す文字列 |
|---|---|
| キャッチコピー | `<h1 class="reveal">` |
| ヒーローの数値4つ | `class="stats reveal"` |
| できること3枚 | `<!-- SERVICE -->` |
| **料金** | `<!-- PRICE -->` / `class="plan"` |
| 料金の金額 | `class="plan-amt"` |
| 含まれる・別途かかる | `class="inc"` / `class="exc"` |
| 各アプリのカード | `<!-- WORK 01 -->` 〜 `<!-- WORK 04 -->` |
| デモを見るボタン | `class="demo"` |
| ご依頼の流れ | `<div class="flow">` |
| FAQ | `<div class="faq">` |
| フォームの項目 | `<form class="cform"` |
| フォームの送信先 | `FORMSPREE_ID` |
| 配色 | 先頭の `:root{ }` 内の `--accent` など |

## 書かないと決めていること

- お客様の実績（受注前のため、載せられる案件がまだない）
- 対面での打ち合わせ（メール・オンラインのみ）
- メールアドレスの直書き
- 大規模サイト・大企業向けの表現（ひとりで回せる範囲を明示する）
