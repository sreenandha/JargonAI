# 🧠 JargonAI — Legal Document Summarizer

<p align="center">
  <img src="https://img.shields.io/badge/Model-FLAN--T5-blue?style=flat-square&logo=google" />
  <img src="https://img.shields.io/badge/Framework-PyTorch-EE4C2C?style=flat-square&logo=pytorch" />
  <img src="https://img.shields.io/badge/HuggingFace-Transformers-FFD21F?style=flat-square&logo=huggingface" />
  <img src="https://img.shields.io/badge/Hardware-NVIDIA%20A100-76B900?style=flat-square&logo=nvidia" />
  <img src="https://img.shields.io/badge/Task-Text%20Summarization-9cf?style=flat-square" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" />
</p>

> **Fine-tuned Google FLAN-T5 on legal corpora to generate plain-English summaries of dense legal text — achieving ROUGE-1: 0.340 and BERTScore F1: 0.591.**

---

## 🎯 Problem Statement

Legal documents are notoriously dense, filled with jargon that's inaccessible to non-experts. **JargonAI** tackles this by fine-tuning a pretrained seq2seq large language model (FLAN-T5) on curated legal document–summary pairs, automating the translation of complex legal language into concise, readable summaries.

---

## ⚡ Key Highlights

| | |
|---|---|
| 🤖 **Base Model** | Google FLAN-T5 (small) — instruction-tuned seq2seq LLM |
| 📊 **ROUGE-1** | **0.340** — strong lexical overlap with human-written summaries |
| 🔍 **BERTScore F1** | **0.591** — high semantic similarity to reference summaries |
| ⏱️ **Training** | 65 epochs on NVIDIA A100 GPU |
| 📄 **Domain** | Legal document summarization |
| 🔧 **Optimizer** | AdamW with gradient clipping |

---

## 🛠️ Tech Stack

```
Language Model  : google/flan-t5-small (Hugging Face)
Framework       : PyTorch + Hugging Face Transformers
Tokenizer       : T5Tokenizer
Optimizer       : AdamW
Data Splitting  : scikit-learn (train/val split)
Batching        : PyTorch DataLoader
Evaluation      : ROUGE (rouge-score), BERTScore
Environment     : Jupyter Notebook (Google Colab, A100 GPU)
```

---

## 🔄 Pipeline

```
Corpus_all.csv
      │
      ▼
┌─────────────────┐
│  Data Loading   │  60 legal document + human summary pairs
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ T5 Tokenization │  Truncate & pad inputs/targets to max model length
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Train/Val Split│  80/20 split via scikit-learn
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Fine-Tuning    │  FLAN-T5 + AdamW · 65 epochs · NVIDIA A100
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Evaluation    │  ROUGE-1: 0.340 · BERTScore F1: 0.591
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Inference     │  model.generate() on unseen legal text
└─────────────────┘
```

---

## 📐 Model Configuration

| Parameter       | Value                             |
|-----------------|-----------------------------------|
| Base model      | `google/flan-t5-small`            |
| Task type       | Sequence-to-Sequence (Summarization) |
| Tokenizer       | `T5Tokenizer`                     |
| Optimizer       | AdamW                             |
| Epochs          | 65                                |
| Batch size      | Via PyTorch `DataLoader`          |
| Hardware        | NVIDIA A100 GPU                   |
| Train/Val split | 80 / 20 (scikit-learn)            |
| Dataset size    | 60 legal document–summary pairs   |

---

## 📊 Results

| Metric             | Score     | What It Measures |
|--------------------|-----------|------------------|
| **ROUGE-1**        | **0.340** | Unigram overlap with reference summaries (lexical match) |
| **BERTScore F1**   | **0.591** | Semantic similarity to reference summaries (meaning match) |

> Both metrics evaluated on a held-out validation set. The combination of ROUGE and BERTScore ensures the model captures both surface-level accuracy and deeper semantic alignment.

---

## 📁 Repository Structure

```
JargonAI/
├── Corpus_all.csv          # 60 legal document + human summary pairs
├── Summa_rizzer.ipynb      # Full pipeline: training, evaluation & inference
└── README.md
```

---

## 🚀 How to Run

### 1. Clone the repository
```bash
git clone https://github.com/sreenandha/JargonAI.git
cd JargonAI
```

### 2. Install dependencies
```bash
pip install torch transformers scikit-learn rouge-score bert-score pandas
```

### 3. Open the notebook
```bash
# Locally
jupyter notebook Summa_rizzer.ipynb

# Or open in Google Colab (A100 GPU recommended for training)
```

> **Note:** For **inference only**, a CPU is sufficient. An A100 GPU is recommended for full fine-tuning across 65 epochs.

---

## 🔮 Future Work

- [ ] Scale dataset to 500+ legal document pairs for improved generalisation
- [ ] Experiment with `flan-t5-base` and `flan-t5-large` for higher capacity
- [ ] Add a **RAG (Retrieval-Augmented Generation)** layer for document-grounded Q&A
- [ ] Integrate **LangChain** for chained summarisation over multi-section legal contracts
- [ ] Deploy interactive demo via **Gradio** or **Streamlit**
- [ ] Benchmark against LexRank and other extractive summarisation baselines

---

## 👩‍💻 Author

**Sree Nandha Sivakumaran**
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/sreenandha)
[![GitHub](https://img.shields.io/badge/GitHub-sreenandha-181717?style=flat-square&logo=github)](https://github.com/sreenandha)

---

## 📜 License

This project is licensed under the MIT License.
