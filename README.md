# Alberto's Blog

This blog is built with [Hugo](https://gohugo.io/) using the [LoveIt](https://hugoloveit.com/) theme. It can be found at:

https://albertoaflores.github.io

## Running Locally

Make sure you have Hugo installed (extended version):

```bash
brew install hugo
```

Run the development server:

```bash
hugo server
```

To include draft posts:

```bash
hugo server -D
```

## Features

- [LoveIt](https://hugoloveit.com/) theme with dark/light/auto mode
- [Giscus](https://giscus.app/) for comments (GitHub Discussions-based)
- [Pagefind](https://pagefind.app/) for client-side search
- KaTeX math rendering
- Google Analytics

## Pagefind Search

Pagefind indexes the built site. To test search locally:

```bash
hugo
npx pagefind --site public
hugo server
```

In production, Pagefind indexing runs automatically via the GitHub Actions workflow.

## Deployment

The site is deployed to GitHub Pages via GitHub Actions. Pushing to `master` triggers a build and deploy automatically.