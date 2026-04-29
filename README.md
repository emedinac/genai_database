# AI/ML Engineering Portfolio

Senior AI and Computer Vision Engineer with production experience in multimodal models, RAG pipelines, LLM fine-tuning, and agentic systems. Background spans fintech, HR tech, ESG compliance, and video generation.

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

Comparing prompt strategies across iterations — zero-shot, few-shot, Chain-of-Thought, Self-Consistency — requires reproducible baselines. Notebook-based runs don't give you that, and API-dependent tooling is a non-starter for sensitive financial data.

This is a fully offline benchmarking system running local LLMs via Ollama. It covers prompt strategy comparison on financial Q&A with interactive parameter tuning and metrics visualization. The emphasis is on fast iteration without external dependencies or data leaving the machine.

| Component | Detail |
|---|---|
| LLM runtime | Ollama (fully local) |
| Strategies | Zero-shot, few-shot, CoT, Self-Consistency |
| Domain | Financial Q&A, stock market data (BeautifulSoup) |
| Interface | Gradio — parameter tuning + metrics dashboard |

[View repo](https://github.com/emedinac/PromptBenchmarkInterface)

---

### 2. Resume Analyzer
**Domain:** HR tech | Recruiting automation

Standard ATS systems match keywords, which means a backend engineer with eight years of Kotlin experience can fail a "5+ years Kotlin" filter. Beyond the retrieval problem, a compatibility score alone isn't useful to a recruiter — they need to know why.

This system uses RAG to retrieve semantically relevant sections of a candidate profile, produces a quantitative compatibility score, and generates a qualitative explanation grounded in the retrieved evidence. Every decision is traceable back to a specific passage, not a black-box inference.

| Component | Detail |
|---|---|
| Retrieval | RAG over candidate profiles |
| Vector stores | FAISS, ChromaDB |
| Orchestration | LangChain |
| Evaluation | LLM-as-judge |
| Interface | Gradio |

[View repo](https://github.com/emedinac/ResumeAnalyzer)

---

### 3. LatentSync Enhanced with Optical Flow
**Domain:** Multimodal generative models | Audio-visual synthesis

LatentSync optimizes per-frame appearance quality but has no explicit temporal motion constraint. The result is mouth movements that look plausible in isolation but lose coherence across frames. VideoJAM showed that joint appearance-motion representations improve temporal consistency in video generation — this work applies that idea to talking-face synthesis.

The modification adds optical flow as an auxiliary motion supervision signal in LatentSync's loss function, directly penalizing frame-to-frame inconsistency during training. Inference was profiled and optimized with DeepCache. Evaluation used HDTF, a high-resolution audio-visual dataset designed specifically for talking-face generation.

| Component | Detail |
|---|---|
| Base model | [LatentSync](https://arxiv.org/abs/2412.09262) |
| Motion supervision | Optical flow (OpenCV), inspired by [VideoJAM](https://arxiv.org/abs/2502.02492) |
| Inference optimization | DeepCache |
| Evaluation dataset | HDTF |
| Framework | PyTorch, HuggingFace Transformers |

[View repo](https://github.com/emedinac/LatentSync)

---

### 4. LoRA Fine-tuning Pipeline
**Domain:** Scientific literature | NLP research

Fine-tuning LLMs for domain-specific Q&A on arXiv and PubMed without API access means working within the constraints of consumer hardware. LoRA handles that. The harder problem is evaluation: BLEU and ROUGE-L measure n-gram overlap, so a semantically correct paraphrase scores near zero. BERTScore is necessary for this domain to mean anything.

The pipeline covers fine-tuning with LoRA, alignment with DPO, and three-metric evaluation — BLEU, ROUGE-L, and BERTScore. Everything runs locally with no external API calls.

| Component | Detail |
|---|---|
| Parameter-efficient tuning | PEFT, LoRA |
| Alignment | TRL, DPO |
| Evaluation | BLEU, ROUGE-L, BERTScore |
| Tasks | Q&A, summarization |
| Datasets | arXiv, PubMed |
| Framework | HuggingFace Transformers |

[View repo](https://github.com/emedinac/Lora4Research)
