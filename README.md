# Archipelago API Docs

This repo hosts the API documentation for api.archipelago.com.

All the documentation is written in Markdown and compiled with [Jekyll](https://jekyllrb.com/).
The content lives in the `docs` folder and uses the [Just the Docs](https://just-the-docs.github.io/just-the-docs/) Jekyll template.

# Deployment

The site is hosted using GitHub pages. Commits to the `main` branch automatically publish to the live site.

# Code Setup

## Prerequisites

1. [Install Ruby](https://www.ruby-lang.org/en/documentation/installation/)
1. [Install Bundler](https://bundler.io/)

## Local Development

1. Checkout the repo
1. Navigate to the `docs` directory, this is the root of the Jekyll site
1. Run `bundle install` to install local development dependencies
1. Run `bundle exec jekyll serve` to run the site locally
1. Open a browser and load `http://localhost:4000` to view the site
