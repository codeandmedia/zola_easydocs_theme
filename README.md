<p align="right">
  <img src="https://img.shields.io/github/languages/code-size/semanticdata/zola-docs" />
  <img src="https://img.shields.io/github/repo-size/semanticdata/zola-docs" />
  <img src="https://img.shields.io/github/commit-activity/t/semanticdata/zola-docs" />
  <img src="https://img.shields.io/github/last-commit/semanticdata/zola-docs" />
  <img src="https://img.shields.io/website/https/semanticdata.github.io/zola-docs.svg" />
</p>

# Zola Docs

An easy way to document your projects.

## Step-by-Step Guide

1. Fork the repo and replace demo-content inside content folder with yours. But take a look to _index.md files. It contains `title` and when you want to have anchor right of your headers add `insert_anchor_links = "right"` to each index. `theme.toml`, screenshot and readme may be deleted too.
2. Inside `config.toml` change URL and title on your own. In extra section you can specify path to your GitHub API for version below the logo on nav, favicon and logo itself. Or just remove the lines if you don't need it. Also, you can configure or turn on some additional settings related to Zola. [Specification is here](https://www.getzola.org/documentation/getting-started/configuration/).
3. In sass/_variables.scss you may change font, color or background if you want.
4. Almost done. Now, you should decide how you want to build and where will be hosted your website. You can build it locally and upload to somewhere. Or build in GitHub Actions and host on GitHub Pages / Netlify / CloudFlare Pages / AnyS3CloudStorage. [Howto for GitHub Pages](https://www.getzola.org/documentation/deployment/github-pages/). [My example](https://github.com/o365hq/o365hq.com/blob/main/.github/workflows/main.yml) of GitHub workflow with 2-steps build (the first checks for links and spelling errors, the second uploads to Azure). [Dockerfile](https://github.com/codeandmedia/zola_docsascode_theme/blob/master/Dockerfile) to make Docker image.

## GitHub Pages via GitHub Actions

This example only builds on pull request or manual activation. It serves as a test before production deployment.

```yml
name: Zola - Build only

on:
  # push:
  #   branches:
  #     - main 
  pull_request:
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build-only:
    runs-on: ubuntu-latest
    # if: github.ref != 'refs/heads/main'
    steps:
      - name: Checkout main
        uses: actions/checkout@v3
      - name: Install Zola
        uses: taiki-e/install-action@zola
      - name: Build Zola
        run: zola build
        env:
          BUILD_ONLY: true
          BUILD_FLAGS: --drafts
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

This next example both builds, and deploys the build to GitHub Pages. This is done without the need to involve Docker, which usually slows down the process.

```yml
name: Zola on GitHub Pages - Taiki

on:
  # push:
  #   branches:
  #     - main 
  # pull_request:
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
          
  build:
    runs-on: ubuntu-latest
    # if: github.ref != 'refs/heads/main'
    steps:
      - name: Checkout main
        uses: actions/checkout@v3
      - name: Install Zola
        uses: taiki-e/install-action@zola
      - name: Build Zola
        run: zola build
        env:
          # BUILD_ONLY: true
          # BUILD_FLAGS: --drafts
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

## Acknowledgements and Attributions

* Icons: [UXWing](https://uxwing.com/license/).
* Core: [Easy Docs](https://github.com/codeandmedia/zola_easydocs_theme) theme for [Zola](https://www.getzola.org).
* Copy-code-button: [Aaron Luna](https://aaronluna.dev/blog/add-copy-button-to-code-blocks-hugo-chroma/).

## License

Source code is available under [MIT](LICENSE).
