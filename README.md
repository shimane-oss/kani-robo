# kani-robo
Matz葉がにロボコン公式ウェブサイト

Jekyll(Beautiful Jekyllテーマ)で構築し、GitHub Actions経由でGitHub Pagesに公開しています。

## 更新方法

### 新着情報(お知らせ)を追加する

`_posts/` ディレクトリに `YYYY-MM-DD-任意のスラッグ.md` という名前でファイルを作成します。

```yaml
---
title: 記事タイトル
subtitle: 補足の一言(任意)
thumbnail-img: "/images/xxx.jpg"   # 一覧に表示する画像(任意)
tags: [タグ1, タグ2]                # 任意
---

本文をMarkdownで書きます。
```

作成・削除するだけでホーム(`index.md`)や新着情報一覧(`/news/`)に自動的に反映されます。他のファイルを編集する必要はありません。

### スポンサーを掲載する

`_includes/sponsors.html` を編集します。現在は「スポンサー募集中」の表示のみですが、掲載が決まったら以下のような形でロゴとリンクを追加してください(1社あたり `.sponsor-item` を1つ追加するイメージです)。

```html
<div class="sponsor-grid">
  <div class="sponsor-item">
    <a href="https://example.com/"><img src="{{ '/images/example-logo.png' | relative_url }}" alt="株式会社Example ロゴ"></a>
    <div><a href="https://example.com/">株式会社Example</a></div>
  </div>
  <!-- 2社目以降も同様に .sponsor-item を追加 -->
</div>
```

- ロゴ画像は `images/` に配置し、`src` は `{{ '/images/ファイル名' | relative_url }}` の形で指定してください(baseurlが自動的に付与されます)。
- `.sponsor-grid` / `.sponsor-item` のスタイルは `assets/css/custom.css` で定義済みです。

このファイルは `{% include sponsors.html %}` で各ページから共通で読み込まれているため、1箇所編集するだけで全ページに反映されます。

### 固定ページ(ルール・講習会・スタッフ募集・スポンサー募集など)を編集する

`rule.md` / `seminar.md` / `staff.md` / `cfs.md` / `index.md` を直接編集します。front matterで `title` / `subtitle` / `share-description`(検索結果・SNSシェア用の説明文) / `share-img`(OGP画像)を設定できます。

### 過去の大会アーカイブ(archives/以下)

`archives/1st`, `archives/2nd`, `archives/3rd`, `archives/pre` は静的HTMLのままです。Jekyllのビルド対象外(front matterなし)なので、従来通りHTMLファイルを直接編集してください。

## ローカルでの確認方法

```bash
bundle install
bundle exec jekyll serve
```

`http://localhost:4000/kani-robo/` でプレビューできます。`_config.yml` を変更した場合はサーバーの再起動が必要です。

## 公開の仕組み

- `main` ブランチにマージされると、GitHub Actions(`.github/workflows/pages.yml`)が自動でビルド・公開します。
- GitHub Pagesの設定(Settings → Pages → Source)は「GitHub Actions」になっています。
