# daily-engineering-news

毎朝のエンジニアリングニュースブリーフを蓄積し、GitHub Pages で公開するためのリポジトリです。
ソフトウェアエンジニアリングの動向を 1 日 1 ブリーフにまとめ、日付ごとにアーカイブしていきます。

## 公開URL

- トップ（一覧）: https://fourn9.github.io/daily-engineering-news/
- 各日のブリーフ: https://fourn9.github.io/daily-engineering-news/YYYY-MM-DD/

## ディレクトリ構成

```
daily-engineering-news/
├── index.html        ← 過去ブリーフ一覧（日付リンク集）
├── README.md
├── .gitignore
└── YYYY-MM-DD/
    └── index.html    ← その日のブリーフ
```

- `index.html`（トップ）は、各日付ディレクトリへの相対リンク一覧を持ちます。
- 新しい日付ほどリストの先頭（上）に来るように追記します。
- 各日のブリーフは `YYYY-MM-DD/index.html` に置きます。

## 更新フロー

1. **日付ディレクトリを追加**して、その日のブリーフ HTML を置く。

   ```sh
   DATE=$(date +%Y-%m-%d)
   mkdir -p "$DATE"
   # 用意したブリーフHTMLを $DATE/index.html として配置する
   ```

2. **トップ index.html にリンクを追記**する。
   `index.html` 内の `<!-- INSERT-NEXT-BRIEF-HERE -->` の直下に、新しい `<li>` を追加します
   （新しい日付が一番上に来るように先頭へ）。

   ```html
   <li>
     <a href="./YYYY-MM-DD/">
       <span class="date-jp">YYYY年MM月DD日(曜)</span>
       <span class="date-iso">YYYY-MM-DD</span>
     </a>
   </li>
   ```

3. **コミットして push** する。

   ```sh
   git add .
   git commit -m "Add brief for $DATE"
   git push
   ```

4. 反映には数分かかります。トップURLを開いて確認してください。

## デザイン方針

- スマートフォン閲覧を最優先したモバイルファースト・レスポンシブ。
- ダークモードは `prefers-color-scheme` で自動切替。
- CSS は各 HTML に `<style>` で埋め込み、CDN 等の外部依存なし。
