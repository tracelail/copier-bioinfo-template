# copier-bioinfo-template

Copier template for Python bioinformatics projects. Generates a fully
configured project with pixi environments, ruff linting, mypy type checking,
pre-commit hooks, and optional trace-bioutils integration.

## Generating a new project

```zsh
# Interactive — prompts for all answers
copier copy --trust gh:tracelail/copier-bioinfo-template ./my-project

# Non-interactive — supply answers inline
copier copy --trust \
  -d project_name=rna-seq-analysis \
  -d description="RNA-seq differential expression" \
  -d author_name="Trace Lail" \
  -d author_email="your@email.com" \
  -d github_username=tracelail \
  gh:tracelail/copier-bioinfo-template ./rna-seq-analysis

# Without trace-bioutils
copier copy --trust \
  -d use_trace_bioutils=false \
  gh:tracelail/copier-bioinfo-template ./my-project
```

After generation, set up the project:

```zsh
cd my-project
just setup       # installs environment + activates pre-commit hooks
just check       # verify everything works
```

## Template questions

| Question | Default | Notes |
|---|---|---|
| `project_name` | `my-bioinfo-project` | kebab-case, becomes package name |
| `description` | `A Python bioinformatics project` | one-line summary |
| `author_name` | `trace` | |
| `author_email` | `your@email.com` | |
| `github_username` | `tracelail` | used in URLs and badges |
| `license` | `MIT` | MIT / BSD-3-Clause / Apache-2.0 / GPL-3.0-only |
| `python_version` | `3.13` | minimum Python version |
| `use_trace_bioutils` | `true` | include personal utility library |

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

## Updating an existing project

When this template is updated (new hooks, improved config, bug fixes), pull
those changes into any project generated from it:

```zsh
cd my-existing-project

# Preview what would change without applying
copier update --trust --pretend

# Apply the update
copier update --trust
```

Or use the justfile shortcuts built into every generated project:

```zsh
just template-preview    # preview changes
just template-update     # apply changes
```

Copier performs a three-way merge between the old template output, the new
template output, and your project's current state. If there are conflicts,
`.rej` files are created next to the conflicting files. Resolve them manually,
delete the `.rej` files, then commit.

## Updating this template itself

When making improvements to the template:

```zsh
cd ~/projects/copier-bioinfo-template

# Make your changes to files in template/
# or update copier.yml questions

# Commit
git add .
git commit -m "describe what changed"

# Tag a new version — required for copier update to work in generated projects
git tag v0.2.0
git push origin master --tags
```

Version tagging follows semver loosely:
- **patch** (v0.1.1) — fix a bug in generated files, bump a hook version
- **minor** (v0.2.0) — add a new file, new recipe, new question
- **major** (v1.0.0) — breaking change to project structure

## Related repositories

- [trace-bioutils](https://github.com/tracelail/trace-bioutils) — personal
  bioinformatics utility library included as an optional dependency
