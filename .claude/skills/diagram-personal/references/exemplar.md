# 模範パターン（パーソナル図解）

**このファイルの役割**: 図解 HTML の **セクション順・ブロック配置・レイアウトの説明** と **品質チェックリスト** の SSoT。**長いマークアップの実体**は [exemplar-layout.html](exemplar-layout.html)（＋ `images/`）のみを正とする。HTML の head・基本テンプレ・配色・Lucide 方針・絵文字禁止・コード前の日本語などは [html-structure.md](html-structure.md)、対話の型・吹き出しのマークアップ・台本は [dialogue-personas.md](dialogue-personas.md)、用語ボックスの語彙ルールは [term-dictionary.md](term-dictionary.md) に従う（ここでは繰り返さない）。

---

## 黄金見本（構造・レイアウトの一次参照）

**新規の図解 HTML を組み立てるときは、まずマスター HTML を開いてレイアウトを合わせる。**

**マスター（マークアップの SSoT）**: 本ディレクトリの **[exemplar-layout.html](exemplar-layout.html)** と **同階層の `images/`**（`learner.png` / `navigator.png`）。見本を改訂するときは **必ずここを編集**し、デプロイ用フォルダ（例: `output/…/index.html`）や Surge へ載せるときは **ここからコピー**する（逆に output だけ直してスキル側を置き換えない）。

| 参照 | 内容 |
|------|------|
| **マスター HTML（開くべき実体）** | [exemplar-layout.html](exemplar-layout.html) |
| **公開 URL（ブラウザ確認用）** | **https://diagram-ai-lift-mar24-2026.surge.sh/** — **このセルのみが正**（他ファイルでは URL を書かず、本表を指す）。ローカル確認: リポジトリ内の `output/ai-lift-consulting-mar24-2026/index.html`（マスターと同型のとき）。アンカー例: `#section-map` / `#section-three` |

**守ること（レイアウト）**

- **ヘッダー**: `header-gradient` + `max-w-4xl` 内の `h1` とリード1行（見本と同じ情報階層）。
- **導入**: **1 つの** `section-card`。学習者ブロック → ナビゲーターブロックの順（両方とも画像アバター + 吹き出し）。見本の `id` は `section-dialogue-intro`。
- **全体の地図**: `h2`（Lucide + 見出し）→ リード文 → `grid gap-4 md:grid-cols-2` のカード（番号付きタイトル + 短い説明。**本スキル既定（競合1件）**では **同一競合の3側面**を各カードに **`md:col-span-2` で縦に3つ**並べる（ターゲット／提供・届け方／価格・立ち位置）。
- **用語**: **1 セクション**に `term-explain` を縦に積む（見本は「先に押さえる用語」+ `lightbulb` の `h2`）。中身の語彙ルールは term-dictionary のみが正。
- **この競合でまず押さえる3つ**: `check-circle` の `h2` → リード → `space-y-4` の行（`badge-essential` / `badge-recommended` / `badge-optional` + 見出し + 補足）。競合分析では **ターゲット／提供・届け方／価格・立ち位置** と **自分の事業との関係（勝ち筋の材料）** を各行に含める（見本の `#section-three`）。**3行の意味**は [SKILL.md](../SKILL.md) の「『この競合でまず押さえる3つ』との対応」に従う。
- **本編各セクション**（トピックごと）: `section-card` ごとに `h2`（Lucide + タイトル）→ **学習者対話（`mb-6`）→ ナビゲーター対話（`mb-6`）** → 本文（箇条書き・`rounded-lg border` のまとめ枠・2 カラムのミニ図・`<details>` など、見本にあるパターンから選ぶ）→ 必要なら `text-xs` の参考リンク行。**本スキル既定（競合1件）**では **深掘り3セクション**（例: `section-profile` プロフィールと強み／`section-offer` 商品と価格／`section-win` あなたとの比較と勝ち筋）。`id` の命名はトピックに合わせてよい。
- **まとめ**: 見本どおり `section-summary` で学習者の**自分の言葉の要約** → ナビゲーターの肯定・締め（台本の型は dialogue-personas）。
- **出典**: `section-sources` で見出し + 箇条書きリンクの一覧。最後に**免責の1段落**（見本文末の注意書きと同趣旨）。
- **目次**: `main` 内の `id` と `<nav class="toc">` の `href` を一対一で対応。命名は見本のように `section-*` で統一してよい（トピックに合わせてラベル文言だけ差し替え）。

**CSS・スクリプトの骨格**（`:root`、`.section-card`、吹き出し、バッジ、`.toc` の位置など）は [html-structure.md](html-structure.md) の基本テンプレートを正とする。見本 HTML に無いユーティリティ（例: `.code-block`）が必要ならテンプレート側の定義をそのまま使ってよい。**見本と矛盾する独自グリッドや別のカード体系は避ける。**

**`<style>` の二重管理**: 基本テンプレ内の `<style>` と [exemplar-layout.html](exemplar-layout.html) の `<style>` は同一の意味を持つ。配色・コンポーネントを変えるときは **両方を同じ内容に更新**（片方だけ直さない）。

---

## うまくいく構成（黄金見本と対応する並び）

```
1. ヘッダー（グラデーション）
   └ タイトル + 「この1枚でわかること」一行

2. 導入対話（1 枚の section-card）
   └ 学習者 → ナビゲーター（長文・用語への本音 → 一言の目的 + 地図の予告）

3. 「全体の地図」（見本: グリッドカード + 締めのたとえ1段落）
   └ 公式の見出しをそのまま並べず、自分向けに再分割。**本スキル既定**は **同一競合の3側面＝地図3ブロック**（各 `md:col-span-2`）。

4. 用語（1 セクションに term-explain を縦積み）
   └ 「この図解では〇〇と呼ぶ」を必ず入れる（詳細は term-dictionary.md）

5. この競合でまず押さえる3つ
   └ 必須 / 推奨 / 任意 などバッジで優先度（見本のカード行レイアウトに合わせる）

6. 各トピック section-card（本スキル既定では **深掘り3セクション**：プロフィール／商品と価格／比較と勝ち筋 など）
   └ h2（Lucide）→ 学習者対話 → ナビゲーター対話 → 本文・図・折りたたみ → 参考リンク行（必要に応じて）

7. まとめ対話（section-card）
   └ 台本・HTML 型は [dialogue-personas.md](dialogue-personas.md) の「まとめ」に従う（位置はこの一覧どおり）

8. 出典一覧（section-card）+ 免責1段落

9. 目次（デスクトップのみ `.toc`）— DOM 位置・マークアップは [html-structure.md](html-structure.md) の「目次（`.toc`）」。リンクは main 内 id と対応（黄金見本の並びを踏襲）
```

---

## HTML の具体例（マークアップ）

**長い HTML の SSoT は [exemplar-layout.html](exemplar-layout.html)**（＋ `images/`）。ここ（exemplar.md）に同じマークアップを二重に置かない。

補助として、head・不足時の `.code-block` などは [html-structure.md](html-structure.md) の基本テンプレート・「目次（`.toc`）」・「Lucide（よく使う）」「コード例の前の日本語」を参照する。

---

## 品質チェックリスト（作成後）

- [ ] **構造・レイアウト**が [exemplar-layout.html](exemplar-layout.html) と同型：導入1カード、地図グリッド、用語1セクション、この競合でまず押さえる3つ、本編は h2→対話2回→本文、まとめ、出典+免責、目次対応
- [ ] 初出の IT 用語に用語解説がある、または言い換えで消えている（用語ボックスに「この図解では〇〇と呼ぶ」を含める。例は [term-dictionary.md](term-dictionary.md)）
- [ ] たとえ話は [SKILL.md](../SKILL.md) の Phase 3 の要件を満たしている
- [ ] 対話まわりは [dialogue-personas.md](dialogue-personas.md) の要件を満たしている（導入・中間・まとめの構造・トーン）。**画面上の名前・ラベル文字列**は [dialogue-personas.md](dialogue-personas.md) の「役割名と画面上の名前（二層）」に従い、`exemplar-layout.html` の対話ブロックと**同一**である
- [ ] **この競合でまず押さえる3つ**または同等の強い絞り込みがあり、**見本と同じバッジ行レイアウト**になっている
- [ ] コード等を出す場合は前に「これがやること」がある（[html-structure.md](html-structure.md) の「コード例の前の日本語」と同趣旨）
- [ ] 表示・アイコン・装飾は [html-structure.md](html-structure.md) の SSoT に従っている（絵文字禁止・**対話以外**は Lucide のみ）
- [ ] 対話の左枠は**学習者・ナビゲーターとも画像**（`images/learner.png` / `images/navigator.png`）。マークアップは [dialogue-personas.md](dialogue-personas.md) の「対話左枠の画像アバター（必須）」、配置・デプロイは [html-structure.md](html-structure.md) の「対話左枠の画像アバター」どおり
- [ ] 最後に学習者が**自分の言葉**で要約している（成功の定義は [SKILL.md](../SKILL.md) の「読者・仕事・ゴール・『この競合でまず押さえる3つ』の意味」→「成功の定義（ゴール）」）
- [ ] **勝ち筋**（どこで勝つか）が本文またはまとめで**一言以上**言語化されている
- [ ] スマホで読める（`max-w-4xl`、適度な `padding`）— html-structure のテンプレートを踏襲
- [ ] **surge.sh にデプロイ済み**で、公開 URL をユーザーに渡している

---

## `diagram-maji` との違い（参照用）

**本表の役割**: 対照のための短い表のみ。[SKILL.md](../SKILL.md) の「読者・仕事・ゴール」や成功の定義の**本文**をここに書き足さない（各セルはリンク先の SSoT に寄せる）。

| 項目 | diagram-maji | diagram-personal（本スキル） |
|-----|--------------|------------------------------|
| 読者 | 一般（非エンジニア） | **自分**（詳細は [SKILL.md](../SKILL.md)「読者」のみを正とする） |
| キャラ | マジくん・マスター画像 | 対話左枠は**画像アバター必須**（学習者・ナビゲーターとも）。[html-structure.md](html-structure.md)「対話左枠の画像アバター」・[dialogue-personas.md](dialogue-personas.md)「対話左枠の画像アバター（必須）」に従う |
| 配色 | 本気AIブランド | **アバターと同じ色箱**（紫系／ローズ系＋バイオレットアクセント。[html-structure.md](html-structure.md)） |
| 成功 | 説明できる | [SKILL.md](../SKILL.md) の「成功の定義（ゴール）」のみを正とする（ここでは繰り返さない） |
