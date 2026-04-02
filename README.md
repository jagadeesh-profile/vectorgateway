<div align="center">

# 🌐 VectorGateway

**Any model. Any database. Zero friction.**

Protocol middleware for translating vector data across LLM providers and vector databases — without re-embedding.

[![PyPI version](https://badge.fury.io/py/vectorgateway.svg)](https://badge.fury.io/py/vectorgateway)
[![Python](https://img.shields.io/pypi/pyversions/vectorgateway)](https://pypi.org/project/vectorgateway/)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Discord](https://img.shields.io/discord/YOUR_DISCORD_ID?label=Discord&logo=discord)](https://discord.gg/YOUR_INVITE)
[![GitHub Stars](https://img.shields.io/github/stars/jagadeesh-profile/vectorgateway?style=social)](https://github.com/jagadeesh-profile/vectorgateway)

</div>

---

## The Problem

When you build a RAG pipeline with OpenAI embeddings and Pinecone, you're locked in. Switch to LLaMA or Weaviate and you have to re-embed everything — costing time, money, and weeks of engineering work.

```
# Today — tightly coupled, impossible to swap
embeddings = OpenAIEmbeddings()        # locked to OpenAI
vectorstore = Pinecone(embeddings)     # locked to Pinecone
# Change either one → re-embed 100k documents
```

## The Solution

VectorGateway sits between your LLM and your vector database. It translates vectors into a universal space — so any model can query any index it didn't create.

```python
from vectorgateway import VectorGateway

vg = VectorGateway(
	embedder="openai",
	database="pinecone",
)

# Index your documents once
vg.index(documents=["doc1", "doc2", "doc3"])

# Switch models anytime — zero re-indexing
vg.switch_embedder("llama")
results = vg.query("your question")  # still works
```

---

## How It Works

```
Your App
	│
	▼
VectorGateway SDK
	│
	├── Embedding Layer (OpenAI / LLaMA / Gemini / Cohere)
	│
	├── Translation Engine (Universal Vector Space)
	│        └── Linear Projection  →  sub-millisecond
	│        └── Neural Adapter     →  higher quality (v0.2)
	│
	└── Connector Layer
			 ├── Pinecone
			 ├── Weaviate
			 ├── ChromaDB
			 ├── FAISS
			 └── Qdrant
```

**Under 5ms end-to-end.** Translation happens via learned projection matrices — pure matrix multiplication, no network calls.

---

## Installation

```bash
pip install vectorgateway
```

Install with your preferred providers:

```bash
pip install "vectorgateway[openai,pinecone]"
pip install "vectorgateway[llama,weaviate]"
pip install "vectorgateway[all]"
```

---

## Quickstart

### 1. Basic RAG Pipeline

```python
from vectorgateway import VectorGateway

# Initialize with any embedder + any database
vg = VectorGateway(
	embedder="openai",
	database="pinecone",
	embedder_config={"api_key": "sk-..."},
	database_config={"api_key": "...", "index_name": "my-index"},
)

# Index documents
documents = [
	"Seagate reported revenue of $1.8B in Q3 2024.",
	"The new HDD model supports PCIe Gen 5.",
	"Enterprise storage demand grew 23% YoY.",
]
vg.index(documents=documents)

# Query
results = vg.query("What is Seagate's revenue?", top_k=3)
for r in results:
	print(r.text, r.score)
```

### 2. Switch Models Without Re-Indexing

```python
# Your index was built with OpenAI
vg = VectorGateway(embedder="openai", database="pinecone", ...)
vg.index(documents=documents)

# Switch to LLaMA — no re-embedding needed
vg.switch_embedder("llama")
results = vg.query("same question, different model")
# Returns accurate results instantly
```

### 3. Cross-Database Migration

```python
# Migrate from Pinecone to Weaviate in one line
vg.migrate(source="pinecone", target="weaviate")
# No data loss. No re-embedding. No downtime.
```

### 4. Drop Into LangChain

```python
from vectorgateway.integrations import VectorGatewayRetriever

retriever = VectorGatewayRetriever(
	embedder="openai",
	database="chromadb",
)

# Use as a standard LangChain retriever
chain = RetrievalQA.from_chain_type(
	llm=llm,
	retriever=retriever
)
```

---

## Supported Providers

### Embedding Models
| Provider | Status |
|---|---|
| OpenAI (text-embedding-3) | ✅ Supported |
| Meta LLaMA 3 | ✅ Supported |
| Google Gemini | 🔜 Coming soon |
| Cohere | 🔜 Coming soon |
| Mistral | 🔜 Coming soon |

### Vector Databases
| Database | Status |
|---|---|
| Pinecone | ✅ Supported |
| Weaviate | ✅ Supported |
| ChromaDB | ✅ Supported |
| FAISS | ✅ Supported |
| Qdrant | 🔜 Coming soon |
| pgvector | 🔜 Coming soon |

---

## Benchmarks

| Operation | Latency | Notes |
|---|---|---|
| Vector translation | < 1ms | Matrix projection |
| Pinecone query | ~2ms | p1 tier |
| End-to-end pipeline | < 5ms | Cached embeddings |
| Cold query (no cache) | ~50ms | Includes embedding call |

Benchmarks run on AWS c5.xlarge. See [`benchmarks/`](benchmarks/) for full results.

---

## Roadmap

- [x] Linear projection translator
- [x] Pinecone + Weaviate + ChromaDB + FAISS connectors
- [x] OpenAI + LLaMA embedders
- [ ] Neural adapter translator (higher quality)
- [ ] Gemini + Cohere + Mistral embedders
- [ ] Qdrant + pgvector connectors
- [ ] LangChain + LlamaIndex integrations
- [ ] Async support
- [ ] Rust core for maximum performance
- [ ] Managed cloud service

---

## Contributing

VectorGateway is built in the open. Contributions are welcome and appreciated.

```bash
git clone https://github.com/jagadeesh-profile/vectorgateway
cd vectorgateway
pip install -e ".[dev]"
pytest tests/
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.
Check [good first issues](https://github.com/jagadeesh-profile/vectorgateway/issues?q=label%3A%22good+first+issue%22) to get started.

---

## Community

- 💬 **Discord** — [Join the VectorGateway server](https://discord.gg/YOUR_INVITE)
- 🐛 **Issues** — [GitHub Issues](https://github.com/jagadeesh-profile/vectorgateway/issues)
- 💡 **Discussions** — [GitHub Discussions](https://github.com/jagadeesh-profile/vectorgateway/discussions)
- 🐦 **Twitter** — Follow for updates

---

## License

Apache 2.0 — see [LICENSE](LICENSE) for details.

---

<div align="center">


</div>
