# Action Repos

Open-Turo has two different types of action repos:

- single actions
- action suites

## Single action repos

These are the default standard for actions. They are appropriate when you have a standalone action that does not have
other related actions. Examples of this:

- [action-pre-commit]()
- [action-???]

## Action Suites

We have found that it is quite common to want to have sets of related actions that either apply to a platform (jvm,
node, terraform, etc.) or apply to a function (semantic-release). In these cases, we use directories inside of action
repos to group actions together.

For example, the actions-jvm repo provides four different high level actions:

- lint
- test
- prerelease
- build-docker

This provides two functions:

1. it groups like actions together where they are easier to maintain
2. the high level actions allow for code repos to have very simple github action workflow files

There is an example of a jvm based repo's CI yaml file

```yaml
name: CI

on:
  pull_request:
    branches:
      - main

jobs:
  lint:
    name: Lint
    runs-on: [self-hosted, general-ubuntu]
    steps:
      - uses: open-turo/actions-jvm/lint@v1
        with:
          checkout-repo: true
          github-token: ${{ secrets.GITHUB_TOKEN }}
          artifactory-username: ${{ secrets.ARTIFACTORY_USERNAME }}
          artifactory-auth-token: ${{ secrets.ARTIFACTORY_AUTH_TOKEN }}

  test:
    name: Test
    runs-on: [self-hosted, general-ubuntu]
    steps:
      - uses: open-turo/actions-jvm/test@v1
        with:
          checkout-repo: true
          github-token: ${{ secrets.GITHUB_TOKEN }}
          artifactory-username: ${{ secrets.ARTIFACTORY_USERNAME }}
          artifactory-auth-token: ${{ secrets.ARTIFACTORY_AUTH_TOKEN }}
```

### Language & Platform Action Suites

When creating actions for repos, we suggest erring on the side of having simple action workflow files in the workflows
that utilize appropriate action suites to abstract away functionality. This makes it easier for people to onboard new
repositories and makes it easier to perform maintenance actions across all repos that are using these actions.
