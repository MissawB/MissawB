<div align="center">

# Hi, I'm Wassim Bahmani 👋

**Final-year engineering student · Data Science & AI · IMT Nord Europe**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)]([https://www.linkedin.com/in/wassim-bahmani-5a0287255)
[![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co/MissawB)
[![Email](https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:wassim.bahmani@imt-nord-europe.fr)

</div>

---

I'm a final-year engineering student at **IMT Nord Europe** (Lille), in the RAISE track (Responsible AI & Data Science), class of 2027, after three years of CPGE MPSI/MP*.

The problems I enjoy most are the ones where the hard part is the evaluation: a model that has to generalize to inputs it has never seen, training labels produced by another model, a benchmark that a single split cannot settle. My recent projects reflect that: hand-written test charters that no training example resembles (IRL Guard), expert-labelled studies kept out of training (RSNA Knee), frame-shuffling tests and subject-wise cross-validation (KTH).

🎯 **Looking for a 6-month end-of-studies internship starting February or March 2027**, in an R&D or applied research team (machine learning, computer vision, LLMs).

---

## 💼 Experience

**Assistant Engineer Intern, AI automation** · Dadum · Gozo, Malta · *Apr – Aug 2026*
- Automated the production of e-learning micro-courses with AI agents, in a two-person team. My part: the content injection runner (TypeScript, Playwright, Fastify), image generation and automated LinkedIn posting.
- Set up Docker-based CI/CD to Hugging Face Spaces.

**Full-Stack Developer Intern** · Nickel (BNP Paribas group) · Charenton-le-Pont · *May – Aug 2025*
- Built REST APIs in Java / Spring Boot on an Oracle database, in hexagonal architecture, with 80% test coverage enforced in CI.
- Cut API response times from about 2 minutes to about 5 seconds.
- Built ReactJS interfaces used daily by internal teams.

---

## 🔭 Featured Projects

### 🛡️ [IRL Guard](https://huggingface.co/spaces/MissawB/irl-guard-demo): charter-driven content blocker for IRL livestreams
> *Python · YOLO · ByteTrack · RapidOCR · NudeNet · Qwen3.5-2B · LoRA (Unsloth) · XGBoost · Gradio*

A streamer filming in the street broadcasts things they don't control: a street name near home, a phone number on a shop window, a knife on a table. IRL Guard detects them in the video and decides, element by element, to **broadcast**, **blur** or **pause** the stream, following a charter the streamer writes in plain language. The same detection leads to different decisions depending on context: a knife is fine in a cooking stream, not in the street.

- **Research question:** can a small fine-tuned LLM apply a charter it has never seen, where a tabular classifier collapses? On 20 hand-written charters whose wording never appears in training (1,000 cases), fine-tuned Qwen3.5-2B reaches **79.1% accuracy**, against 53.1% for deterministic rules and 46.0% for XGBoost on TF-IDF.
- **Safety first:** on its own, the model still lets 29% of sensitive cases through. The default mode keeps the more protective of the rules' and the model's decisions, which cuts leakage to **5.5%**. Any model error (timeout, invalid output, crash) produces a blur, never a broadcast.
- **What it taught me:** v1 learned the *words* of the training templates, not the concept: 84.6% on synthetic charters but 59.9% on hand-written ones. v2 (2B model, about 20 phrasings per sanction, test expressions blacklisted from training) gained 19 points.
- 237 tests that run without GPU or network, plus an end-to-end anti-leak test with real OCR.

[Live demo](https://huggingface.co/spaces/MissawB/irl-guard-demo) · [Models & datasets](https://huggingface.co/collections/MissawB/irl-guard-6ac9ea0b623e8e00170b6ffd)

---

### 🩻 [RSNA Knee Abnormality Detection](https://www.kaggle.com/competitions/rsna-knee-abnormality-detection): Kaggle competition
> *PyTorch · DINOv2 · CoAtNet · attention-MIL · Qwen3.8 · Kaggle kernels (2× T4)*

Detect 12 findings per knee MRI study, scored by mean AUC.

- **Two model families, blended by rank averaging:** a DINOv2-B ViT applied per slice, with a slice mixer and one query head per finding (up to 336 px), and a 2.5D CoAtNet-384 on slice triplets with an attention-MIL head per finding, reading up to 96 slices per study at native resolution.
- **Labels from reports:** training labels are soft labels produced by an LLM from the radiology reports, blended with three public label sets after per-finding normalization. The 58 expert-labelled studies are kept for evaluation only.
- **0.950 mean AUC on the public leaderboard**, up from 0.928 for the best single model.

---

### 🎭 [Animetix](https://github.com/MissawB/Animetix): AI game & discovery platform for anime, manga, movies and games
> *Django · React / TypeScript · PostgreSQL + pgvector · Neo4j · Ollama · Qwen3.8-27B (QLoRA) · CLIP · GCP Cloud Run (L4 GPU) · OpenTelemetry*
 
Solo research project: 16 game modes, a bilingual (FR/EN) interface, image search, a manga reader and a set of experimental AI labs, built in hexagonal architecture with dependency injection. It ran in production on GCP until October 2026 and now runs locally.
 
- **Agentic RAG:** a semantic router classifies each query, specialized processors gather evidence (vector retrieval, Neo4j graph traversal, web research), a synthesizer writes the answer and a judge rates its faithfulness, all streamed live over Server-Sent Events.
- **One L4 GPU for everything:** a VRAM lease time-shares a 27B text model (18.4 GB of the card's 24 GB) with vision, diffusion, video and audio models, evicting the least recently used one when the next does not fit. All 12 GPU routes verified end to end on the L4.
- **An honest fine-tune:** a QLoRA adapter on the 27B, [published on Hugging Face](https://huggingface.co/MissawB/otaku-qwen38-27b-adapter). It improved recall on its synthetic held-out split (0.331 → 0.431) but scored below the base model on an independently written 77-question gold set (0.340 vs 0.471): it learned the *form* of an expert answer, not more knowledge.
- Games built on real algorithms (Akinetix picks each question by exact expected information gain), image search with CLIP and CCIP encoders over pgvector, an 80% coverage gate in CI and Playwright end-to-end tests.

---

### 🎥 [Deep Learning with PyTorch](https://github.com/MissawB/deep-learning-pytorch): from MLPs to CLIP, plus a video action recognition study
> *PyTorch · PyTorch Geometric · Hugging Face transformers / diffusers · OpenCV · MediaPipe*

17 notebooks covering CNNs, Transformers, generative models, GNNs and multimodal learning, with most models written from scratch (attention, ViT, VAE, GCN, mini-GPT, mini-CLIP). The featured team project benchmarks **five spatio-temporal architectures on KTH** (MobileNetV2 features or GCN skeleton graphs, with mean pooling, LSTM or Transformer heads).

- Subject-wise splits, 10–11 seeds per model, bootstrap confidence intervals over test subjects and subject-wise 5-fold cross-validation (**87.5 ± 4.1%** for the best model).
- Shuffling the test frames costs the Transformer **0 points**: on KTH, accuracy comes from per-frame appearance, not temporal order. Sampling frames inside annotated action segments raises every head by **+6.5 to +11.8 points**, more than any change of temporal head.

---

### 🎮 [From Folksonomy to Ontology: Steam game mechanics](https://github.com/MissawB/Game-Mechanics-Classification-Steam)
> *Pandas · scikit-learn · XGBoost · Sentence-BERT · NetworkX · SQLite*

Research project turning the noisy user tags of **126,000+ Steam games** into reliable game-mechanics metadata: FP-Growth association rules, lift-weighted co-occurrence network, Louvain / OPTICS / K-Medoids clustering, ML classification, and Sentence-BERT embeddings to measure diachronic semantic drift (PMI).

---

### 🏃 [Text-to-Motion Retrieval](https://github.com/MissawB/Text-to-Motion): 🥈 Top 2
> *PyTorch · MPNet · BiGRU · InfoNCE*

Joint embedding space aligning natural-language descriptions with 3D human motion sequences, focused on two-person interactions (hugs, handshakes). Contrastive training with InfoNCE, evaluated by Recall@K. **Top 2** in the challenge.

---

### 📺 [Anime Data Platform](https://github.com/YasserMourabih/anime-data-platform)
> *Dagster · PostgreSQL (Neon) · scikit-learn · Streamlit · AniList GraphQL API*

Big Data course project: 25,000+ anime extracted from the AniList API and orchestrated with Dagster on a weekly schedule, TF-IDF recommendations (70% metadata / 30% synopsis) served through Streamlit, plus a Higher-or-Lower score guessing game.

---

## 🧩 More Projects

| Project | What it is | Stack |
|---|---|---|
| [SonicMatch](https://github.com/MissawB/SonicMatch) | Genre classification with conformal prediction, and a Shazam-like audio fingerprinting engine | scikit-learn · XGBoost · Librosa · Streamlit |
| [Flappy Bird NEAT](https://github.com/MissawB/Flappy_Bird_RL_Project) | Agent evolved with NeuroEvolution of Augmenting Topologies, with genealogy tracking and replay | NEAT · Pygame |
| [EPS MultiScore](https://github.com/MissawB/EPS-Innov) | Live sports-performance data collection app, piloted with a school volleyball class | Kivy |
| Transformer from scratch | The original encoder-decoder Transformer rebuilt in 80 steps, down to Adam, the Noam schedule, label smoothing and beam search (Deep-ML) | PyTorch |

---

## 🛠️ Tech Stack

- **Languages:** Python · SQL · Java · TypeScript
- **Machine learning:** PyTorch · Hugging Face transformers · LoRA (Unsloth) · scikit-learn · XGBoost · PyTorch Geometric · Sentence-Transformers
- **Computer vision:** DINOv2 · CoAtNet · YOLO · ByteTrack · OpenCV · MediaPipe
- **LLM applications:** LangChain · RAG · n8n · Gradio
- **Data & back end:** PostgreSQL · Oracle · Neo4j · Dagster · Kafka · Spring Boot · Fastify · Django
- **Infra & tooling:** Docker · CI/CD · GCP (Cloud Run) · Hugging Face Spaces · uv · pytest · Playwright
- **Front end & visualization:** React · Streamlit · Plotly · Matplotlib

---

## 📜 Certifications & Coursework

- **IBM Generative AI Engineering** Professional Certificate (Coursera, 16 courses, 2026)
- **IBM AI Engineering** Professional Certificate (Coursera, 13 courses, 2026)
- **Stanford CME 295**: Transformers & Large Language Models
- **Stanford CME 296**: Diffusion & Large Vision Models
- **Google Cloud**: Transformer Models and BERT Model (Coursera, 2026)
- **École Polytechnique**: Introduction to Probability, Parts 1 & 2 (Coursera, 2026)

**Selected IMT Nord Europe coursework (RAISE track)**
- *Mathematics:* Monte Carlo methods, continuous optimization, metaheuristics, estimation & detection, graph theory
- *Machine learning:* advanced supervised & unsupervised learning, deep learning & MLOps, image and time-series analysis
- *Systems & responsible AI:* Big Data architectures (batch & stream processing), data security, AI ethics & data law
- *Current semester:* advanced deep learning for vision and text, 3D computer vision & geometry, reinforcement learning & decision-making under uncertainty, AI for healthcare

---

## 🌟 Languages & Interests

🇫🇷 French (native) · 🇬🇧 English (B2)

`🏃 Open-source` · `🌍 Sustainability` · `🤖 LLMs & GenAI` · `📐 Mathematics` · `📚 Cross-cultural reading`

---

<div align="center">

*"Turning noise into signal - whether in data, tags, or tokens."*

</div>
