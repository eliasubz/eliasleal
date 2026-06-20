# Flow MRI Notes

A minimal Jekyll blog for 4D flow MRI paper recreations.

Run locally:

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`.

## Deploy on GitHub Pages

1. Create a GitHub repo. For a personal root site, name it `<username>.github.io`.
2. Push this repo to GitHub.
3. In GitHub, go to `Settings -> Pages`.
4. Set `Build and deployment -> Source` to `GitHub Actions`.
5. Push to `main`; the included workflow deploys the site.
