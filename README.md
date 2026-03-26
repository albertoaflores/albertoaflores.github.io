# Alberto's Blog

This blog is built with [Hugo](https://gohugo.io/) using the [Hugo Blog Awesome](https://github.com/hugo-sid/hugo-blog-awesome) theme. It can be found at:

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

- [Hugo Blog Awesome](https://github.com/hugo-sid/hugo-blog-awesome) theme with dark/light mode
- [Giscus](https://giscus.app/) for comments (GitHub Discussions-based)
- [Pagefind](https://pagefind.app/) for client-side search
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