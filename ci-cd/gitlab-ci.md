# GitLab CI/CD CheatSheet

A comprehensive guide covering essential GitLab CI/CD commands and configurations for continuous integration and deployment.

## Table of Contents

- [Introduction](#introduction)
- [Setting Up GitLab CI/CD](#setting-up-gitlab-cicd)
- [GitLab CI/CD Configuration File (.gitlab-ci.yml)](#gitlab-cicd-configuration-file-gitlab-ciyml)
- [Jobs & Stages](#jobs--stages)
- [Runners](#runners)
- [Pipeline Triggers](#pipeline-triggers)
- [Artifacts & Caching](#artifacts--caching)
- [Environments & Deployment](#environments--deployment)
- [Variables & Secrets](#variables--secrets)
- [Monitoring & Debugging](#monitoring--debugging)

## Introduction

GitLab CI/CD is a continuous integration and continuous deployment (CI/CD) system integrated into GitLab to automate build, test, and deployment pipelines.

## Setting Up GitLab CI/CD

Enable GitLab CI/CD for a project:

1. Navigate to your GitLab repository.
2. Go to **Settings > CI/CD**.
3. Expand the **Runners** section and register a runner.
4. Add a `.gitlab-ci.yml` file in the repository root.

## GitLab CI/CD Configuration File (.gitlab-ci.yml)

A basic `.gitlab-ci.yml` file:

```yaml
stages:
  - build
  - test
  - deploy

build:
  stage: build
  script:
    - echo "Building the application"

test:
  stage: test
  script:
    - echo "Running tests"

deploy:
  stage: deploy
  script:
    - echo "Deploying application"
```

## Jobs & Stages

Define job stages:

```yaml
stages:
  - compile
  - test
  - release
```

Define a job:

```yaml
compile:
  stage: compile
  script:
    - echo "Compiling the code"
```

## Runners

Register a GitLab runner:

```bash
sudo gitlab-runner register --url https://gitlab.com/ --registration-token <TOKEN>
```

List all registered runners:

```bash
gitlab-runner list
```

## Pipeline Triggers

Trigger a pipeline manually:

```bash
curl --request POST --form "token=<TOKEN>" --form ref=main https://gitlab.com/api/v4/projects/<PROJECT_ID>/trigger/pipeline
```

Schedule pipeline execution:

```yaml
schedule:
  rules:
    - if: "$CI_COMMIT_BRANCH == 'main'"
      when: always
```

## Artifacts & Caching

Save artifacts between jobs:

```yaml
artifacts:
  paths:
    - build/
```

Enable caching:

```yaml
cache:
  paths:
    - node_modules/
```

## Environments & Deployment

Define deployment environments:

```yaml
environment:
  name: production
  url: https://example.com
```

Deploy using a job:

```yaml
deploy:
  script:
    - echo "Deploying to production"
  environment:
    name: production
```

## Variables & Secrets

Define environment variables:

```yaml
variables:
  DATABASE_URL: "mysql://user:password@host/db"
```

Access secret variables:

```yaml
script:
  - echo "$SECRET_KEY"
```

## Monitoring & Debugging

View job logs:

```yaml
script:
  - cat /var/log/gitlab-runner.log
```

Enable debug mode:

```bash
gitlab-runner --debug run
```

Restart a GitLab runner:

```bash
sudo gitlab-runner restart
```