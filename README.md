# AI/ML Engineering Portfolio

Senior AI & Computer Vision Engineer. Production background in multimodal models, RAG pipelines, LLM fine-tuning, and agentic systems across fintech, business workflows, HR tech, social media, and ESG compliance domains.

---

## Projects

| # | Project | Domain | Problem Addressed | Stack |
|---|---|---|---|---|
| 1 | [Prompt Benchmark Interface](#1-prompt-benchmark-interface) | Financial NLP | Reproducible prompt strategy evaluation without API dependencies | Ollama, Gradio, HuggingFace |
| 2 | [Resume Analyzer](#2-resume-analyzer) | HR Tech | Semantic candidate ranking with explainable scoring, beyond keyword matching | RAG, LangChain, FAISS, ChromaDB |
| 3 | [LatentSync Enhanced with Optical Flow](#3-latentsync-enhanced-with-optical-flow) | Multimodal / Video Gen | Temporal motion incoherence in lip-sync diffusion models | PyTorch, OpenCV, DeepCache |
| 4 | [LoRA Fine-tuning Pipeline](#4-lora-fine-tuning-pipeline) | Scientific NLP | Domain-specific LLM fine-tuning on consumer hardware with semantic evaluation | PEFT, LoRA, TRL, DPO, HuggingFace |

---

## Stack

```
Models        Diffusion models, LLaMA variants, Qwen, CLIP, EfficientNet
LLM Infra     Ollama, HuggingFace Transformers, PEFT/LoRA, TRL, DPO
RAG           LangChain, FAISS, ChromaDB, LLM-as-judge
CV            PyTorch, OpenCV, optical flow, DeepCache
Interfaces    Gradio, FastAPI
```

---

## Project Details

---

### 1. Prompt Benchmark Interface
**Domain:** Financial NLP | LLM evaluation

**Problem:** Comparing prompt strategies — zero-shot, few-shot, Chain-of-Thought, Self-Consistency — on financial Q&A requires reproducible, side-by-side benchmarks. Ad-hoc notebook runs produce no baselines and no comparability across iterations. API-dependent tooling is unsuitable for sensitive financial data.

**Solution:** Fully offline benchmarking system running local LLMs via Ollama. Covers prompt strategy comparison on stock market Q&A with interactive parameter tuning and metrics visualization — designed for fast, reproducible iteration without external dependencies.

| Component | Detail |
|---|---|
| LLM runtime | Ollama (fully local, no API calls) |
| Strategies compared | Zero-shot, few-shot, CoT, Self-Consistency |
| Domain | Financial Q&A, stock market data (BeautifulSoup) |
| Interface | Gradio — parameter tuning + metrics dashboard |

[View repo](https://github.com/emedinac/PromptBenchmarkInterface)

---

### 2. Resume Analyzer
**Domain:** HR tech | Recruiting automation

**Problem:** Keyword-matching ATS systems reject qualified candidates by ignoring semantic relationships between skills, experience, and role requirements. A backend engineer with 8 years of Kotlin experience fails a "5+ years Kotlin" filter. Hiring decisions need explainability — a score alone is not actionable for a recruiter.

**Solution:** RAG-based evaluation system that retrieves semantically relevant candidate profile sections, generates a quantitative compatibility score, and produces a qualitative explanation per decision — grounded in retrieved evidence, not black-box inference.

| Component | Detail |
|---|---|
| Retrieval | RAG over candidate profiles |
| Vector stores | FAISS, ChromaDB |
| Orchestration | LangChain |
| Evaluation | LLM-as-judge for qualitative scoring |
| Interface | Gradio |

[View repo](https://github.com/emedinac/ResumeAnalyzer)

---

### 3. LatentSync Enhanced with Optical Flow
**Domain:** Multimodal generative models | Audio-visual synthesis

**Problem:** Lip-sync diffusion models optimize for per-frame appearance quality but lack explicit temporal motion constraints. The result is mouth movements that are visually plausible in isolation but incoherent across frames — a known limitation of LatentSync. The VideoJAM framework demonstrated that joint appearance-motion representations improve motion coherence in video generation; this had not been applied to talking-face synthesis.

**Contribution:** Modified LatentSync's loss function to incorporate optical flow as an auxiliary motion supervision signal, enforcing temporal consistency between frames during training. Profiled for inference performance using DeepCache. Evaluated exclusively on HDTF (high-resolution audio-visual dataset for talking face generation).

| Component | Detail |
|---|---|
| Base model | [LatentSync](https://arxiv.org/abs/2412.09262) |
| Motion supervision | Optical flow via OpenCV, inspired by [VideoJAM](https://arxiv.org/abs/2502.02492) |
| Inference optimization | DeepCache |
| Evaluation | HDTF dataset |
| Framework | PyTorch, HuggingFace Transformers |

[View repo](https://github.com/emedinac/LatentSync)

---

### 4. LoRA Fine-tuning Pipeline
**Domain:** Scientific literature | NLP research

**Problem:** Fine-tuning LLMs for domain-specific research Q&A (arXiv, PubMed) without API access requires parameter-efficient methods that fit on consumer hardware. Standard BLEU and ROUGE-L metrics measure n-gram overlap but miss semantic correctness — a paraphrastic correct answer scores near zero. BERTScore is necessary for meaningful evaluation in this domain.

**Solution:** End-to-end framework for fine-tuning and evaluating open LLMs using LoRA, with DPO alignment and three-metric evaluation (BLEU, ROUGE-L, BERTScore). No external APIs — full pipeline runs locally.

| Component | Detail |
|---|---|
| Parameter-efficient tuning | PEFT, LoRA |
| Alignment | TRL, Direct Preference Optimization (DPO) |
| Evaluation metrics | BLEU, ROUGE-L, BERTScore |
| Tasks | Q&A, summarization |
| Datasets | arXiv, PubMed |
| Framework | HuggingFace Transformers |

[View repo](https://github.com/emedinac/Lora4Research)
