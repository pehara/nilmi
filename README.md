# Deploying nilmi.net on GitHub Pages

This folder is your whole site, ready to push as-is:
- `index.html` — the site
- `assets/`, `fonts/`, `_ds/`, `support.js`, `image-slot.js` — everything the site loads
- `CNAME` — tells GitHub Pages to serve this repo at nilmi.net

Don't rename or move any of these — `index.html` references them by relative path.

## 1. Push to GitHub
1. Create a new **public** repo on GitHub (e.g. `nilmi-portfolio`). Leave it empty (no README/license).
2. On your computer, inside this unzipped folder, run:
   ```
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```

## 2. Turn on GitHub Pages
1. In the repo, go to **Settings → Pages**.
2. Under "Build and deployment", set **Source** to `Deploy from a branch`.
3. Set **Branch** to `main` and folder to `/ (root)`. Save.
4. GitHub gives you a URL like `https://<your-username>.github.io/<repo-name>/` — wait a minute and confirm it loads.

## 3. Point nilmi.net at GitHub Pages
nilmi.net's DNS currently points at Wix (or wherever it's hosted now). You need to move it:

1. **In GitHub**: Settings → Pages → "Custom domain" → enter `nilmi.net` → Save.
2. **At your domain registrar** (wherever nilmi.net is managed — check Wix or your registrar account):
   - Remove the DNS records currently pointing to Wix.
   - Add these instead:
     - Four **A** records for `@` pointing to GitHub's IPs:
       - 185.199.108.153
       - 185.199.109.153
       - 185.199.110.153
       - 185.199.111.153
     - One **CNAME** record for `www` pointing to `<your-username>.github.io`
3. Back in GitHub Pages settings, once DNS has propagated (can take a few hours), check **Enforce HTTPS**.

## One thing to check after deploying
The hero portrait photo (and any other photo you dropped into a placeholder in the editor) is stored in the editor's own browser storage, not in these files. Open the live site once it's up and re-drop any photos that show as empty placeholders.

## Notes
- If you update the site later, come back here, ask for a fresh export, replace these files, commit, and push again.
- Wix will stop serving nilmi.net once you switch the DNS records in step 3 — there's no way to run both at once.
