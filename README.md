# My Portfolio Website

A hand-built, pond-themed portfolio site for myself, a software engineer and game developer
(B.S. Computer Science & Game Design, UC Santa Cruz).

Scrolling down the page is like sinking through a pond:
- lily pads and lotus flowers float on the surface;
- below that, sunlight filters through the water, past fish and bubbles;
- at the bottom, a treasure chest rests in the sand among the kelp, and it holds the contact form.

**Live site:** https://nilmi.net

---

## Contents
- [What's on the page](#whats-on-the-page)
- [Interactive details](#interactive-details)
- [How it was made](#how-it-was-made)
- [Technical overview](#technical-overview)
- [Project structure](#project-structure)
- [Running it locally](#running-it-locally)
- [Publishing (GitHub Pages)](#publishing-github-pages)
- [Updating content (Pages CMS)](#updating-content-pages-cms)
- [Services used](#services-used)
- [Accessibility & performance](#accessibility--performance)
- [Credits](#credits)

---

## What's on the page

| Section | What it shows |
|---|---|
| **Opening** | A short intro: lotus petals tumble down in 3D, "Hello!" fades in, and the water clears to reveal the site. It plays once per visit; click, press any key, or hit *skip* to jump past it. |
| **Hero** | Name, "Portfolio" title, a one-line introduction and a **Let's connect** button that opens LinkedIn. |
| **About Me** | A short bio and photo, plus where Pehara is based, where they currently work, and the languages they speak. |
| **Outside of Work** | Seven hobby cards, each opening its own pop-up: **Digital Art** (2D/3D tabs), **Gel-X Nails**, **Reading** (a wooden bookshelf with notes on each book), **Gaming** (a game shelf with covers and short descriptions), **Music** (a record player and the Spotify playlist), **Travel** (photos with locations) and **Food** (Homemade / Favorites tabs). |
| **Projects** | Project cards with screenshots or looping gameplay clips, the platform or engine used, tags, and a link to play, download or view the source. Filter buttons switch between Games, Web and Python, and once there are more than 12 projects they're shown 12 at a time. |
| **Skills** | Languages, traits, and engines/tools. |
| **Contact** | A form inside the treasure chest that emails messages straight to Pehara, plus email, GitHub and LinkedIn links. |

---

## Interactive details
The pond reacts to you:

- **Lily pads** drift and rock gently on the water. Clicking the water sends out ripples, and nearby pads bob in response, with farther ones moving later and less.
- **Lotus flowers** sway petal by petal, and each petal springs away from your cursor when you brush past.
- **Buds** bob on the surface and wobble or dip when touched.
- **Bubbles** drift upward, pop now and then (or when you touch them), and reappear elsewhere.
- **Sunbeams** slowly brighten and sway through the water below the surface.
- **Floating specks** drift up through the deep water, with a little depth as you scroll.
- **Fish**:
  - Each one drifts on its own, and its eyes follow your cursor.
  - **Click the water near them to sprinkle food.** They swim over, open their mouths, and eat.
  - Each fish eats 3–8 flakes, then is full for a while.
  - Up to 14 flakes can be in the water at once.
- **Kelp** sways at the bottom and bends away when you sweep the cursor through it.
- **Scroll reveals**: text and cards rise into place as you reach them. Buttons give a small water-drop splash when clicked.
- **Music pop-up**: the record spins up and slows down like a real turntable, picking a song puts its name on the label, and the needle drops while Spotify is playing.

---

## How it was made
1. **Design:** I designed the whole site in **Figma**: layout, colours, type and every illustration, from the lily pads and lotus flowers to the fish, seaweed, sand and chest.
2. **Build:** the design was turned into a plain static website with **Claude** (Anthropic's AI assistant), working from the Figma file:
   - the illustrations were exported from Figma and pre-rendered as images;
   - the layout reproduces the Figma artboard exactly;
   - the animations and interactions were written in plain JavaScript;
   - the result was refined through many rounds of feedback, covering colours, fonts, layout, motion, performance and content.
3. **No frameworks or build tools:** it's one HTML file, plus images, fonts and two small content files.

---

## Technical overview

**Layout**
- The desktop layout is a fixed **1440 × 9098 px artboard** that matches the Figma frame. CSS `zoom` scales it to the window, so every element keeps its exact position relative to the others.
- Below 640 px wide, the site switches to a stacked layout for phones.

**Artwork**
- The Figma illustrations use grainy noise textures. These were **pre-rendered to WebP at 1× and 2×**, and the browser loads whichever matches the screen. The grain looks the same as the design without being recalculated while you scroll.
- Lotus petals, lily pads, buds, bubbles and fish are separate images, so each one can move on its own.

**Animation**
- Lily pads, bubbles and the intro use CSS and Web Animations.
- Petals, buds, kelp and fish use small spring simulations, driven by `requestAnimationFrame`.
- Everything moves using transforms only, so the graphics card can move it without redrawing. For example, the kelp is a chain of jointed pieces, each rotated at its joint.
- Sunbeams and floating specks are drawn on small `<canvas>` elements.
- Animations pause automatically while they're off screen.

**Content**
- Projects and hobby content live in `content/projects.json` and `content/hobbies.json`, and the page loads them when it opens.
- Because of this, content can be added through **Pages CMS** without touching code.

**Loading**
- Images further down the page load lazily.
- Once the page has settled, those images are fetched and decoded one at a time in idle moments, so jumping to the bottom stays smooth.

---

## Project structure
```
index.html            The whole site: layout, styles and scripts
content/
  projects.json       Project cards
  hobbies.json        Books, games, travel, food, art, nails, music song list
assets/
  decor/              Pond artwork (lily pads, lotus petals, fish, sand, chest, kelp textures…), 1× and @2x
  art/                Digital Art (2d/, 3d/) and Gel-X (nails/) gallery images, full size + thumbnails
  projects/           Project screenshots and looping clips (MP4)
  hobbies/            Hobby images (e.g. game covers)
  uploads/            Images added through Pages CMS
  fonts/              Web fonts (see Credits)
  favicon.svg, favicon-32.png, apple-touch-icon.png, social-preview.jpg
.pages.yml            Pages CMS setup (which fields can be edited)
.nojekyll             Tells GitHub Pages to publish files as-is
CNAME                 Custom domain (nilmi.net)
SETUP-GUIDE.md        Step-by-step guide: preview, publish, update, troubleshoot
```

---

## Running it locally
The page loads its content files, and browsers block that when you open `index.html` directly. Preview it through a local server instead:

- **VS Code:** install the **Live Server** extension (it's suggested automatically), then click **Go Live**.
- **Terminal:** run `python3 -m http.server 8000` in this folder, then open http://localhost:8000.

To preview the phone layout, open DevTools (F12) and turn on device mode (Ctrl+Shift+M).

---

## Publishing (GitHub Pages)
The site is served by GitHub Pages from the `main` branch, root folder, using the custom domain in `CNAME`.
Push to `main` and the live site updates within a minute or two.
`SETUP-GUIDE.md` has the full step-by-step instructions and troubleshooting.

---

## Updating content (Pages CMS)
1. Go to https://app.pagescms.org, sign in with GitHub, and open this repo.
2. **Projects** and **Outside of work** appear as forms. Add or edit entries, upload pictures, and **Save**.
3. Saving commits to GitHub, and the site updates automatically.

Tips:
- Book and game covers look best at a **2:3** ratio (e.g. 600×900).
- Keep photos under about 500 KB.
- For games on Steam, enter the **Steam app ID** (the number in the store link) and the cover is fetched automatically.
- The music song list doesn't sync with Spotify by itself. Add songs there when the playlist changes.

To change wording or layout, edit `index.html` directly.

---

## Services used
| Service | Used for |
|---|---|
| **GitHub Pages** | Hosting |
| **Pages CMS** | Editing content through forms |
| **FormSubmit** | Sends contact-form messages to my inbox. The first message triggers a one-time activation email. |
| **Spotify Embed / iFrame API** | Music player with 30-second previews, and full songs for logged-in Spotify users |
| **Steam** | Game cover art for Steam titles |
| **GoatCounter** | Privacy-friendly visit counts: no cookies, and only counted on nilmi.net |

---

## Accessibility & performance
- **Reduced motion:** visitors who have "reduce motion" turned on in their system settings get a still page, with no intro and no animations.
- **Keyboard:** pop-ups can be closed with Esc, gallery images browsed with the arrow keys, and the intro skipped with any key.
- **Screen readers:** decorative artwork is hidden from them.
- **Speed:**
  - Animations pause when off screen.
  - Images load lazily and decode in the background.
  - Moving pieces only use transforms, so the graphics card moves them without redrawing.

---

## Credits
- **Design & illustrations:** Pehara Vidanagamachchi
- **Fonts:**
  - Desevon, Semika, Sparky Dream and Ethereal.
  - Crimson Text, Playfair Display and Source Serif 4, under the SIL Open Font License (licence files are in `assets/fonts/`).
- **Built with:** Claude by Anthropic, from the Figma design.
- Game covers and logos belong to their respective publishers and are shown here for personal, non-commercial reference.

© 2026 Pehara Vidanagamachchi
