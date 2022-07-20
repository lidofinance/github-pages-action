# github-pages-action

Custom action to push static files to specific branch for GitHub pages

Note: You must build static files by himself because it depends on your static-site generator engine.
After that, static files will be an input to github-pages-action

Unlike other public actions, this action is simple and not required access tokens with superfluous rights
(in fact, it doesn't even give you the option to pass it on). 

## Usage

Workflow example:

```yaml
name: Build static files and deploy to gh pages

on:
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          fetch-depth: 0
      
      - name: Build static files to 'build' folder
        ...
      
      - name: Publish
        uses: lidofinance/github-pages-action@v1
        with:
          branch: gh-pages
          folder: build
```

### Possible action inputs

```yaml
inputs:
  branch:
    description: 'This is the branch you wish to deploy to, for example gh-pages or docs.'
    required: false
    default: gh-pages
  folder:
    description: >
      The folder in your repository that you want to deploy. 
      If you wish to deploy the root directory you can place a . here.'
    required: true
```