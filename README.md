# 🛡️ AI-Powered Intrusion Prevention System

> Master's Thesis  Distributed Information Systems Engineering and Security (ISIDS)
> University of Batna 2 — Faculty of Mathematics and Computer Science
> Defended June 2, 2026 

An AI-driven Intrusion Prevention System capable of distinguishing malicious network flows from legitimate traffic in real time, benchmarked on **700,000+ real NetFlow records** across a 5-phase experimental pipeline covering classical Machine Learning, ensemble methods, and Deep Learning (Transformers).

📄 **[Read the full thesis (PDF)](./AI_Powered_IPS_Thesis_Abdenebi_Chaker.pdf)**

---

## 👥 Authors


| **Abdenebi Taha Abdelmalik** | [GitHub](https://github.com/tahx00) · [LinkedIn](https://www.linkedin.com/in/tahaabdenebi) |
| **Chaker Abdelhafid** | [GitHub](https://github.com/Chaker-AB) |

**Supervisor:** Dr. Boubechal Ikram — Batna 2 University

---

## 📌 The Problem

Traditional IPS solutions rely on static signatures and predefined rules. They work — until they meet a zero-day exploit, polymorphic malware, or encrypted traffic. Then they're blind. This thesis investigates whether AI/ML can close that gap while satisfying the primary security constraint of any real-world IPS: **minimizing missed attacks (False Negatives), even more than minimizing false alarms.**

## 🔬 Methodology — 5 Experimental Phases

Built on the **NF-CSE-CIC-IDS2018-v2** NetFlow dataset (University of Queensland), 700K rows, 41 features:

| Phase | What we did |
|---|---|
| **1. Baseline ML** | 9 classifiers on the full 41-feature space (SVM, Decision Tree, Random Forest, AdaBoost, Bagging, LightGBM, XGBoost, Stacking, Soft Voting) |
| **2. PCA** | Dimensionality reduction retaining 95% variance |
| **3. Feature Selection** | Supervised selection (Random Forest importance) → top 20 features |
| **4. Ensemble Learning** | Soft Voting, Stacking, AdaBoost, Bagging |
| **5. Deep Learning** | MLP, TabNet (attention-based), FT-Transformer (self-attention on tabular data) |

Cross-dataset generalization was additionally validated against **NF-UNSW-NB15-v2** as an independent benchmark.

## 🏆 Key Results

| Model | Accuracy | Recall | FPR | **FNR** | Missed Attacks |
|---|---|---|---|---|---|
| **LightGBM** (full features) | 99.9993% | 100.0000% | 0.0008% | **0.0000%** | **0 / 15,870** |
| FT-Transformer (Deep Learning) | 99.9935% | 99.9874% | 0.0057% | 0.0126% | 2 / 15,870 |
| Stacking / Soft Voting (Ensemble) | 99.9993% | 99.9937% | 0.0000% | 0.0063% | 1 / 15,870 |

✅ **LightGBM on the full feature space achieved a perfect 0.0000% False Negative Rate** on the held-out test set — zero attacks slipped through.

✅ Ensemble strategies (Stacking, Soft Voting) delivered the strongest overall balance between detection and false-alarm elimination.

✅ Among Deep Learning architectures, the **FT-Transformer** was the standout performer, confirming that transformer self-attention generalizes well beyond NLP to tabular network traffic.

✅ PCA-based dimensionality reduction did **not** improve results — it discards discriminative information. Supervised feature selection (top 20/41 features) preserved near-baseline performance instead.

## 🧠 Most Discriminative Features (Random Forest, top 5)

`DURATION_IN` · `L7_PROTO` · `FLOW_DURATION_MILLISECONDS` · `SRC_TO_DST_AVG_THROUGHPUT` · `TCP_WIN_MAX_OUT`

— confirming that **timing behavior and flow duration** are primary indicators of malicious traffic in this dataset.

## 🛠️ Tech Stack

**Language:** Python 3
**Data:** Pandas, NumPy
**Classical ML:** Scikit-learn (SVM, Decision Tree, Random Forest, AdaBoost, Bagging), XGBoost, LightGBM
**Deep Learning:** TensorFlow/Keras (MLP), PyTorch + `pytorch-tabnet` (TabNet), PyTorch + `rtdl_revisiting_models` (FT-Transformer)
**Evaluation:** Confusion Matrix, ROC-AUC, Matplotlib
**Environment:** Google Colab (CPU runtime), Google Drive storage

## 📊 Dataset

- **Primary:** [NF-CSE-CIC-IDS2018-v2](https://rdm.uq.edu.au/files/ce5161d0-ef9c-11ed-827d-e762de186848) — 700K NetFlow records, 41 features, Open Access
- **Benchmark:** [NF-UNSW-NB15-v2](https://espace.library.uq.edu.au/view/UQ:ffbb0c1) — independent generalization test

## 📖 Thesis Structure

1. Cybersecurity fundamentals — offensive/defensive security, attack taxonomy, IPS role in the defensive ecosystem
2. AI in Cybersecurity — ML/DL foundations, XAI, offensive AI, defensive applications across threat categories
3. Datasets — feature engineering, selection methodology, experimental setup
4. Proposed Approach — 5-phase results, model comparison, final evaluation
5. General Conclusion & future work

## 🚀 Future Work

- Improve detection of stealthy, low-volume attacks (Infiltration class was excluded due to poor separability)
- Cross-dataset generalization at larger scale
- Adversarial robustness testing
- Explainable AI (SHAP/LIME) integration for analyst-facing decisions
- Real-time deployment testing

## 📬 Contact

Questions or collaboration ideas? Reach out via [LinkedIn](https://www.linkedin.com/in/tahaabdenebi) or open an issue on this repo.

---

*If you find this work useful, consider ⭐ starring the repo.*
