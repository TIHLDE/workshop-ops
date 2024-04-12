# Challenge 1 - Get to know Github Actions

## Assumed knowledge

* Git
* Basic linux

## What is Github Actions

GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline.


GitHub Actions goes beyond just DevOps and lets you run workflows when other events happen in your repository. For example, you can run a workflow to automatically add the appropriate labels whenever someone creates a new issue in your repository. [GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)


```yaml
name: Hello world

on:
    push:

jobs:
  my_first_job:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Hello, world!"

```

