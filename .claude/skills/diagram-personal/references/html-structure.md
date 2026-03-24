# HTML 構造ガイド（パーソナル図解）

## 方針

### SSoT（アイコン・装飾）

**このファイルが正。** 図解 HTML 全体について次を守る。

- **アイコン**: **Lucide のみ**（CDN は基本テンプレートどおり）。装飾・意味付けに絵文字を使わない。
- **絵文字**: **禁止**。本文・見出し・箇条書き・吹き出し内テキストを含め、絵文字で表現しない。

対話ブロックの**左枠**に Lucide を使わないことは、上記「対話の左枠（パーソナル図解）」および [dialogue-personas.md](dialogue-personas.md) の **「対話左枠の画像アバター（必須）」** どおり。[dialogue-personas.md](dialogue-personas.md) にある Lucide の HTML 例は**参照用**（セリフ構造の見本）であり、左枠の実装には使わない。**対話以外**で Lucide をどう使うかは下記「Lucide（よく使う）」および dialogue-personas の汎用記述に従う。

### その他

- **本気AIブランド色は使わない**（`diagram-maji` とは別系統）
- **配色**は `images/learner.png`・`images/navigator.png` のトーン（紫系／ローズ系）と**同じ色箱**に揃え、ヘッダ・用語ボックス・リンク・アクセントもその系統で統一する（具体値は基本テンプレの `:root` と `.header-gradient` など）
- **対話の左枠（パーソナル図解）**: **常に画像アバター**（学習者・ナビゲーターとも）。詳細は下記 **「対話左枠の画像アバター」**。左枠に Lucide アイコンは使わない。吹き出しの構造・台本は [dialogue-personas.md](dialogue-personas.md)。**対話以外**の装飾は引き続き Lucide のみ（絵文字禁止など、他の SSoT は変わらない）。

### 構造・レイアウト（ページ全体の並び）

**セクションの順序・各セクション内のブロック配置**（導入を1枚の `section-card` にまとめること、全体の地図のグリッドカード、用語を1セクションに縦積み、「この競合でまず押さえる3つ」のバッジ行、本編の `h2`→学習者→ナビゲーター→本文、まとめ、出典一覧＋免責、目次との `id` 対応など）は **[exemplar.md](exemplar.md) の「黄金見本」** の説明に従い、**具体マークアップの SSoT は [exemplar-layout.html](exemplar-layout.html)**（＋同階層 `images/`）。ブラウザで確認する場合は [exemplar-layout.html](exemplar-layout.html) を開くか、デプロイ済みスナップショットの URL は [exemplar.md](exemplar.md) の「黄金見本」表の **公開 URL（ブラウザ確認用）** を参照（アンカー例は同表に付記）。

**本ファイル**は `<head>`・`body` のラッパー・共通 `<style>`（`:root`、`.section-card`、吹き出し、バッジ、`.toc` など）・`</main>` 直後の目次 `<nav>` の **DOM 位置とクラス名の定義** の SSoT である。`<main>` **内に何セクションをどの順で置くか、各セクションの中身の並べ方**は [exemplar-layout.html](exemplar-layout.html) に合わせる（テンプレートの `main` プレースホルダはあくまで最小例）。exemplar-layout に `<style>` が無いユーティリティ（例: `.code-block`）が必要なときは、本ファイルのテンプレートの定義をそのまま使う。

### 対話左枠の画像アバター

パーソナル図解では対話左枠は**毎回必ず**画像とする。**政策**（必須であること）・**ファイル名と配置**・**デプロイ時の同梱**はこの見出し以下だけを正とする（スキルの Phase 6 などからは繰り返さない）。**マークアップの HTML 型**は [dialogue-personas.md](dialogue-personas.md) の **「対話左枠の画像アバター（必須）」** を正とする。

- **ファイル名・配置**: 学習者は `images/learner.png`、ナビゲーターは `images/navigator.png`。`index.html` と**同じ階層**に `images/` を置き、HTML からは相対パス `images/...` で参照する。
- **デプロイ**: 静的ホスト（Surge 等）に載せるときは、`index.html` と `images/` を**常に同じアップロード単位**に含める。HTML だけ上げて `images/` を欠くと表示が壊れる。
- **サイズ・切り抜き**: 枠は `w-12 h-12`・`rounded-xl`・`flex-shrink-0`・`overflow-hidden`。画像は `class="w-full h-full object-cover"`。`width` / `height` に `48` を付与してよい。
- **枠線・背景**: 吹き出しと色を揃える。色の正は基本テンプレの `:root`（`--learner-border` / `--nav-border` など）と `.learner-bubble` / `.guide-bubble` / `.learner-avatar` / `.navigator-avatar`（イラストの色に合わせて更新する）。
- **アクセシビリティ**: 装飾のみなら `<img alt="">` とし、親に `role="img"` と **`aria-label`**（文字列は [dialogue-personas.md](dialogue-personas.md) の「役割名と画面上の名前（二層）」に従い、[exemplar-layout.html](exemplar-layout.html) の対話ブロックと同一）を付ける。

---

## 基本テンプレート

下記 `<style>` は [exemplar-layout.html](exemplar-layout.html) の `<style>` と**同じ意味**を保つこと（配色・コンポーネント変更時は両方を更新。[exemplar.md](exemplar.md) の「`<style>` の二重管理」参照）。

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>【図解タイトル】 — パーソナル図解</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://unpkg.com/lucide@latest"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&display=swap" rel="stylesheet">
  <style>
    :root {
      /* ページ全体（B: アバターと同じ色箱） */
      --personal-accent: hsl(258, 45%, 40%);
      --personal-accent-light: hsl(270, 50%, 97%);
      /* learner.png / navigator.png 中央付近の明暗をスポイトした値をベースに調整 */
      --learner-border: #423773;
      --learner-bubble-a: #faf8ff;
      --learner-bubble-b: #e8e0ff;
      --learner-avatar-bg: #f3f0ff;
      --nav-border: #a86f6f;
      --nav-bubble-a: #fff9f8;
      --nav-bubble-b: #fde8e3;
      --nav-avatar-bg: #fef2f2;
    }
    body { font-family: 'Noto Sans JP', system-ui, sans-serif; }

    .header-gradient {
      background: linear-gradient(125deg, #3730a3 0%, #5b3d5c 48%, #8b5a6a 100%);
    }

    .section-card {
      background: white;
      border-radius: 1rem;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.08);
      padding: 2rem;
      margin-bottom: 2rem;
    }

    .term-explain {
      background: linear-gradient(135deg, var(--personal-accent-light) 0%, hsl(270, 40%, 99%) 100%);
      border-left: 4px solid var(--personal-accent);
      padding: 1.5rem;
      border-radius: 0.75rem;
      margin: 1.5rem 0;
    }
    .term-word { color: var(--personal-accent); }

    .char-bubble {
      position: relative;
      padding: 1.25rem 1.5rem;
      border-radius: 1rem;
      margin-left: 0.5rem;
    }
    .char-bubble::before {
      content: '';
      position: absolute;
      left: -10px;
      top: 18px;
      border-width: 10px;
      border-style: solid;
    }
    .learner-bubble {
      background: linear-gradient(135deg, var(--learner-bubble-a) 0%, var(--learner-bubble-b) 100%);
      border: 2px solid var(--learner-border);
    }
    .learner-bubble::before {
      border-color: transparent var(--learner-border) transparent transparent;
    }
    .guide-bubble {
      background: linear-gradient(135deg, var(--nav-bubble-a) 0%, var(--nav-bubble-b) 100%);
      border: 2px solid var(--nav-border);
    }
    .guide-bubble::before {
      border-color: transparent var(--nav-border) transparent transparent;
    }

    /* 対話左枠の画像アバター（dialogue-personas.md の「対話左枠の画像アバター（必須）」と併用） */
    .learner-avatar {
      border: 2px solid var(--learner-border);
      background: var(--learner-avatar-bg);
    }
    .navigator-avatar {
      border: 2px solid var(--nav-border);
      background: var(--nav-avatar-bg);
    }

    .label-learner { color: #2e285a; }
    .label-navigator { color: #5c3030; }

    .badge-essential {
      background: linear-gradient(135deg, #b91c1c 0%, #ef4444 100%);
      color: white;
      padding: 0.25rem 0.75rem;
      border-radius: 9999px;
      font-size: 0.875rem;
      font-weight: 600;
    }
    .badge-recommended {
      background: linear-gradient(135deg, #5b4d8c 0%, #8b6b8e 100%);
      color: white;
      padding: 0.25rem 0.75rem;
      border-radius: 9999px;
      font-size: 0.875rem;
      font-weight: 600;
    }
    .badge-optional {
      background: linear-gradient(135deg, #6b7280 0%, #9ca3af 100%);
      color: white;
      padding: 0.25rem 0.75rem;
      border-radius: 9999px;
      font-size: 0.875rem;
      font-weight: 600;
    }

    .code-block {
      background: #1e293b;
      color: #e2e8f0;
      padding: 1.5rem;
      border-radius: 0.75rem;
      overflow-x: auto;
      font-family: ui-monospace, monospace;
      font-size: 0.875rem;
      line-height: 1.7;
    }

    .toc {
      position: fixed;
      left: 2rem;
      top: 50%;
      transform: translateY(-50%);
      background: white;
      padding: 1rem;
      border-radius: 0.75rem;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
      max-height: 80vh;
      overflow-y: auto;
      z-index: 50;
    }
    @media (max-width: 1280px) {
      .toc { display: none; }
    }
  </style>
</head>
<body class="bg-violet-50">
  <header class="header-gradient text-white py-8">
    <div class="max-w-4xl mx-auto px-4">
      <h1 class="text-3xl md:text-4xl font-bold">【タイトル】</h1>
      <p class="mt-2 text-lg opacity-90">サブタイトル（この1枚で何がわかるか）</p>
    </div>
  </header>

  <main class="max-w-4xl mx-auto px-4 py-8">
    <!-- セクション（見出しには id を付け、目次の href と対応させる） -->
  </main>

  <nav class="toc" aria-label="このページの目次">
    <p class="text-sm font-bold text-slate-700 mb-2">目次</p>
    <ul class="text-sm space-y-1 list-none m-0 p-0">
      <li><a href="#section-example" class="text-violet-700 hover:underline">見出しの例</a></li>
      <!-- main 内の各セクションに対し、<li><a href="#..." class="text-violet-700 hover:underline">...</a></li> を追加 -->
    </ul>
  </nav>

  <script>lucide.createIcons();</script>
</body>
</html>
```

### 目次（`.toc`）

- **DOM 上の位置**: `</main>` の直後、`lucide.createIcons()` の `<script>` の直前（上記テンプレートどおり）。
- **画面上の位置**: ビューポート左寄りに固定（上記 `.toc` の `left: 2rem` など。左右はこのブロックのみを変更する）。
- **表示**: ビューポート幅 1280px 未満では `.toc` は非表示（上記 `<style>` 内のメディアクエリ）。
- **中身**: `main` 内の見出し要素に付けた `id` と、`href="#..."` を一対一で対応させる。クラス名・ネストはテンプレートの `<nav class="toc">` ブロックに合わせる。

---

## Lucide（よく使う）

対話ブロックの**左枠**には Lucide を使わない（方針および※注を参照）。下表は**汎用**（用語ボックス・箇条書き・コード見出しなど、**対話左枠以外**）の目安であり、**一覧の重複ではない**。

| 用途 | アイコン名 |
|-----|-----------|
| 学習者の疑問 | `message-circle-question` |
| ナビゲーター | `compass` |
| 用語 | `lightbulb` |
| チェック | `check-circle` |
| 注意 | `alert-circle` |
| コード | `code` |
| 本 | `book-open` |

※ **対話の左枠**はパーソナル図解では常に画像のため、下表の「学習者の疑問」「ナビゲーター」行の Lucide は**対話左枠には使わない**（[dialogue-personas.md](dialogue-personas.md) の Lucide は**参照用**の見本のみ）。用語ボックスなど**対話左枠以外**では下表どおり Lucide を使ってよい。上表の「本」行の `book-open` は**汎用**（書籍・参考の意味付け）であり、対話の役割とは別。

---

## コード例の前の日本語

コード・設定・コマンドを出す前に必ず「これがやること」を書く。例:

```html
<div class="mb-4">
  <div class="flex items-center gap-2 mb-2">
    <i data-lucide="code" class="w-5 h-5 text-violet-600"></i>
    <span class="font-bold text-slate-700">これがやること</span>
  </div>
  <p class="text-slate-600 ml-7">
    〇〇が起きそうなときに、<span class="font-bold text-red-600">△△しない</span>、というルールを書いています。
  </p>
</div>
<div class="code-block">
  <pre><code><!-- 例 --></code></pre>
</div>
```

---

## フロー図

`sample/majiai-diagram/.claude/skills/diagram-maji/references/html-structure.md` のフロー図パターンと同様に、`flex` + `arrow-right` / `arrow-down` で簡易フローを表す。配色はページのアクセント（バイオレット系）に合わせる。
