# Pull Request standards

Our baseline standards follow
teh [GitHub: Best practices for pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/getting-started/best-practices-for-pull-requests)

## Additional standards and expectations

### Standard names for checks

When creating status checks, we expect the following names to be used:

- Lint
- Test
- PR Lint

#### Lint

Perform linting checks on the codebase. This should include checks for formatting, style, and other linting checks. It
is suggested to use a tool such as pre-commit to perform these checks.

#### Test

When you have the ability to run tests, we expect them to run on all PRs and report as `Test`.

#### PR Lint

Not only should you look into writing good code and commits, but your pull requests should also be written with
intention. Where possible, we should add appropriate linting. These should repot as `PR Lint`.

##### Checkboxes

Adding checkboxes to PRs is a really powerful way to help reviewers understand what you have done and what you expect to
be done. We suggest the following checkboxes be added to PRs:

- Use [actions-pr-lint](https://github.com/open-turo/actions-pr-lint) to validate PR checklists
- Use the reusable workflow in this repo to lint your PRs
- Have a required check for `PR Lint`

The `check-pr-checklist` action validates that all markdown checkboxes in the PR body are checked. No special HTML
comments or indicators are needed — all checkboxes are validated by default.

```
#### :heavy_check_mark: Checklist

- [ ] Added or updated documentation
- [x] Tests for new functionality and regression tests for bug fixes
```

#### Adding PR Lint Action

Add the following file to your `.github/workflows` directory:

```shell
cat << EOF > .github/workflows/ci.pr-lint.yaml
name: CI

on:
  pull_request:
    types: [edited, opened, reopened, synchronize]
    branches: [main]

jobs:
  pr-lint:
    name: PR Lint
    uses: open-turo/github-actions-standards/.github/workflows/reusable-workflow.pr-lint.yaml@v1
    secrets: inherit
EOF
```
