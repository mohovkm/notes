### Pre-commit config

### Installing pre-commit module:
```bash
pip install pre-commit
```

### Installing pre-commit hook
```bash
pre-commit install
```

# Running against all files
```bash
pre-commit run --all-files
```

.pre-commit-config.yaml
```yml
repos:
  - repo: https://github.com/PyCQA/isort
    rev: 5.6.4
    hooks:
      - id: isort
  - repo: https://github.com/psf/black
    rev: 20.8b1
    hooks:
      - id: black
  - repo: https://github.com/gvanderest/pylama-pre-commit
    rev: 0.1.2
    hooks:
      - id: pylama
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.0.1
    hooks:
      - id: check-merge-conflict
      - id: debug-statements
      - id: end-of-file-fixer
      - id: no-commit-to-branch
        args: [--branch, develop, --branch, master]
default_language_version:
  python: python3.7

```