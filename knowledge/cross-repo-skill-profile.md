# Cross-Repo Skill & Thinking Profile
# 石丸浩司（Koji Ishimaru）

**作成日**: 2026-04-03  
**データソース**: koji140 GitHub 全リポジトリを横断的に読み、構造化したもの  
**目的**: 自分のスキル・思考様式・行動パターンを一元的に記述し、AI・他者との協業の前提とする

---

## 1. 一言で表すと

> 複雑で曖昧な業務・判断・知識を「実際に動く構造」に変え、再利用可能な資産として残す。

---

## 2. バックグラウンド（キャリアの流れ）

| 期間 | 組織 | 役割 |
|------|------|------|
| 1995–2006 | 首都高速道路 | 土木技術者・国際インフラ協力 |
| 2006–2011 | Booz Allen Hamilton | シニアアソシエイト（経営コンサルタント） |
| 2011–2024 | Amazon（Japan/US/Brazil） | Product Manager → Sr. PM → Concept Designer |
| 2024–2025 | KAKEAI Inc. | Head of Product Management |
| 2026– | Hi-Serve Co., Ltd. | 代表取締役（アドバイザリー・コンサルティング） |
| 2026– | 首都高速道路アソシエイト | DX戦略コンサルタント |

**学歴**: MIT 構造工学修士（2002）、東京大学工学研究科 修士/学士（1993/1995）

---

## 3. コアスキル（本質的な強み）

### 3-1. 業務を「回る状態」に変える設計力

単に資料を作るのではなく、人・役割・手順・データ・責任分界まで含めて、  
**現実に運用できる最小構成を設計する**。

実例（リポジトリから）:
- `kinsetsu-process`: Web受付プロセス全体の責任分界・フロー・DBを一体設計
- `bridge-inspection-v2`: 点検業務のGAS+ChatGPT+Cloudflareシステム設計
- `receipt-agent`: 領収書処理の全パイプライン（OCR → 科目判定 → Sheets登録）設計

---

### 3-2. 境界（Interface）から考える

「誰がやるか」より先に「どこまでが誰の責任か」「どこで受け渡すか」を決める。

> 例（kinsetsu-process）:  
> 「回付メール + 案件番号 + 案件フォルダURL」が境界  
> 境界より前 → アソシエイト責任  
> 境界より後 → 局責任

この考え方はシステム設計・業務設計・組織設計すべてに一貫して現れる。

---

### 3-3. 正本（Single Source of Truth）を決める

情報が増えるほど「何を基準に判断するか」を明定する。

実例:
- `resume/source/en/resume.md` が正本、日本語版は派生物
- `kinsetsu-process/docs/process-design.md` がすべての変更の基準
- `tax-handbook/source/` が原文、`scenarios/` が整理版

---

### 3-4. 層を分ける（Layer Separation）

原文・整理版・証拠書類・実行物・説明物を混ぜない。役割が違うものは保存先も分ける。

全リポジトリに共通するパターン:

| 層 | 例 |
|----|-----|
| 原文（Source） | `source/` `records/` |
| 整理版（Scenarios/Design） | `scenarios/` `docs/` |
| 実行物（Output） | `outputs/` `gas/` `html/` |
| 説明物（Guide） | `GUIDE_*.md` `skill.md` |
| 資産管理（Reusable） | `knowledge/` `prompts/` `templates/` |

---

### 3-5. 最小運用から始めて段階的に拡張（MVO: Minimum Viable Operation）

最初から完成形を目指さず、人手で回る最小構成を置き、改善と自動化を重ねる。

実例:
- `kinsetsu-process`: 4月は「Web受付のみ」→ 5月以降に判定図受領まで拡張
- `bridge-inspection-v2`: GASのPoC → Cloudflare経由でGPT統合
- `receipt-agent`: OCR確認 → 勘定科目自動判定 → 銀行照合（段階的)

---

### 3-6. 試行錯誤を資産化する

失敗・未解決・つまずきをそのまま捨てず、次に使える形で残す。

実例:
- `bridge-inspection-v2/docs/KNOWN_BUGS_AND_PITFALLS.md`
- `receipt-agent/docs/receipt-agent-lessons.md`（バグ取り記録・教訓）
- `kinsetsu-process/docs/decision-log/`（判断根拠のログ）

---

### 3-7. AIを実行者として組み込む

AIに「いい感じにやって」と丸投げせず、人が設計・判断し、AIが実行しやすい形に分解して渡す。

分担の原則（personal-operating-system.md より）:

| 人がやること | AIがやること |
|------------|------------|
| 目的設定 | 構造化 |
| 判断基準の決定 | 文書化 |
| 正本の決定 | 選択肢の整理 |
| 曖昧さの解消 | 差分反映案の作成 |
| 最終判断 | 反復作業の代行 |

実例:
- GAS+Cloudflare+ChatGPT のパイプライン設計（橋梁点検・領収書）
- `social-post-gpt`: 過去投稿データを知識化してカスタムGPTに食べさせる
- `travel`: Claude + スクリプトで旅行insights自動提案

---

## 4. 思考様式（問題の捉え方）

問題を前にしたとき、ほぼ常に以下の順序で考える：

```
1. これは何の問題か
2. どこが曖昧なのか
3. 何を正本にするか
4. どの層に分けるべきか
5. 境界はどこか
6. 最小運用は何か
7. どう残せば次に使えるか
```

**判断原則（decision-principles.md より）**:

| 原則 | 内容 |
|----|-----|
| 正本優先 | 正本から先に直す。派生物は正本に従う |
| 層分離 | 原文・整理版・証拠・実行物を混ぜない |
| Interface First | 境界を先に定義する |
| MVO | 最小運用 → 段階的拡張 |
| Explanation over Assertion | 条件・前提・例外・リスクを結論とセットで書く |
| Reusable by Default | 1回きりで終わらせず、命名・構造・保存先を次回も使える形にする |
| Human Judgment, AI Execution | AIには具体差分と禁止事項を明示して渡す |
| Preserve Friction | つまずいた点を消さない。その摩擦が改善ポイント |

---

## 5. テクニカルスキル（GitHubの実装から）

| 技術 | 使用リポジトリ / 用途 |
|------|----------------------|
| Google Apps Script (GAS) | bridge-inspection-v2, receipt-agent: バックエンドCRUD・PDF生成 |
| Cloudflare Workers | bridge-inspection-v2, receipt-agent: OpenAI→GAS APIブリッジ（CORS回避） |
| OpenAI Vision API | receipt-agent: 領収書OCR |
| Custom GPT (Actions) | bridge-inspection-v2, social-post-gpt, travel: フロントエンドUI |
| Python | social-post-gpt, travel, pvr-vacancy-scraper: データ処理・スクリプト |
| JavaScript / Node.js | pvr-vacancy-scraper: Playwrightスクレイピング |
| Playwright | pvr-vacancy-scraper: ブラウザ自動化 |
| Mermaid / Flowchart | kinsetsu-process, conversation-intelligence: 図表設計 |
| GitHub | 全リポジトリ: 知識管理の基盤インフラ |

---

## 6. ドメイン知識

| ドメイン | 深度 | 関連リポジトリ |
|---------|------|--------------|
| インフラ・土木 | 専門（11年の実務） | kinsetsu-process, bridge-inspection-v2 |
| B2Bプロダクトマネジメント | 専門（Amazon 6年） | resume |
| 物流・フルフィルメント設計 | 専門（Amazon FC設計） | resume |
| 経営コンサルティング | 実務（5年） | resume, kinsetsu-process |
| 日本税務（中小法人） | 実務的理解 | tax-handbook |
| AI活用・自動化 | 実装レベル | receipt-agent, bridge-inspection-v2 |
| 個人知識管理（PKM） | 実装・実践中 | km-memory |
| SNS・コミュニケーション設計 | 実践中 | social-post-gpt, km-memory |
| 旅行・ライフデザイン | 構造化実践中 | travel |

---

## 7. 活動中のプロジェクト分類

### 実務 DX（業務プロセス設計）
- `kinsetsu-process`: 近接施工協議Web受付 PoC運用中（2026年4月〜）
- `kinsetsu-form`: 申請フォームのHTML+GASシステム
- `bridge-inspection-v2`: 首都高高架下点検マップ・報告書システム

### 自動化ツール（AI + Infra）
- `receipt-agent`: 領収書処理パイプライン（OCR→Sheets→銀行照合）
- `pvr-vacancy-scraper`: ホテル空室情報スクレイパー（Playwright）

### 知識管理・自己理解
- `resume`: 英文正本→日本語派生、スキル・判断原則の文書化
- `km-memory`: 人間関係AIサポートの知識ベース
- `social-post-gpt`: 過去SNS投稿の知識化→カスタムGPT

### 探索・研究
- `conversation-intelligence`: 対話ログ構造化・パターン化の特許ドラフト
- `tax-handbook`: 税務判断の説明可能な資産化

### ライフスタイル
- `travel`: 旅行記録・計画・insights管理

---

## 8. ストレス源と力が出る状態

**ストレスを感じやすい状態:**
- 正本が曖昧
- 責任分界が不明確
- 「具体的な差分」でなく「抽象的な要約」しか返ってこない
- 実行者への指示に判断余地が残りすぎている
- 構造なしに情報が増え続ける

**力が出る状態:**
- 基準資料が明確に存在する
- 層が分かれている
- 判断理由が残せる
- 小さく始めて改善できる
- AIとの役割分担が明確

---

## 9. 今後の課題・強化領域

（resume/context/personal-operating-system.md より）

1. 自分のスキルを外部に伝わる言葉で表現すること
2. 構造化能力をキャリア上の強みとして提示すること
3. GitHub上の実例を汎用的なポートフォリオに翻訳すること

---

## 10. このプロファイルの使い方

AIセッション開始時に参照することで:
- 指示の背景を汲んだ応答が可能になる
- 曖昧な指示でも思考パターンに沿った補完ができる
- 出力の構造・粒度が期待値に近くなる

**更新タイミング**: 新規リポジトリ作成時、または大きなプロジェクトの節目に更新する。
