# Alberto's Blog
This blog is based on Jekyll. This can be found at:

https://albertoaflores.github.io

## Running locally
Make sure you have ruby version 2.7.1. For simplicity, see the `.ruby-version` file if using

Running the following:
```bash
bundle exec jekyll serve
```
Runs Jekyll locally with our server running on port localhost:4000

### Updating
Since we are (ideally) using bundler, we can run the following:

```bash
bundle update
```
This should update the `Gemfile.lock` which contains all dependency versions.