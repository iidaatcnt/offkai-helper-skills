---
name: uranai-workers
description: オリジナル占いアプリを対話形式で作成し、Cloudflare Workers に自動デプロイするスキル。uranai-maker と同じインタビュー形式でテーマ・キャラクター・判定方法・デザインを決めた後、HTML/CSS/JS を生成して src/index.js に変換し、wrangler deploy まで全自動で実行する。ユーザーが「占いアプリを作ってWorkersにデプロイ」「uranai_workers」「占いを公開して」「占いアプリをCloudflareにデプロイ」と言ったら必ずこのスキルを起動すること。
---

# uranai-workers — 占いアプリ作成 → Cloudflare Workers 自動デプロイ

uranai-maker と同じインタビューで占いアプリを作り、そのまま Cloudflare Workers にデプロイする。

---

## ステップ1: インタビュー（uranai-maker と同じ）

以下の質問を **1つずつ** 順番に聞く。

1. **テーマ**「どんな占いにしますか？（例：昆虫占い、フルーツ占い、家電占い）」
2. **キャラクター数**「何種類に分けますか？（例：6・8・12）」
3. **キャラクター名**「キャラクターの名前を教えてください。思いつかなければ『考えて』でOK」
4. **キャラクター説明**「各キャラクターの性格・特徴を一言で。思いつかなければ『考えて』でOK」
5. **判定方法**
   - A) 誕生日で判定
   - B) 質問に答えて判定
   - C) 両方使う
   - B または C の場合：質問内容と数を聞く（思いつかなければ提案する）
6. **デザイン**「雰囲気は？（かわいい系・クール系・ポップ系・和風・シンプル など）」
7. **カラー**「メインカラーは？（なければ『おまかせ』でOK）」
8. **タイトル**「アプリのタイトルを教えてください」

インタビュー後、内容を箇条書きで確認してから生成に進む。

---

## ステップ2: ファイル生成

出力先フォルダ：`/Users/iidaatcnt/libe0531/{テーマ名}-uranai/`

### 2-1. index.html を生成

- HTML / CSS / JS をすべて1ファイルに収める
- レスポンシブデザイン（スマートフォン対応）
- 外部ライブラリ・CDN 不使用
- 絵文字でキャラクターを表現（画像不使用）

画面構成：
1. タイトル画面（タイトル・キャッチコピー・スタートボタン）
2. 入力・質問画面（誕生日フォームまたは選択肢ボタン）
3. 結果画面（キャラクター名・説明・絵文字・もう一度ボタン）

### 2-2. src/index.js を生成

index.html の内容を以下の形式で src/index.js に変換する：

```js
const HTML = `...index.htmlの全内容...`;

export default {
  async fetch(request, env, ctx) {
    return new Response(HTML, {
      headers: { 'Content-Type': 'text/html; charset=UTF-8' },
    });
  },
};
```

**重要**: HTML内のバックティック（`）は `\`` にエスケープ、`${` は `\${` にエスケープする。

### 2-3. wrangler.toml を生成

```toml
name = "{テーマ名}-uranai"
main = "src/index.js"
compatibility_date = "2024-01-01"
preview_urls = false
```

`name` はアルファベット・ハイフンのみ（日本語不可）。例：`fruits-uranai`、`insect-uranai`

---

## ステップ3: Cloudflare Workers にデプロイ

```bash
cd /Users/iidaatcnt/libe0531/{テーマ名}-uranai
wrangler deploy
```

デプロイ成功後、以下を表示する：

```
✅ デプロイ完了！

🌐 URL: https://{name}.miidacnt.workers.dev

【アプリを修正したいときは】
「〇〇を変更して」とクロコに伝えるだけで修正→再デプロイできます。
```

---

## エラーが出た場合

- `No loader is configured for ".html"` → wrangler.toml の main が index.html になっている。`src/index.js` に修正して再実行。
- `wrangler: command not found` → `npm install -g wrangler` を案内する。
- `not logged in` → `wrangler login` を案内する。
