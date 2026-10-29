# Host this on GitHub Pages

This app is a static site. `npm run build` makes a `dist` folder. GitHub Pages can serve that folder for free. You push the code yourself. GitHub builds and publishes it.

Do not commit `node_modules` or `dist`. Both are already in `.gitignore`.

## Already done in this project

You do not need a `.env` file. `import.meta.env.BASE_URL` is built into Vite.

These files are already set:

- `vite.config.js` uses `/facebook-clone/` only when GitHub builds the site.
- `src/components/PreviewCard.jsx` loads the map from that base path.
- `.github/workflows/deploy.yml` builds and publishes the site.

Name the GitHub repository exactly `facebook-clone`. The live site will be:

`https://YOUR-USERNAME.github.io/facebook-clone/`

Local `npm run dev` stays at `http://127.0.0.1:5173/`.

## Push to GitHub

1. Create a new **public** repository on GitHub. Leave it empty. Do not add a README, license, or `.gitignore` there.
2. In this project folder:

```bash
git init
git add .
git commit -m "Add Marketplace vehicle listing page"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/facebook-clone.git
git push -u origin main
```

3. On GitHub, open the repository.
4. Go to **Settings → Pages**.
5. Under **Build and deployment**, set **Source** to **GitHub Actions**.
6. Open the **Actions** tab. The "Deploy to GitHub Pages" workflow should run. Wait until it is green.
7. Go back to **Settings → Pages**. The site URL is shown at the top.

The first visit can take a minute after the action finishes.

Each later `git push` to `main` publishes a new version.

## If the site is blank

- `base` in `vite.config.js` does not match the repository name.
- Pages source is still "Deploy from a branch" instead of **GitHub Actions**.
- The Actions run failed. Open the failed job and read the red step. `npm ci` fails when `package-lock.json` was not committed.

## Other free hosts

GitHub Pages is the right choice if you want the site on GitHub and nowhere else.

**Cloudflare Pages** is the better free host if you want a faster site or a cleaner address (`something.pages.dev` or your own domain). You still push only to GitHub. Cloudflare reads that repo and builds it. You do not upload a server, and you do not use Vercel or Railway.

Cloudflare Pages settings:

- Build command: `npm run build`
- Build output directory: `dist`
- Leave `base` as `"/"` (the default). Do not set `/YOUR-REPO-NAME/`.
- Keep the map image as `/redding-map.png`, or the `BASE_URL` version also works when `base` is `"/"`.

You do not need the GitHub Actions file for Cloudflare. Skip `.github/workflows/deploy.yml` if you use Cloudflare only.

Netlify can do the same job. Cloudflare Pages is the one to pick if you leave GitHub Pages.
