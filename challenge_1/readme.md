# Challenge 1 - Get to know Github Actions

## Assumed knowledge

* Git
* Basic linux
* Baiscs on containers

## What is Github Actions

GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline.


GitHub Actions goes beyond just DevOps and lets you run workflows when other events happen in your repository. For example, you can run a workflow to automatically add the appropriate labels whenever someone creates a new issue in your repository. [GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)


```yaml
name: Hello world

on:
    push:
    workflow_dispatch:

jobs:
  my_first_job:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Hello, world!"

```

## Running github actions

To run a github action you need to create a `.github/workflows` directory in your repository and add a `.yml` file with the workflow definition. Then you can push the changes to your repository and the action will work.


Running locally is a bit more complicated, you need to install the `act` tool. The `act` tool is a command line tool that allows you to run GitHub Actions locally. It uses the Docker container API to run workflows in containers. [Act](https://github.com/nektos/act)

*See all the jobs*
```sh
act --workflows examples --list
```

*Run a specific job*
```sh
act --workflows examples --job my_first_job
```


## Challenge 🔈

Get github actions to work locally and run the `my_first_job` job.

> Tip: If you don't get `act` to work, you can add the workflow to a github repository and see the results there.

Some useful links:
* [Docker desktop](https://www.docker.com/products/docker-desktop/) - This is a easy way to start using docker.
* [Podman desktop](https://podman-desktop.io/) - A better and free alternative to docker desktop (in my opinion).
* [Act](https://github.com/nektos/act) - The tool to run github actions locally.


## Github Actions possibilities

> "It's just a computer"

*Simple discord bot*

```yaml
name: Discord bot

on:
  cron:
    - cron: '0 7 * * *'  # Runs at 7am UTC every day

jobs:
    wake_up:
        runs-on: ubuntu-latest
        steps:
            - name: Good morning message
              run: |
                curl -X POST -H 'Content-type: application/json' --data '{"content":"Good morning!☀️"}' ${{ secrets.DISCORD_WEBHOOK }}

```

*Simple deployment of static site*

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4

    - name: Deploy
      uses: peaceiris/actions-gh-pages@v4
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./website
```

## Challenge 🔈

Create your own gitub action!

Ideas:
* Deploy a static site to github pages.
* Prints out a message each time a pull request is opened containing the PR title
* Run "smoke tests" on your application when a new release is created

Some useful links:
* [GitHub Actions Marketplace](https://github.com/marketplace?type=actions) - Find cool actions to use in your workflows.
