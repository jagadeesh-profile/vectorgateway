# Contributing to VectorGateway

Thanks for your interest in improving VectorGateway.

## Getting Started

1. Fork the repository.
2. Create a feature branch.
3. Make your changes with clear commit messages.
4. Run local quality checks before opening a PR.
5. Open a pull request with context and test notes.

## Development Setup

1. Create a virtual environment and activate it.
2. Install build tooling:

```bash
python -m pip install -U pip build twine
```

3. Build and validate package metadata:

```bash
python -m build
python -m twine check dist/*
```

## Pull Request Guidelines

- Keep PRs focused and small.
- Update README or docs when behavior changes.
- Add tests for new behavior when test scaffolding is available.
- Link issues in your PR description.

## Code Style

- Prefer clear naming and small functions.
- Keep public APIs stable or document breaking changes.
- Keep backward compatibility in mind for adapters and schemas.

## Reporting Issues

Please include:

- Reproduction steps
- Expected behavior
- Actual behavior
- Python version
- Platform information
