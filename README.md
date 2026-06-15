# BanglaForge: A Multi-Label Bengali Document Forgery Dataset with Overlapping Manipulation Annotations

[![Paper](https://img.shields.io/badge/Paper-PDF-red)]()
[![License](https://img.shields.io/badge/License-MIT-blue.svg)]()
[![Dataset](https://img.shields.io/badge/Dataset-1800%20Images-green)]()

> The first publicly available multi-label Bengali document forgery dataset, designed to reflect realistic, overlapping forgery scenarios.

---

## 📌 Overview

**BanglaForge** is a multi-label Bengali document forgery dataset containing **1,800 structurally authentic document images** spanning five document categories. It supports **five overlapping forgery classes**: Copy-Paste, Splicing, Font Inconsistency, Inpainting, and AI-Generated manipulation.

Unlike binary "forged vs. authentic" datasets, BanglaForge reflects real-world composite forgeries, where multiple manipulation types can coexist within a single document.

---

## 📂 Document Categories

1. Cash Memos
2. University Academic Marksheets
3. Certificates and Government Gazettes
4. Tender Documents
5. VAT Returns

---

## 🏷️ Forgery Taxonomy

| Label | Description |
|-------|-------------|
| **Copy-Paste (CP)** | Replication of portions of text, stamps, and signatures within the document |
| **Splicing (SP)** | Concatenation of content from two or more sources, resulting in boundary/lighting discontinuities |
| **Font Inconsistency (FI)** | Inconsistent font types, sizes, and spacing — especially Bangla digits |
| **Inpainting (IP)** | Deletion and recreation of information using conventional fill techniques |
| **AI-Generated (AG)** | Synthetic regions generated via Nano Banana 2 and ChatGPT Images 2.0 |

---

## 🖼️ Sample Images

<!-- PLACE: Fig. 1 - Original and forged document samples (Cash Memo & Tender examples) -->
<p align="center">
  <img src="assets/fig1_samples.png" width="800">
  <br>
  <em>Original and forged document samples from BanglaForge dataset. Forged parts are circled in red.</em>
</p>

---

## 📊 Dataset Statistics

- **Total images:** 1,800
- **Split:** 70% train (1,260) / 15% validation (270) / 15% test (270)
- **Annotation:** Two annotators with consensus protocol
- **Inter-annotator agreement:** Mean per-class Cohen's κ = 0.81 (computed independently per label as binary present/absent)

<!-- PLACE: Fig. 2 - Class distribution and label co-occurrence matrix -->
<p align="center">
  <img src="assets/fig2_stats.png" width="800">
  <br>
  <em>(a) Class distribution across five forgery types. (b) Normalized label co-occurrence matrix.</em>
</p>

---

## 🧠 Benchmarks

### A. Vision Transformer (ViT) Generalization Study

Four ViT-based architectures were fine-tuned with weighted binary cross-entropy loss, label co-occurrence priors, and class-wise threshold calibration.

| Model | P | R | F1 | mAP | Hamming Loss |
|---|---|---|---|---|---|
| EVA02-Base | 0.512 | 0.701 | 0.581 | 0.603 | 0.182 |
| **ViT-L (ROPE)** | **0.548** | 0.728 | **0.620** | **0.641** | **0.165** |
| DeiT3-Large | 0.405 | **0.929** | 0.533 | 0.598 | 0.214 |
| Swin-Base | 0.476 | 0.803 | 0.575 | 0.617 | 0.176 |

<!-- PLACE: Fig. 3 - Training dynamics of ViT models (Validation F1 & Loss curves) -->
<p align="center">
  <img src="assets/fig3_training_dynamics.png" width="800">
  <br>
  <em>Training dynamics of ViT models: (a) Validation F1 curves, (b) Validation loss curves for EVA02-Base and DeiT3-L.</em>
</p>

---

### B. Zero-Shot LVLM Evaluation

Three frontier Large Vision-Language Models were evaluated zero-shot using structured two-stage JSON-based prompting.

| Model | Macro F1 | Hit@1 | Hit@3 |
|---|---|---|---|
| Qwen3.6-Plus | 0.572 | **0.667** | **1.000** |
| Claude Sonnet 4.6 | 0.447 | 0.600 | 0.800 |
| Gemini 2.5 Pro | **0.650** | 0.500 | 0.700 |

<!-- PLACE: Fig. 4 - Radar chart comparing ViT-L (ROPE) vs LVLMs across 6 metrics -->
<p align="center">
  <img src="assets/fig4_radar_chart.png" width="500">
  <br>
  <em>ViT Architecture Comparison on BanglaForge Test Set across Precision, Recall, F1, mAP and Hamming Loss.</em>
</p>

---

### C. Per-Class Performance

<!-- PLACE: Fig. 5 - Per-class F1 heatmap for all models -->
<p align="center">
  <img src="assets/fig5_heatmap.png" width="700">
  <br>
  <em>Per-class F1 heatmap for all models. Blue = high F1; red = low F1. White line separates fine-tuned ViTs (top) from zero-shot LVLMs (bottom).</em>
</p>

**Key findings:**
- 🟢 **AI-Generated** content is the easiest category across all models (F1 ≈ 0.86–0.97)
- 🔴 **Inpainting** and **Copy-Paste** are hardest for LVLMs (F1 ≈ 0.15–0.18); fine-tuned ViTs perform better (F1 ≈ 0.42–0.58)
- 🔵 **Font Inconsistency** shows the largest paradigm gap — LVLMs (especially Gemini 2.5 Pro, F1 ≈ 0.95) outperform fine-tuned ViTs (F1 ≈ 0.37–0.42)

---

## 💡 Key Insights

1. Fine-tuned ViTs offer consistent, balanced performance across all five forgery categories.
2. AI-generated forgeries are reliably detected by all models (F1 near 1.0).
3. A **hybrid approach** is recommended: ViTs for pixel-level manipulations (copy-paste, inpainting), LVLMs for semantic/layout-level inconsistencies (font changes, stylistic mismatches).

---

## 🇧🇩 Bengali-Specific Challenges

- Complex conjunct consonants make font substitution harder to detect
- Bengali numerals differ from Western numerals, limiting transfer learning from English-oriented systems
- Mixed Bengali-English text adds detection complexity

---

## 📥 Download

> **Dataset will be released here upon paper acceptance.**

```bash
git clone https://github.com/MehediAhamed/BanglaForge.git
```

<!-- PLACE: Download links / Google Drive / Hugging Face dataset links -->

---

<!-- PLACE: Update structure to match actual repo layout before release -->

---


## 📄 License

<!-- PLACE: Specify license (e.g., MIT, CC BY 4.0) -->
This dataset is released under the [LICENSE NAME] license.
