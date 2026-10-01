# nilmi.net — pond redesign

Static site built from the "Pehara Portfolio" Figma file. No build step.

**New here? Read `SETUP-GUIDE.md`**: how to preview in VS Code, publish on GitHub Pages, and finish setup.

## Deploy (GitHub Pages)
Copy everything in this folder into the root of the existing nilmi.net repo — including the hidden
`.pages.yml` file — and keep the repo's existing `CNAME` file. Commit and push.

## Adding content without touching code (Pages CMS)
All projects and hobby content live in two files:
- `content/projects.json` — the project cards
- `content/hobbies.json` — books, games, travel, food, art, nails and the music song list

To edit them with simple forms:
1. Go to https://app.pagescms.org and sign in with GitHub.
2. Pick the nilmi.net repo. It reads `.pages.yml` and shows **Projects** and **Outside of work**.
3. Add or edit entries, upload pictures (they're saved to `assets/uploads/`), then **Save**.
   Saving commits to GitHub, and the live site updates a minute or two later.

Tips
- Book and game covers look best at 2:3 (e.g. 600×900). Keep photos under ~500 KB; export as WebP or JPG.
- Games on Steam: just fill in the Steam app ID (the number in the store link) and leave the cover empty.
- Projects: add as many as you like; computers show 12 at a time with Previous / More buttons.
- The music song list doesn't sync with Spotify by itself. Add songs to it when you change the playlist.

## Previewing on your computer
The page loads its content files, so opening `index.html` by double-clicking won't show projects.
Instead, in this folder run `python3 -m http.server` and open http://localhost:8000.

## Contact form
Messages are sent through FormSubmit (formsubmit.co) to pehara002@gmail.com.
The **first** message triggers a one-time "Activate form" email from FormSubmit — click the link in it.
After that every message arrives as a normal email. To send yourself a test, use the form on the live site.

## Visitor stats (GoatCounter)
1. Sign up free at https://www.goatcounter.com with the code **nilmi** (so the dashboard is nilmi.goatcounter.com).
   If you choose a different code, change `CODE='nilmi'` near the top of `index.html`.
2. That's it. Visits are only counted on nilmi.net (not local previews), no cookies, no consent banner needed.
   Opening each hobby pop-up is also counted, as an event.

## Folders
- `assets/decor/` – illustrations from Figma, pre-rendered to WebP at 1× and 2× (`@2x`) so the textured
  grain looks exactly like the design without the browser having to recompute it while scrolling
- `assets/art/2d|3d|nails/` – gallery images (`N.webp` full size, `N-t.webp` thumbnail)
- `assets/projects/` – project clips (MP4) and stills
- `assets/uploads/` – images you add through Pages CMS
- `assets/fonts/` – Desevon, Semika, Sparky Dream and Ethereal, plus Crimson Text, Playfair Display and Source Serif 4 (SIL OFL)
- `assets/favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` – the lotus tab icon
