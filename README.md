# AI-based Comparison of Prefrontal Cortex Activity Between Pianists and Non-Pianist Musicians
**PLOS ONE submission: PONE-D-25-12782**  
**Manuscript title:** *AI based Comparison of Prefrontal Cortex Activity Between Pianists and Non-Pianist Musicians During Score Playing and Improvisation*

[![DOI](https://zenodo.org/badge/DOI/XX.XXXX/zenodo.XXXXXXX.svg)](https://doi.org/XX.XXXX/zenodo.XXXXXXX)

This repository provides the **minimal de-identified dataset** and **analysis code** required to reproduce the key results reported in the manuscript, including **Fig. 5** and **Table VII**. The project analyzes fNIRS data from musicians during **score-playing (Task A)** and **motif improvisation (Task B)** using an **LSTM Autoencoder** (LSTM-AE) to derive reconstruction-error–based indices of neural activity, with a focus on **BA45 (IFG triangularis; channels 1 & 15)**.

---

## 📦 What’s included
- **Data (minimal, de-identified)**
  - `dataset/participants.tsv` — pseudonymous participant ID and group label (`pianist` / `non_pianist`)
  - `dataset/channels.tsv` — channel metadata (optode pairs, approximate BA labels incl. 45L/45R)
  - `dataset/task_A/` — preprocessed channel-wise time series (CSV; HbO/HbR; timestamps; markers)
  - `dataset/task_B/` — same structure for Task B
  - `dataset/markers/` — block/event timing per participant (CSV)
  - `dataset/roi_indices/roi_summary.csv` — LSTM-AE–derived ROI indices (BA45) and channel-wise reconstruction errors used for Fig. 5 / Table VII
- **Code**
  - `analysis/10_train_LSTM_AE.py` — train LSTM-AE on Task A (baseline)
  - `analysis/20_compute_recon_error.py` — compute per-window, per-channel reconstruction errors; export ROI summaries
  - `analysis/30_inferential_tests.ipynb` — reproduce Fig. 5 and Table VII (Welch t, Mann–Whitney, permutation tests; effect sizes)
  - `requirements.txt` *(or `environment.yml`)* — exact Python environment
- **Docs**
  - `README.md` (this file)
  - `LICENSE` — Code license (MIT) and Data license (CC BY 4.0)
  - `DATA_DICTIONARY.md` — variable descriptions & units

> ⚠️ No personally identifiable information (PII) is included. Participant IDs are pseudonymized.  
> If raw (unprocessed) fNIRS files are restricted by IRB, see **Data Availability** below for controlled-access instructions.

---

## 🔁 Reproducibility (quick start)
```bash
# 1) Create environment
python -m venv .venv && source .venv/bin/activate   # (Windows: .venv\Scripts\activate)
pip install -r requirements.txt

# 2) Train baseline (Task A) and save model weights
python analysis/10_train_LSTM_AE.py

# 3) Compute reconstruction errors & ROI summaries (Task B)
python analysis/20_compute_recon_error.py

# 4) Reproduce figures/tables
# Open and run cells in:
#   analysis/30_inferential_tests.ipynb
# This notebook generates Fig. 5 and Table VII in /outputs/
