# Deploy this site on GitHub Pages

## What you need to provide / decide

1. **GitHub account** — username you will push from.
2. **Repository name**
   - **User site (recommended for a primary portfolio):** create a public repo named `YOUR_USERNAME.github.io`. The live URL will be `https://YOUR_USERNAME.github.io/` with **no path prefix**.
   - **Project site:** any repo name (e.g. `portfolio`). The URL will be `https://YOUR_USERNAME.github.io/REPO_NAME/` (all asset paths in this project are relative, so this still works).
3. **Branch name** — this workflow deploys on push to **`main`**. If your default branch is `master`, either rename it to `main` in GitHub repo settings or change `branches: [main]` in `.github/workflows/pages.yml` to match.
4. **Optional — custom domain** (e.g. `alirezasepehri.com`): you will add DNS records at your registrar and a `CNAME` file in the repo (see below).

## One-time GitHub settings (after the repo exists)

1. On GitHub: **Settings → Pages**.
2. Under **Build and deployment**:
   - **Source:** **GitHub Actions** (not “Deploy from a branch”).
3. Push this repo to GitHub; the **Deploy GitHub Pages** workflow should run and publish the site.
4. After the first successful run, Pages shows the public URL (often under **Settings → Pages** or in the workflow summary).

## Push this folder to a new GitHub repo

From your machine (replace placeholders):

```bash
cd "/path/to/myWebsite"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

If the remote repo was created with a README and you need to reconcile history:

```bash
git pull origin main --rebase
git push -u origin main
```

## Custom domain (optional)

1. In the repo root, add a file named **`CNAME`** whose **only line** is your hostname, e.g. `alirezasepehri.com` (no `https://`).
2. At your DNS provider:
   - **Apex domain:** add **A** records to GitHub’s IPs (see [GitHub docs: configuring a custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)).
   - Or use a **CNAME** from `www` → `YOUR_USERNAME.github.io`.
3. In the repo: **Settings → Pages → Custom domain** — enter the domain and enable **Enforce HTTPS** after DNS validates.

Also update **`og:url`**, **`twitter:image` / `og:image`**, and **`canonical`** in `index.html` if they still point at a placeholder domain, so link previews match your real URL.

## Checklist before you call it done

- [ ] `images/` folder committed (headshot, favicon, product screenshots, etc.).
- [ ] `images/og-image.png` exists (1200×630) for LinkedIn/Slack previews.
- [ ] Open **Settings → Pages** and confirm **Source** is **GitHub Actions**.
- [ ] Visit the published URL on your phone (layout, fonts, hash links like `#experience`).

## Local preview

```bash
npm run preview
```

Then open `http://localhost:5173`.
