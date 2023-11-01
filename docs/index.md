# Turo GitHub Actions Development Standards

## Baseline standards

We use the following standards as a baseline for all Terraform code at Turo:

- [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/)
- [Rebase & Merge](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-request-merges#rebase-and-merge-your-pull-request-commits)
  workflow
- [pre-commit](https://pre-commit.com/) for linting
- [mkdocs](https://www.mkdocs.org/) for documentation -- For full documentation
  visit [mkdocs.org](https://www.mkdocs.org).
- Formatting -- all files are formatted using appropriate language specific tools during the pre-commit phase to ensure
  baseline style is consistent.
- Action Documentation -- all actions are to be documented using the [action-docs](https://github.com/npalm/action-docs)
- Standards are enforced with code where ever possible. For example, we use [pre-commit](https://pre-commit.com/) to
  enforce formatting and linting standards.
- Scripts to rule them all -- we use [scripts to rule them all](https://github.com/github/scripts-to-rule-them-all) to
  provide consistent usage and functionality across all repositories.

This document will attempt to summarize what is important and provide links to other sources for more details and
examples.

## `pre-commit` configuration

We expect that all tf repos will have the following pre-commit configuration:

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.1.0 # Use the ref you want to point at
    hooks:
      - id: check-json
      - id: check-yaml
      - id: pretty-format-json
        args:
          - --autofix
      - id: end-of-file-fixer
      - id: trailing-whitespace
  - repo: https://github.com/pre-commit/mirrors-prettier
    rev: v2.5.1
    hooks:
      - id: prettier
        stages: [commit]
  - repo: https://github.com/alessandrojcm/commitlint-pre-commit-hook
    rev: v8.0.0
    hooks:
      - id: commitlint
        stages: [commit-msg]
        additional_dependencies: ["@open-turo/commitlint-config-conventional"]
  - repo: https://github.com/rhysd/actionlint
    rev: v1.6.8
    hooks:
      - id: actionlint
  - repo: https://github.com/jumanjihouse/pre-commit-hooks
    rev: 3.0.0 # or specific git tag
    hooks:
      - id: shellcheck
      - id: shfmt
  - repo: https://github.com/open-turo/github-actions-standards
    rev: v1.0.0
    hooks:
      - id: action-docs
```
