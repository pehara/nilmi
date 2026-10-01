# nilmi.net: test, publish and update guide

This folder is the complete website. There is no build step: what's here is exactly what gets published.

> **It comes in two zips.** `nilmi-site-part1.zip` has the site, and `nilmi-site-part2-art.zip` has the Digital Art and
> Gel-X gallery images. Unzip **both into the same place**; they share the `nilmi-site/` folder and merge together.
> Without part 2, the art and nails pop-ups will be empty.

```
nilmi-site/
├── index.html            the whole page (layout, styles, animations)
├── content/
│   ├── projects.json     project cards
│   └── hobbies.json      books, games, travel, food, art, nails, song list
├── assets/
│   ├── decor/            pond artwork (lily pads, flowers, fish, sand, chest…)
│   ├── art/              Digital Art + Gel-X gallery images
│   ├── projects/         project screenshots and clips
│   ├── fonts/            your fonts
│   ├── hobbies/, uploads/  where new pictures go
│   └── favicon.svg, favicon-32.png, apple-touch-icon.png
├── .pages.yml            Pages CMS setup (hidden file, keep it)
├── .nojekyll             tells GitHub Pages to publish files as-is (hidden file, keep it)
├── .vscode/              recommends the Live Server extension
├── README.md             short reference
└── SETUP-GUIDE.md        this guide
```

> **Hidden files:** `.pages.yml`, `.nojekyll` and `.vscode` start with a dot, so your file manager may hide them.
> On Linux press **Ctrl+H** in the file manager to show them. VS Code always shows them.

---

## Part 1: Test it on your computer with VS Code

The page loads its content from the `content/` files, and browsers block that when you double-click
`index.html` (you'd see "Projects couldn't load here"). So always preview through a small local web server.
Option A is the easiest.

### Option A: Live Server extension (recommended)
1. Unzip both zips into the same place, e.g. `~/Projects/`, so you end up with one `~/Projects/nilmi-site` folder.
2. Open VS Code → **File → Open Folder…** → choose the `nilmi-site` folder.
3. VS Code may pop up "Do you want to install the recommended extensions?" Click **Install**.
   If not: open the Extensions panel (**Ctrl+Shift+X**), search **Live Server** (by Ritwick Dey) and click **Install**.
4. Click **Go Live** in the blue status bar at the bottom right (or right-click `index.html` → **Open with Live Server**).
5. Your browser opens at `http://127.0.0.1:5500/index.html`. Every time you save a file, the page reloads.
6. To stop it, click **Port: 5500** in the status bar.

### Option B: VS Code's terminal (no extension)
1. Open the folder in VS Code, then **Terminal → New Terminal** (**Ctrl+`**).
2. Run:
   ```bash
   python3 -m http.server 8000
   ```
3. Open `http://localhost:8000` in your browser. Press **Ctrl+C** in the terminal to stop.

### What to check
Use this as a checklist before publishing.

- [ ] **Opening animation:** petals fall, then the page appears at the top.
      It plays once per browser tab; open a new tab to see it again.
- [ ] **Hero:** lily pads float, lotus petals sway and react to your cursor, buds bob, bubbles pop and come back.
- [ ] **Click the water:** ripples spread and nearby pads rock.
- [ ] **About Me:** text, the portrait, and "based in / currently working / languages".
- [ ] **Outside of Work:** open every "See More…" pop-up.
  - [ ] Digital Art: both the 2D and 3D tabs.
  - [ ] Gel-X Nails.
  - [ ] Reading: the wooden bookshelf. It's empty until you add books.
  - [ ] Gaming: game covers load from Steam.
  - [ ] Music: the song list and the record player. Spotify's player loads on localhost and on the live site.
  - [ ] Travel and Food: show "coming soon" until you add photos.
- [ ] **Projects:** all 11 cards appear, the filter buttons work, clips play, and the link buttons open.
- [ ] **Skills:** fish drift, their eyes follow the cursor, and clicking the water sprinkles food they come to eat.
      Sunbeams and floating specks show here.
- [ ] **Bottom:** the kelp bends when you sweep the cursor through it, and the chest and sand have their grain.
- [ ] **Phone layout:** press **F12** in Chrome/Vivaldi → click the phone/tablet icon (**Ctrl+Shift+M**) →
      pick e.g. "iPhone 12 Pro". The page switches to a stacked phone layout with the decorations simplified.
- [ ] **Contact form:** best tested on the live site (see Part 3). Sending from localhost works too,
      but the first message triggers FormSubmit's activation email.

> **Tip:** if a change doesn't show up, do a hard refresh with **Ctrl+Shift+R**.

---

## Part 2: Publish with GitHub Pages

nilmi.net is already set up as a GitHub Pages site with a `CNAME` file holding your domain.
You'll replace the old site's files with these and keep the `CNAME`.

### Step 1: Get your repo onto your computer
If you don't have it locally yet, in VS Code:
1. Press **Ctrl+Shift+P**, type **Git: Clone** and press Enter.
2. Choose **Clone from GitHub**, sign in if asked, and pick your nilmi.net repo. It's probably named
   `pehara.github.io` or similar; it's the one with the `CNAME` file.
3. Pick a folder to clone into, then click **Open** when VS Code asks.

Or, in a terminal (replace the URL with your repo's):
```bash
git clone https://github.com/pehara/YOUR-REPO-NAME.git
cd YOUR-REPO-NAME
code .
```

### Step 2: Back up anything you still need from the old site
Before deleting, check the repo for anything the new site still links to.
- **Important:** the *Lethal Love* card's "Download build" button points to
  `https://www.nilmi.net/_files/archives/4d702e_86733a831a574eb7b18b48a57ff02649.zip`.
  - If your repo has that `_files/` folder, **keep it**.
  - If that link came from an older host (e.g. Wix), it will stop working once the domain points here.
    In that case, upload the build to itch.io or a GitHub Release, then paste the new link into
    `content/projects.json` (`"link_url"` for Lethal Love).
- Keep anything else you want, such as your résumé PDF.

### Step 3: Replace the old files with the new site
In the cloned repo folder:
1. Delete the old site files, **but keep**:
   - `CNAME` (your domain, required!)
   - the hidden `.git` folder (never delete this)
   - anything from Step 2 you decided to keep
2. Copy **everything** from inside `nilmi-site/` into the repo folder, including the hidden
   `.pages.yml`, `.nojekyll` and `.vscode`.
   The repo root should now hold `index.html`, `CNAME`, `content/`, `assets/` and so on, not a `nilmi-site` subfolder.

Quick check in a terminal from the repo folder:
```bash
ls -a
# you should see: .git  .nojekyll  .pages.yml  .vscode  CNAME  README.md  SETUP-GUIDE.md  assets  content  index.html
```

### Step 4: Commit and push
**In VS Code:**
1. Open **Source Control** (**Ctrl+Shift+G**). You'll see the list of changed files.
2. Type a message such as `New pond redesign` in the box at the top.
3. Click **Commit**. If it asks "stage all changes?", click **Yes**.
4. Click **Sync Changes** (or **Push**).

**Or in a terminal:**
```bash
git add -A
git commit -m "New pond redesign"
git push
```

The upload is around 40 MB, so the first push can take a minute.

### Step 5: Check the Pages settings (one time)
On github.com, open your repo → **Settings → Pages**.
- **Source:** *Deploy from a branch*.
- **Branch:** `main` (or whatever your default branch is), folder `/ (root)` → **Save**.
- **Custom domain:** `www.nilmi.net` or `nilmi.net` (it should already be filled in from `CNAME`).
- Tick **Enforce HTTPS** if it isn't already.

### Step 6: Wait, then look
- Open the repo's **Actions** tab to watch the "pages build and deployment" job. It usually takes 1–3 minutes.
- When it's green, visit **https://nilmi.net** and do a hard refresh (**Ctrl+Shift+R**).
- Run through the Part 1 checklist once more on the live site, and on your phone.

---

## Part 3: One-time setup after the site is live

**Nothing in the code needs changing after you push.** Every pop-up (Digital Art 2D/3D, Gel-X, Reading, Gaming,
Travel, Food Homemade/Favorites, Music) and the Projects section read from `content/*.json`, so you add things
through Pages CMS. Empty sections show "coming soon" until you do. The only steps left are these three
sign-ups, and only the GoatCounter one could ever mean touching code (if the code `nilmi` is taken).

### Contact form (FormSubmit)
1. On **nilmi.net**, send yourself a test message through the form.
2. FormSubmit emails **pehara002@gmail.com** asking you to activate the form. Click the **Activate** button in that email.
   Check spam if it's not there.
3. Send another test. It should now arrive as a normal email, and replying goes straight to the sender.

### Visitor stats (GoatCounter)
1. Sign up at **https://www.goatcounter.com/signup**.
2. For the code, enter **nilmi** (your dashboard becomes `nilmi.goatcounter.com`).
   If that's taken, pick another code and change `CODE='nilmi'` near the top of `index.html` to match.
3. Visit nilmi.net. Within a minute the visit shows in your dashboard.
   Local previews are never counted. Opening each hobby pop-up is also counted, as an event.

### Edit content without code (Pages CMS)
1. Go to **https://app.pagescms.org** → **Sign in with GitHub** → allow access to your nilmi.net repo.
2. Open the repo. You'll see **Projects** and **Outside of work** in the sidebar.
3. Add a book, game, trip or dish, or edit a project, upload a picture, then click **Save**.
   Saving commits to GitHub, and the live site updates in 1–3 minutes.

---

## Part 4: Updating the site later

**Content (most changes):** use Pages CMS, as above.
- Book and game covers look best at 2:3 (e.g. 600×900).
- Games without a picture show a styled title card. To add or change a cover, open the game in Pages CMS and upload one in **Cover**.
- For a Steam game, just fill in the **Steam app ID** (the number in its store link, e.g.
  store.steampowered.com/app/**413150**/Stardew_Valley) and leave the cover empty.
- Keep photos under about 500 KB (export as WebP or JPG).
- Add as many projects as you like: on computers they're shown 12 at a time with **‹ Previous / More ›** buttons (phones show them all).
- The music song list doesn't sync with Spotify by itself. Add songs to it when you change the playlist.

**If you edited in Pages CMS and also want to work in VS Code**, pull the latest changes first so you
don't overwrite them: **Source Control → … → Pull** (or `git pull`).

**Anything else** (wording in `index.html`, styles, layout): edit in VS Code, preview with Live Server,
then commit and push as in Part 2, Step 4.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| "Projects couldn't load here" | You opened `index.html` directly. Use Live Server or `python3 -m http.server`. |
| Live site shows the old design | Wait for the Actions job to finish, then hard refresh with **Ctrl+Shift+R**. |
| Site shows a 404 | Make sure `index.html` is in the repo **root**, not inside a `nilmi-site/` folder. |
| Domain stopped working | The `CNAME` file was deleted. Add it back with the single line `www.nilmi.net` (or whatever it held before), or re-enter the domain in Settings → Pages. |
| Pages CMS doesn't show Projects / Outside of work | `.pages.yml` didn't get copied (it's hidden). Copy it into the repo root and push. |
| Spotify player or game covers missing | Usually a browser privacy blocker. In Vivaldi, click the shield icon and allow nilmi.net. The song list always shows regardless. |
| Contact form says "Couldn't send just now" | The form hasn't been activated yet (Part 3), or FormSubmit is briefly down. Visitors still get an "Email me instead" link. |
| Animations feel slow on an old computer | They pause automatically when off screen, and are switched off for anyone with "reduce motion" turned on in their system settings. |
