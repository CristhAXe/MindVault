# MindVault

A local AI knowledge workspace built with Memorwise, Ollama and Obsidian.

MindVault combines local LLMs with RAG to search and chat with your own documents without relying on external APIs.

## Features

- Local AI inference with Ollama
- Semantic search using Memorwise
- PDF and document indexing
- Docker-based deployment
- Obsidian knowledge workflow
- Fully local data storage

## Architecture

```
Documents
    |
    v
Memorwise (RAG + Search)
    |
    v
Ollama (Local LLM)
    |
    v
Obsidian (Notes)
```

## Stack

- Memorwise
- Ollama
- Docker
- Obsidian
- Qwen / Llama models

## Setup

Clone the repository:

```bash
git clone https://github.com/CristhAXe/AI-Powered-Personal-Knowledge-System.git
cd mindvault
```

Start services:

```bash
docker compose up -d --build
```

Run Ollama and download a model:

```bash
ollama pull qwen2.5:7b
```

Open:

```
http://localhost:4747
```
## Docker Benefits

- No dependency conflicts
- Portable environment
- Easy setup and deployment
- Simple service management
- Clean host system
- Reproducible configuration

## Purpose

MindVault is a personal knowledge system setup for studying, organizing documents and building a local AI assistant.

It is an integration project built on top of existing open-source tools.
