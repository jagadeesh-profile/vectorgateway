# VectorGateway

Protocol middleware for translating vector data across providers, vector databases, and LLM pipelines.

## Project Status

VectorGateway is currently in **alpha** (`v0.1.1`).

The package is published and installable, and the public API currently exposes:

- Package metadata/version (`vectorgateway.__version__`)

Core protocol adapters and translation primitives are planned and will be introduced incrementally.

## Why VectorGateway

VectorGateway is designed as a protocol layer between embedding providers, vector databases, and downstream LLM applications.

Long-term goals:

- Normalize vector records into a consistent internal schema
- Translate data contracts between vector database formats
- Make provider and backend swaps easier in RAG systems
- Reduce lock-in by standardizing handoff boundaries

## Installation

Install from PyPI:

```bash
pip install vectorgateway
```

Install from source for local development:

```bash
git clone https://github.com/jagadeesh-profile/vectorgateway.git
cd vectorgateway
python -m pip install -U pip
python -m pip install -e .
```

## Quick Start

```python
import vectorgateway

print(vectorgateway.__version__)
```

## Roadmap

Planned areas of implementation include:

- Canonical vector record schema
- Adapter interface for embedding/vector backends
- Format translators for common vector database payloads
- Validation and compatibility helpers for ingestion/retrieval pipelines

## Development

Build and validate package artifacts:

```bash
python -m pip install -U pip build twine
python -m build
python -m twine check dist/*
```

## Contributing

Contributions are welcome. See the project guidelines:

- [Contributing](CONTRIBUTING.md)
- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Security Policy](SECURITY.md)

## Links

- PyPI: https://pypi.org/project/vectorgateway/
- Repository: https://github.com/jagadeesh-profile/vectorgateway
- Issues: https://github.com/jagadeesh-profile/vectorgateway/issues
