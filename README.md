# DehazeFormer-BCF (Artifact for Peer Review) — **Anonymous / Read‑Only**

**EN / 中文双语说明** · **Last updated:** 2025-11-10

> **Purpose (EN):** This repository is an **anonymous artifact for peer review** of our TVC submission.
> It contains **inference & evaluation code** plus **pretrained checkpoints** to verify the **main tables** in the paper.
> **Training code and internal data pipelines are withheld** during the review phase and will be released upon acceptance.
>
> **用途（中文）：** 本仓库为**同行评审匿名工件**，随稿提供。包含**推理与评测代码**及**预训练权重**，用于**核验论文主表**。
> **训练代码与内部数据处理脚本在评审阶段不公开**，将于录用后发布。

---

## 1. What is included / 本工件包含

- `src/` Minimal **inference** and **evaluation** scripts.
- `weights/` Pretrained checkpoints for **1–2 core benchmarks** (e.g., SOTS‑Outdoor, Dense‑Haze).
- `configs/` Example eval configs (paths, device, precision).
- `TRAINING/` High‑level training overview and a **template** config (no runnable training scripts).
- `LICENSE` **Evaluation‑Only** license (review phase).
- `CITATION.cff` Citation metadata.
- `LINKS.txt` Official dataset links (**to be filled with URLs you use**).

> ⚠️ **Scope:** This artifact is for **evaluation only**. Redistribution, derivative works, or re‑publication are **not permitted** during review.

---

## 2. Quick start / 快速开始

### 2.1 Create environment / 创建环境
```bash
# (A) Use conda + pip (recommended)
conda create -n dehaze-bcf python=3.10 -y
conda activate dehaze-bcf
pip install -r requirements.txt  # or: pip install -r requirements.txt --extra-index-url https://download.pytorch.org/whl/cu121

# (B) Or use environment.yml
# conda env update -n dehaze-bcf -f environment.yml
```

> **Torch build note:** Install the **CPU** build for CPU‑only machines, or the **CUDA‑matched** build for NVIDIA GPUs.

### 2.2 Data placement / 数据放置
Download datasets (RESIDE SOTS‑Indoor/Outdoor, **O‑HAZE**, Dense‑Haze, Rain1400, Test2800) via **official links** (see `LINKS.txt`).
Organize as:
```
<DATA_ROOT>/
  SOTS_OUT/
    hazy/*.png
    gt/*.png
  DenseHaze/
    hazy/*.png
    gt/*.png
  OHAZE/
    hazy/*.png
    gt/*.png
  Rain1400/
    rainy/*.png
    gt/*.png
  Test2800/
    rainy/*.png
    gt/*.png
```

### 2.3 One‑command evaluation / 一键评测
```bash
# Example: SOTS-Outdoor (RGB metrics by default)
python src/infer.py --cfg configs/eval_sots_outdoor.yaml
python src/eval.py  --pred outputs/sots_outdoor --gt <DATA_ROOT>/SOTS_OUT/gt --save-csv outputs/sots_outdoor_metrics.csv

# Example: Dense-Haze (set metric to RGB or Y, see --help)
python src/infer.py --cfg configs/eval_densehaze.yaml
python src/eval.py  --pred outputs/densehaze --gt <DATA_ROOT>/DenseHaze/gt --metric rgb --save-csv outputs/densehaze_metrics.csv
```

**Expected ranges（示例占位）/ 期望范围（占位）**  
- **SOTS‑Outdoor:** PSNR ≈ 37.56 ± 0.05, SSIM ≈ 0.980 ± 0.002  
- **Dense‑Haze:** PSNR ≈ 17.30 ± 0.05, SSIM ≈ 0.76 ± 0.01  
> 请将上方数值替换为你的实际主表范围。

---

## 3. Reproducibility policy / 可复现实务

- This artifact **verifies the main tables** via inference & evaluation.  
- **Training code** and advanced data pipelines will be **released upon acceptance** under a research‑friendly non‑commercial license.  
- We include **checksums** to ensure integrity.

### SHA‑256 checksums / 摘要校验
After zipping the artifact (e.g., `artifact.zip`) and preparing weights, compute SHA‑256 and paste here:
```
artifact.zip  SHA256 = <TO BE FILLED>
weights/BCF_SOTSoutdoor.pth  SHA256 = <TO BE FILLED>
...
```

---

## 4. License summary / 许可证摘要
**Evaluation‑Only (review phase)** — see `LICENSE` for full terms.  
- **Permitted:** Download and run for **peer‑review evaluation**.  
- **Prohibited:** Redistribution, derivative works, re‑publication, and any **commercial** use.

**录用后**：将以**研究友好、非商用**许可发布完整仓库（含训练脚本）。

---

## 5. Anonymity & contact / 匿名与联系
This artifact is anonymized for peer review. Any questions can be raised **via the editorial system**.  
本工件为匿名评审用途，若有问题请通过**期刊编辑系统**沟通。

---

## 6. Repository layout / 仓库结构
```
dehazeformer-bcf-anon/
├─ README.md
├─ LICENSE
├─ CITATION.cff
├─ LINKS.txt
├─ requirements.txt
├─ environment.yml
├─ src/
│  ├─ infer.py
│  ├─ eval.py
│  ├─ models/
│  │  ├─ __init__.py
│  │  └─ model_def.py          # placeholder; default identity model unless replaced
│  └─ utils/
│     ├─ io_utils.py
│     └─ metrics.py
├─ weights/
│  ├─ BCF_SOTSoutdoor.pth      # to be added by authors
│  └─ README_weights.md
├─ configs/
│  ├─ eval_sots_outdoor.yaml
│  └─ eval_densehaze.yaml
└─ TRAINING/
   ├─ README_training.md
   └─ templates/
      └─ train_config_template.yaml
```

---

## 7. How to cite / 引用方式
See `CITATION.cff`. A DOI‑backed archive will be provided **upon acceptance**.
