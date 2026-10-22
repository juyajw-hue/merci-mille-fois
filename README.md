# Merci mille fois — ホームページの更新と公開の手引き

```
merci-site/
├── index.html   ← ページの見た目（レイアウト・色）。ふだん触りません
├── content.js   ← ★ 文章・ニュース・料金・写真の指定はすべてここ
├── images/      ← ロゴ・写真
├── CNAME        ← 独自ドメイン名（merci-mille-fois.com）
├── .nojekyll    ← GitHub用のおまじない（空ファイル）
└── README.md    ← この手引き
```

---

## 1. 更新のしかた（ふだんの運用）

### 文章・料金・ニュースを変える
`content.js` を開き、`" "` の中の日本語を書き換えて保存するだけです。
GitHub 上なら：リポジトリで `content.js` をクリック → 右上の鉛筆（Edit）→ 書き換え → 緑の **Commit changes** → 1〜2分で反映。

- 行末の `,`（カンマ）と `"`（引用符）は消さない
- 文中で改行したいところは `\n` と書く
- 画面が真っ白／上に赤い帯が出たら、カンマか引用符の消し忘れ

### ニュースを足す
`news: [ ... ]` の中の1行をコピーして一番上に貼り、日付と文章を変えます。

```js
{ date: "2026.11.01", text: "11月のレッスンのご案内", link: "https://www.instagram.com/p/xxxx/", isNew: true },
```
- `link` は空 `""` でもOK（Instagramの投稿URLを入れるとクリックで飛びます）
- `isNew: true` で「New」マーク。古くなったら `false` に

### 写真を差し替える
`images/` の中のファイルと **同じ名前** で新しい写真を上書きアップロードすれば、`content.js` を触らずに差し替わります。

| ファイル名 | 使われる場所 | おすすめの形 |
|---|---|---|
| `hero.jpg` | トップの大きな写真 | 縦長（4:5） 1200px幅くらい |
| `lesson.jpg` | レッスンの写真 | 縦長（3:4） |
| `product-bouquet.jpg` ほか | 商品3点 | 正方形 |
| `gallery-1.jpg` 〜 | ギャラリー | 縦長（3:4） |
| `ogp.jpg` | LINEやInstagramでURLを貼ったとき出る画像 | 横長 1200×630 |

別の名前で足したいときは `images/` に入れて、`content.js` の該当箇所のファイル名を書き換えます（ギャラリーは行をコピーして増やせます）。
写真はスマホからそのまま上げると重いので、長辺1200px前後に縮小してからが理想です（iPhoneなら「写真」→共有→「サイズを調整」等）。

### 黒を基調にした色味・レイアウトを変えたい
`index.html` の先頭 `:root{ ... }` に色がまとまっています（`--bg` 背景、`--ink` 文字、`--accent` 差し色）。

---

## 2. 公開先：GitHub Pages（無料）で大丈夫です

サーバー契約は不要。かかるのはお名前.com のドメイン更新料のみです。
GitHub Pages は無料プランで独自ドメイン・HTTPS 対応。同じ条件で使える無料の代替は下記です。

| | GitHub Pages（おすすめ） | Netlify | Cloudflare Pages |
|---|---|---|---|
| 料金 | 無料 | 無料 | 無料 |
| アップロード | ブラウザにドラッグ＆ドロップ | フォルダをドラッグ＆ドロップ（最も簡単） | GitHub と連携 |
| 独自ドメイン／HTTPS | ○ | ○ | ○ |
| 向いている人 | 文章をブラウザ上で直接直したい | とにかく手軽に上げたい | Cloudflare で DNS も管理したい |

どれを選んでも、お名前.com 側の作業は「Aレコード／CNAMEを書き換える」だけで、値が違うだけです。以下は GitHub Pages の手順です。

---

## 3. 公開手順（GitHub Pages）

### 3-0. 先にお名前.com でドメイン更新
期限が切れるとすべて止まります。お名前.com Navi →「ドメイン」→「更新」→ `merci-mille-fois.com` にチェック → クレジットカードで更新。
期限2週間前を切ると銀行振込・コンビニ払いは不可。ついでに「自動更新」をONに。

> ショップ（BASE）の `shop.merci-mille-fois.com` も同じドメインです。切れるとショップも開けなくなります。

### 3-1. GitHub にアップロード（15分）
1. https://github.com でアカウント作成（無料）→ ログイン
2. 右上「＋」→ **New repository** → 名前 `merci-mille-fois` → **Public** → **Create repository**
3. 「**uploading an existing file**」をクリック（または Add file → Upload files）
4. Finder で `merci-site` の **中身**（index.html, content.js, CNAME, README.md, images フォルダ, .nojekyll）をすべて選んでドラッグ＆ドロップ
   - `.nojekyll` は隠しファイル。Finder で ⌘＋Shift＋. を押すと見えます（上げ忘れても動きます）
5. **Commit changes**

### 3-2. Pages をON（3分）
1. **Settings** → 左メニュー **Pages**
2. Source：**Deploy from a branch** ／ Branch：**main** ／ **/ (root)** → **Save**
3. 1〜2分後、`https://ユーザー名.github.io/merci-mille-fois/` で表示を確認
4. **Custom domain** に `merci-mille-fois.com` → **Save**（CNAMEファイルを上げたので既に入っていることもあります）

### 3-3. お名前.com の DNS（10分、反映は数分〜24時間）
お名前.com Navi →「ネットワーク」（または「DNS・サーバー」）→「DNS設定／転送設定」→ ドメインを選ぶ →「DNSレコード設定を利用する」→ 設定する

**消すもの**：ホスト名が空欄（＝merci-mille-fois.com）や `www` の、古いサーバー向け A レコード／CNAME
**残すもの**：ホスト名 `shop` の CNAME（BASE用。**絶対に消さない**）、MX／TXT（メール用）があればそれも

**追加するもの**：

| ホスト名 | TYPE | VALUE | TTL |
|---|---|---|---|
| （空欄） | A | 185.199.108.153 | 3600 |
| （空欄） | A | 185.199.109.153 | 3600 |
| （空欄） | A | 185.199.110.153 | 3600 |
| （空欄） | A | 185.199.111.153 | 3600 |
| www | CNAME | ユーザー名.github.io | 3600 |

- A レコードは4行すべて追加
- www の CNAME は「ユーザー名.github.io」だけ（リポジトリ名は付けない）
- ネームサーバーが外部（さくら等）のままなら、先に「ネームサーバーの設定」で **お名前.com のネームサーバー** に戻す

「確認画面へ進む」→「設定する」で完了。

### 3-4. HTTPS
DNS 反映後、GitHub の Settings → Pages で Custom domain に緑チェックが付いたら **Enforce HTTPS** をON（出るまで最大24時間）。
`https://merci-mille-fois.com` で開けるようになります。

---

## 4. 公開後にやっておくこと
- Instagram のプロフィールのリンクを `https://merci-mille-fois.com` に変更
- BASE（ショップ）の「ホームページへ」ボタンのリンク先も新アドレスに変更
- 旧サイトのバックアップ「サイト情報」フォルダにはパスワードが平文で入っています。**GitHub には絶対に上げない**（上げるのは `merci-site` の中身だけ）
