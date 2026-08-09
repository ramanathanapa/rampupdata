# Your Data Engineering Site

A minimal Hugo site with no theme dependency and no build tooling beyond Hugo itself.
100% portable — the entire site is plain Markdown + Go templates + one CSS file.

## Local setup

1. Install Hugo (extended version): https://gohugo.io/installation/
2. Clone this repo
3. Run the dev server:
   ```
   hugo server -D
   ```
4. Open http://localhost:1313

## Writing a new post

```
hugo new posts/my-post-title.md
```

Edit the file in `content/posts/`, set `date:` and write in Markdown below the `---` front matter.
Drafts (`draft: true` in front matter) won't be published until you remove that line.

## Publishing

1. Update `baseURL` in `hugo.yaml` to your real domain, e.g. `https://yourdomain.com/`
2. Push to a GitHub repo on the `main` branch
3. In repo Settings → Pages, set Source to "GitHub Actions"
4. The included workflow (`.github/workflows/deploy.yml`) builds and deploys automatically on every push
5. In your domain registrar, point DNS to GitHub Pages (CNAME to `<username>.github.io`, or A records for an apex domain — GitHub's docs cover both)

## Moving off GitHub Pages later

Since Hugo just outputs static files to `public/`, you can host that folder anywhere —
Cloudflare Pages, Netlify, your own VPS with Nginx, S3, etc. Only the deploy workflow changes;
your content and templates stay exactly the same.

## Customizing

- Styling: `static/css/style.css`
- Page templates: `layouts/_default/` and `layouts/index.html`
- Site title/description: `hugo.yaml`
