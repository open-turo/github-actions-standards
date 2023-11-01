# Conventional Commit message structure

Commit messages in code repositories are expected to follow the conventional-commit standards as defined
by [conventionalcommits.org](https://www.conventionalcommits.org/en/v1.0.0/).

### GitHub Actions

The following table describes the meaning of our conventional commits within the usage of a GitHub Action repository.

Remember that the purpose of conventional commits is to track the API changes. In the case of GitHub actions, that
includes the inputs, outputs, functional behavior, calling context etc.

| Type     | Release?               | Description                                                                                      |
| -------- | ---------------------- | ------------------------------------------------------------------------------------------------ |
| feat     | :white-check-mark: yes | Adding new functionality, in particular to the API. New inputs & outputs would be a new feature. |
| fix      | :white-check-mark: yes | Modifying existing functionality or fixing a bug.                                                |
| docs     | :x: no                 | Changes to documentation - both markdown files and comments                                      |
| chore    | :x: no                 | Changes that don't modify resource or test files - modifying scripts, repository config          |
| ci       | :x: no                 | Changes to continuous integration - GHA workflows                                                |
| refactor | :x: no                 | Changes which do not affect the public behavior                                                  |
| revert   | :x: no                 | Permanently revert a change                                                                      |
| style    | :x: no                 | Changes due to code style, whitespace, or documentation linting                                  |
| build    | :x: no                 | Do not use - use CI instead                                                                      |
| perf     | :x: no                 | Do not use                                                                                       |
| test     | :x: no                 | Do not use - deployments do not have tests at this time.                                         |

#### Scope

- undefined at this time

#### Breaking change

This must be specified if the change will break any current usages of the GitHub action.

This is best implemented through deprecation first to add new/replacement functionality followed up with remove of the
now unused functionality.

When creating a breaking change - you MUST include a markdown document in the `docs/breaking-changes` directory. It
should be named `v<version>.md` where `<version>` is the new/breaking version. This document should explain the breaking
change and how to migrate to the new version.
