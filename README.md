# 🧠 SCCR AI Agent – Enterprise RAG Assistant
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-green)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100%2B-black)](https://fastapi.tiangolo.com)
[![llama.cpp](https://img.shields.io/badge/llama.cpp-vulkan-blue)](https://github.com/ggerganov/llama.cpp)
[![PWA](https://img.shields.io/badge/PWA-Enabled-green)](https://web.dev/progressive-web-apps/)
![SCCR AI Agent UI](docs/Screen Shot 2025-11-11 at 10.10.59.png)

> **Internal AI Assistant for SCCR Indonesia**  
> A secure, factual, and production-ready Retrieval-Augmented Generation (RAG) system built with **Llama-3**, **FastAPI**, and **PWA** — designed for corporate use with full transparency and data governance.

⚠️ **Disclaimer**: This is a **technical demonstration** using **publicly available information** from [sccr.id](https://sccr.id). Not an official product of SCCR Indonesia.

---

## 🔍 Overview

SCCR AI Agent enables employees to ask questions about:
- Company vision, mission, and structure
- Stem cell & cancer research protocols
- Product specifications (Secretome, CTL, etc.)
- Facilities and certifications

...and get **accurate, source-backed answers** — without relying on the model’s outdated or hallucinated knowledge.

### ✨ Key Features
- ✅ **RAG-powered** with internal knowledge base
- ✅ **Local LLM**: Runs `Meta-Llama-3.1-8B-Instruct` via `llama.cpp` (no cloud, no data leakage)
- ✅ **Transparency**: Every AI response shows its source (e.g., `company_profile.md`)
- ✅ **PWA + APK-ready**: Works on browser and mobile (Cordova)
- ✅ **Dark/light mode**, message actions (copy, delete, regenerate)
- ✅ **Production-ready**: Logging, health checks, Docker support
- ✅ **Secure by design**: No external data sent; all processing on-premise

---

## 🏗️ Architecture

```mermaid
flowchart LR
    A[PWA / APK] -->|HTTP| B(FastAPI Orchestrator\n:8002)
    B --> C{RAG Retrieval}
    C -->|Query| D[(Vector Store\nFAISS + MiniLM)]
    B -->|Prompt + Context| E[llama.cpp Server\n:8001]
    E -->|Streamed Response| B
    B -->|Response + Sources| A
