# Personal Website

Academic personal website of [Minhuan Li](https://minhuanli.github.io), built with [al-folio](https://github.com/alshedivat/al-folio).

## Local Development

Requires Ruby 3.3. On macOS with Homebrew:

```sh
brew install ruby@3.3
```

Install dependencies:

```sh
PATH="/opt/homebrew/opt/ruby@3.3/bin:/opt/homebrew/opt/ruby@3.3/lib/ruby/gems/3.3.0/bin:$PATH" bundle install
```

Start the server:

```sh
PATH="/opt/homebrew/opt/ruby@3.3/bin:/opt/homebrew/opt/ruby@3.3/lib/ruby/gems/3.3.0/bin:$PATH" bundle exec jekyll serve --livereload --port 4000
```

The site will be available at `http://127.0.0.1:4000`.

## Deployment

Pushing to `master` triggers the GitHub Actions workflow (`.github/workflows/deploy.yml`), which builds the site and deploys it to the `gh-pages` branch. GitHub Pages is configured to serve from `gh-pages`.
