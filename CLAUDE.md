# ナカムラサイクル WEBサイト プロジェクト記録

## プロジェクト概要
- **クライアント**：ナカムラサイクル（東京都江戸川区鹿骨の自転車屋）
- **目的**：修理・メンテナンスサービスを前面に出した集客サイト。物売りではなくサービス提供の認知を高める
- **公開URL**：https://nakamura-cycle.pages.dev
- **GitHub**：https://github.com/niwa-eiji/nakamura-cycle（mainブランチ）
- **開設**：2025年11月〜（開店から半年程度の新しい店）

---

## 技術構成

| 項目 | 内容 |
|------|------|
| フロントエンド | HTML / Tailwind CSS（CDN）/ Vanilla JS |
| ホスティング | Cloudflare Pages（genba-standard アカウント）|
| CMS | microCMS（中村さんアカウント・サービスID: tz5fxdvfug）|
| デプロイ | GitHub mainブランチへpushで自動デプロイ（Cloudflare Pages連携）|
| フォント | Noto Sans JP（Google Fonts）|
| アイコン | Phosphor Icons |

---

## microCMS API情報（現在）

| エンドポイント | 用途 | フィールド |
|---|---|---|
| `/api/v1/news` | お知らせ | title, content（publishedAtで日付）|
| `/api/v1/lineup` | 商品ラインナップ | name, description, image, category |
| `/api/v1/calendar` | 営業カレンダー | date（日時）, type（セレクト・配列で返る）, note（備考）|

**typeフィールドの値（配列で返ってくる）**
- `["臨時休業"]` → 黄色・臨休
- `["特別営業日"]` → 緑・特営
- それ以外 → 赤・定休（水曜日デフォルト）

⚠️ `item.type` は **配列**で返る（`item.種類` ではない）。`Array.isArray`で対応済み。

---

## サイト構成（セクション順）

1. **Header**：ロゴ・ナビ（おすすめ自転車・修理サポート・メンテナンス知識・お知らせ・Q&A・アクセス）・電話番号
2. **Hero**：自転車修理店内写真（Pexels #132682）・1枚固定・background-image方式
3. **News**：microCMSから取得
4. **Lineup**：おすすめ自転車（microCMSから取得・タブ切り替え）
5. **Service**：修理サービス4種 + 料金表
6. **Knowledge**：プロが教えるメンテナンス知識（6カード）← 新設
7. **Q&A**：よくある質問（アコーディオン）
8. **Access**：営業カレンダー + Googleマップ
9. **Footer**：Instagram リンク

---

## ヒーロー画像について

**現在**：`hero.png`（モノクロ自転車修理工場・プロジェクトフォルダ内ローカルファイル）

**重要**：`background-image` CSS方式を採用（`<img>`タグではない）
- Android Chromeのスクロールガタつき対策のため
- `height: 90svh` を使用（`vh`だとAndroidアドレスバー連動でカクつく）
- スマホ幅（767px以下）はアニメ全無効化済み

**将来**：中村さんの実際の店内・作業風景写真に差し替え予定

---

## Gitの使い方

```bash
# ナカムラサイクルフォルダで作業
cd "C:\Users\eeeni\OneDrive\デスクトップ\AI company\営業\ナカムラサイクル"

# 変更をpush（これでCloudflare Pagesに自動デプロイ）
git add index.html
git commit -m "変更内容のメモ"
git push origin main
```

---

## これまでの主な作業履歴

| 日付 | 作業内容 |
|------|---------|
| 2026-04 | docx_workフォルダ（node_modules）削除・整理 |
| 2026-04 | ヒーロー画像をUnsplash→Pexels日本写真→1枚固定に変更 |
| 2026-04 | ヒーロー画像をスライドショー→background-image方式に変更 |
| 2026-04 | スマホスクロールのガタつきをsvh+アニメ無効化で対応 |
| 2026-04 | メンテナンス知識セクションを新設（6カード） |
| 2026-04 | ナビに「メンテナンス知識」追加（PC・スマホ・フッター全対応）|
| 2026-04 | microCMSカレンダーのバグ修正（item.種類→item.type・配列対応）|
| 2026-04 | メンテナンス知識の見出しを「プロが教えるメンテナンス知識」に変更 |
| 2026-04 | git初期化・GitHub連携・自動デプロイ設定 |
| 2026-04 | ホスティングをCloudflare Workers → Cloudflare Pagesに移行（GitHub自動デプロイ対応）|
| 2026-04 | microCMSを中村さんアカウント（tz5fxdvfug）に移行・APIキー更新 |
| 2026-04 | ヒーロー画像をhero.pngに差し替え・コピー変更 |
| 2026-04 | メンテナンス知識セクションを画像カードデザインに刷新 |
| 2026-04 | 全セクション見出しサイズを統一（text-xl md:text-2xl font-light）|

---

## 今後やること（気に入ってもらえた後）

### STEP 1｜microCMS移行 ✅ 完了
- 中村さんのmicroCMSアカウント（tz5fxdvfug）に切り替え済み
- お知らせ・商品ラインナップ・営業カレンダーのAPI設定済み

### STEP 2｜カスタムドメイン
- 中村さんがお名前.com等でドメイン購入
- Cloudflare PagesにカスタムドメインをAdd → DNSレコードを中村さんに送付
- 中村さんがDNS設定（コピペのみ）

### STEP 3｜写真差し替え
- 中村さんに店内・作業・外観写真を撮ってもらう
- スレッドに添付 → ヒーロー画像に反映

### STEP 4｜コンテンツ充実
- お知らせ・商品ラインナップ・カレンダーをmicroCMSに入力

---

## 運用体制

| 作業 | 担当 |
|------|------|
| CMS更新（お知らせ・カレンダー等）| 中村さん |
| コード修正・機能追加 | niwa-eiji + Claude Code |
| インスタ更新 | 中村さん |
| Cloudflare Pages管理 | niwa-eiji（genba-standard アカウント）|
| ドメイン更新（年1回）| 中村さん |
