# copier-bioinfo-template

Copier template for Python bioinformatics projects.

## Usage

```zsh
# Generate a new project (interactive)
copier copy --trust gh:tracelail/copier-bioinfo-template ./my-project

# Generate with answers inline (non-interactive)
copier copy --trust \
  -d project_name=rna-seq-analysis \
  -d description="RNA-seq differential expression" \
  gh:tracelail/copier-bioinfo-template ./rna-seq-analysis

# Skip trace-bioutils
copier copy --trust \
  -d use_trace_bioutils=false \
  gh:tracelail/copier-bioinfo-template ./my-project
```

## Updating an existing project

When the template evolves, propagate changes to existing projects:

```zsh
cd my-existing-project
copier update --trust
```

## What gets generated

```
my-project/
├── src/my_package/          # Importable Python package
│   ├── analysis/
│   ├── data/
│   ├── visualization/
│   └── utils/
├── tests/
├── data/                    # Raw, processed, external (git-ignored)
├── notebooks/
├── results/
├── docs/
├── config/
├── pyproject.toml           # Build + ruff + mypy + pytest config
├── pixi.toml                # conda-forge + bioconda environment
├── justfile                 # Task runner
├── .pre-commit-config.yaml  # Git hooks
├── CITATION.cff             # Machine-readable citation
└── README.md
```

## Template questions

| Question | Default |
|---|---|
| `project_name` | `my-bioinfo-project` |
| `description` | `A Python bioinformatics project` |
| `author_name` | `trace` |
| `author_email` | `your@email.com` |
| `github_username` | `tracelail` |
| `license` | `MIT` |
| `python_version` | `3.13` |
| `use_trace_bioutils` | `true` |
