# sdlg-edu — Synthetic Data Local Generator (Education)

**英語教育向けの学習データ（Q&A 等）をローカルで大量生成し、品質チェックまで自動化するためのツール群。**  
Colab / ローカルのどちらでも動作し、**再現性（`--deterministic`）** と **品質KPI**（言語一致・5-gram重複・毒性・PII）を重視します。

> Status: Phase 4 完了（100サンプル公開 & 品質サマリー）。次は Phase 5（パッケージング＆配布）へ。

---

## 🚀 Quickstart

### 1) 取得
```bash
git clone https://github.com/<REPO_SLUG>/sdlg-edu.git
cd sdlg-edu
```

### 2) 依存インストール（ある場合）
```bash
# ある場合のみ
pip install -r requirements.txt
# パッケージ構成が整っていれば
pip install -e .
```

### 3) 生成（スクリプト直叩き）
```bash
python src/sdlg_edu/run_generate.py   --recipe recipes/grammar.jsonl   --seed 42 --deterministic   --outdir outputs   --n-per-topic 2
```
> `python -m sdlg_edu.run_generate` が使える場合はパッケージが正しくインストールされています（環境によっては直叩きを推奨）。

---

## 📦 Public Samples

- **100-sample JSONL**: `samples/english_grammar_qa_sample100.jsonl`
- **100-sample CSV**  : `samples/english_grammar_qa_sample100.csv`

まずは構造・トーン・品質の当たりを確認できます。完全版は後日リリース予定。

---

## ✅ Quality Summary

品質指標の要約は `quality_summary.md` を参照。詳細レポートは以下に出力されます：
- `outputs/report.json`
- `outputs/kpi_summary.md`

### 主要KPI（目標値）
- `language_match` ≥ **0.98**
- `dup_5gram_rate` ≤ **0.02**
- `toxicity_rate` = **0.00**
- `pii_rate` = **0.00**

---

## 🧩 レシピと再現性

- 生成仕様（トピック/パターンなど）は `recipes/*.jsonl` に定義  
- `--seed` と `--deterministic` で再現可能な結果を確保  
- 大量生成時は `--n-per-topic` とレシピ行数の積で件数をコントロール

---

## 📁 代表構成
```
sdlg-edu/
├─ recipes/                # 生成仕様（トピック・パターン）
├─ outputs/                # 生成物（*.jsonl）と品質レポート
├─ samples/                # 公開用の少量サンプル
├─ src/sdlg_edu/           # 実装（run_generate.py ほか）
├─ quality_summary.md      # 品質サマリー（人間向け要約）
└─ README.md
```

---

## 🛠 トラブルシュート

- **ModuleNotFoundError: `sdlg_edu`**  
  → パッケージ未インストール。`pip install -e .` か `python src/sdlg_edu/run_generate.py` を使用。

- **`recipes/grammar.jsonl` が見つからない**  
  → レシピのパス/ファイル名を確認（別名/別フォルダの可能性あり）。

---

## 📣 リリース計画（Phase 5 予定）

- wheel / SDist のビルド & GitHub Release
- マーケット向けメタデータ（タイトル/説明/タグ/ライセンス）
- 追加サンプル/プレビュー（Notebook/スクショ）

---

## 📜 License
TBD（後日確定）。現状は私的利用の範囲で利用可／再配布・商用化は不可（予定が決まり次第アップデート）。

---

## 📚 Citation
```
@software{sdlg-edu,
  title        = {sdlg-edu: Synthetic Data Local Generator – Education},
  year         = {2025},
  publisher    = {GitHub},
  url          = {https://github.com/<REPO_SLUG>/sdlg-edu}
}
```

---

## Dataset Availability
- Free 100-sample (Hugging Face): https://huggingface.co/datasets/kanon0111/sdlg-edu-english-qa-samples  
- Full 10k dataset (paid, Booth): https://booth.pm/ja/items/XXXXXXX

This public repository contains code, docs, and small samples only.  
**Full datasets, generation recipes, and internal pipelines are intentionally excluded.**
