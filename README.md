# 🐊 offkai-helper-skills — Claude Code スキル集

サバ缶が作った Claude Code 用スキルの置き場所です。
スキルをインストールすることで、Claude Code に新しいコマンドが追加されます。

---

## スキル一覧

| スキル名 | コマンド | 説明 |
|---|---|---|
| offkai-helper | `/offkai-helper` | オフ会で使える質問文を作ってくれる |
| uranai-maker | `/uranai-maker` | オリジナル占いアプリを対話形式で自動生成 |

---

## インストール方法

### 1. このリポジトリをダウンロード

画面右上の緑の「Code」ボタン → 「Download ZIP」を選択して解凍。

または git clone:
```bash
git clone https://github.com/iidaatcnt/offkai-helper-skills.git
```

### 2. スキルファイルをコピー

使いたいスキルの `.md` ファイルを `~/.claude/commands/` にコピーします。

```bash
# 例: uranai-maker をインストール
cp uranai-maker.md ~/.claude/commands/uranai-maker.md
```

### 3. Claude Code を再起動

Claude Code を一度終了して、再起動してください。

```bash
/exit
claude
```

### 4. 使ってみる

```
/uranai-maker
```

---

## スキルの説明

### 🔮 uranai-maker
質問に答えるだけでオリジナルの占いアプリ（HTML）を自動生成します。
- 昆虫占い・お魚占い・家電占いなど、テーマは自由
- 誕生日入力・質問形式の両方に対応
- 生成した HTML は Cloudflare Pages にそのまま公開できる

### 🐊 offkai-helper
Claude Code オフ会で使える質問文を作ってくれるスキルです。
モヤッとした悩みを入力するだけで、他の参加者に聞きやすい質問文を丁寧版・カジュアル版の2パターンで生成します。
