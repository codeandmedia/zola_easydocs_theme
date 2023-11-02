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

## Requirements

Before using the theme, you need to install [Zola](https://www.getzola.org/documentation/getting-started/installation/) ≥ 0.17.2.

## Quick Start

```bash
git clone git@github.com:semanticdata/mabuya.git
cd mabuya
zola serve
# open http://127.0.0.1:1111/ in the browser
```

## Customization

You can changed the configuration, templates and content yourself. Refer to the `config.toml`, and templates files for an idea.

In most cases you only need to modify the contents of `config.toml` to
customize the appearance of your blog.

### Custom CSS Styles

Adding custom CSS is as easy as adding your styles to `sass/_custom.scss. This is made possible because SCSS files are backwards compatible with CSS3. This means you can type normal CSS code into a SCSS file and it will be valid.

## Provided configurations options

These options can be configured in the `extra` section of the [config.toml](config.toml).
If any are not present it has the same behaviour as the default which is shown in the starter [config.toml](config.toml).

- **easydocs_logo_always_clickable** controls if the logo is always clickable. By default the logo is only clickable if you are not on the home page. If this is enabled it will make the logo clickable when you are on the home page as well. Thus on the home page it will basically just refresh the page as it will take you to the same page.
- **easydocs_uglyurls** provides support for offline sites that do not use a webserver. If set to true links in the nav are generated with the full path indcluding `index.html`. This functionality was  insired by [Abridge theme](https://www.getzola.org/themes/abridge/). Note that for this to work it also requries the base URL to be set to the local folder where the site will be stored eg. `base_url = file:///home/user/mysite/public/`. Therefore this is not portable and only works with a specific local folder, but does not require a webserver to navigate the site.
- **easydocs_heading_threshold** controls minimum number of headings needed on a page before the headings show in the navigation on the left. Defaults to 5. Can be used for example to always show headings on each page by setting it to 1.

## Useful Commands

A short list of commands that will help you develop your own version of the theme.

| Command                    | Description                |
| -------------------------- | -------------------------- |
| `zola build`               | Build only                 |
| `zola serve`               | Build and Serve            |

## Reporting Issues

We use GitHub Issues as the official bug tracker for **Mabuya**. Please
search [existing issues](https://github.com/semanticdata/mabuya/issues). It’s
possible someone has already reported the same problem.

If your problem or idea is not addressed yet, [open a new issue](https://github.com/semanticdata/mabuya/issues/new).

## Contributing

We'd love your help! Please see [CONTRIBUTING.md](./CONTRIBUTING.md) to learn
about the kinds of contributions we're looking for.

## Acknowledgements and Attributions

- The core of the theme is based on [Easy Docs](https://github.com/codeandmedia/zola_easydocs_theme).
- Icons used in the site come from [UXWing](https://uxwing.com/license/).
- Code for the copy-code-button by [Aaron Luna](https://aaronluna.dev/blog/add-copy-button-to-code-blocks-hugo-chroma/).

## License

Source code in this repository is available under the [MIT](LICENSE) license. You are free to use this code however you see fit. That said, some acknowledgement would be well received.
