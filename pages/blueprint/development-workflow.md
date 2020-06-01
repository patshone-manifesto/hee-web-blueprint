---
layout: layouts/page.njk
title: Development workflow
pageTitle: Development workflow
pageDescription: What's the process for developing on the platform?
path: /blueprint
permalink: /blueprint/development-workflow.html
eleventyNavigation:
  subgroup: Development
  parent: Blueprint
  key: Development workflow
  order: 12
---

## Development Workflow

Development workflows are implemented using [Github Actions](https://github.com/features/actions). Find below workflows that are implemented so far for CI/CD.

### Continuous Integration (CI) Workflow

When a commit had been made to any branch except `develop`/`release/**` or a PR has been made, then Continuous Integration workflow (`.github/workflows/ci.yml`) would be triggered which would essentially compile & test the project.

### Continuous Deployment (CD) Workflows
#### Development Environment [`master` should be replaced with `develop` when ready]
When a commit (essentially merge commits) had been made to `master`, then Continuous Deployment workflow (`.github/workflows/ci-and-cd-dev.yml`) would be triggered which would perform both Continuous Integration & Deployment to brCloud `development` environment.

#### Test Environment (disabled temporarily) [TODO: yet to be tested & verified]
When a commit (essentially merge commits) had been made to `release/**`, then Continuous Deployment workflow (`.github/workflows/ci-and-cd-tst.yml`) would be triggered which would perform both Continuous Integration & Deployment to brCloud `test` environment. This would also deploy the release package onto Github Packages artefact repo.

TODO:

Add notes describing:

- states and transitions
- source control workflow (Git Flow, etc )
- ticket management (JIRA) ?