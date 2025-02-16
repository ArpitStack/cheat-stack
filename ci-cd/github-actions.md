# GitHub Actions CI/CD CheatSheet

A comprehensive guide covering essential GitHub Actions workflows and configurations for continuous integration and deployment.

## Table of Contents

- [Understanding GitHub Actions](#understanding-github-actions)
- [Workflow Basics](#workflow-basics)
- [Triggers](#triggers)
- [Jobs & Steps](#jobs--steps)
- [Runners](#runners)
- [Environment Variables & Secrets](#environment-variables--secrets)
- [Caching Dependencies](#caching-dependencies)
- [Matrix Builds](#matrix-builds)
- [Reusable Workflows](#reusable-workflows)
- [Debugging & Monitoring](#debugging--monitoring)

## Understanding GitHub Actions

GitHub Actions automates CI/CD workflows using YAML-based configuration files stored in `.github/workflows/`.

## Workflow Basics

A simple GitHub Actions workflow:

```yaml
name: CI Workflow
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
      - name: Install Dependencies
        run: npm install
      - name: Run Tests
        run: npm test
```

## Triggers

Workflows can be triggered by various events:

- `push` – Runs on every push to a branch.
- `pull_request` – Runs on PR creation or update.
- `schedule` – Runs on a cron schedule.
- `workflow_dispatch` – Manually triggered workflows.

Example scheduled trigger:

```yaml
on:
  schedule:
    - cron: '0 0 * * 1'  # Runs every Monday at midnight
```

## Jobs & Steps

- **Jobs** define independent tasks.
- **Steps** execute commands or actions within a job.

Example:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
      - name: Run Tests
        run: pytest
```

## Runners

Runners execute workflows on different environments:

- `ubuntu-latest`
- `windows-latest`
- `macos-latest`

Self-hosted runners can be used for custom environments:

```yaml
runs-on: self-hosted
```

## Environment Variables & Secrets

Set environment variables:

```yaml
env:
  NODE_ENV: production
```

Use GitHub Secrets:

```yaml
steps:
  - name: Use Secret
    run: echo "${{ secrets.MY_SECRET }}"
```

## Caching Dependencies

Speed up workflows by caching dependencies:

```yaml
steps:
  - name: Cache Node Modules
    uses: actions/cache@v4
    with:
      path: ~/.npm
      key: npm-cache-${{ runner.os }}-${{ hashFiles('**/package-lock.json') }}
      restore-keys: npm-cache-${{ runner.os }}-
```

## Matrix Builds

Run jobs on multiple environments:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [16, 18, 20]
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
```

## Reusable Workflows

Define workflows that can be reused:

```yaml
on:
  workflow_call:
    inputs:
      environment:
        required: true
        type: string
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying to ${{ inputs.environment }}"
```

## Debugging & Monitoring

Enable debugging:

```yaml
steps:
  - name: Enable Debugging
    run: env | sort
```

View logs in **Actions > Workflow Runs** on GitHub.