# Poker Odds — Marketing Site

A tiny static site (5 files, no build step, no JavaScript) that serves three pages:

- `index.html` — landing page describing the app, with a GTO comparison and the educational/no-betting disclaimer baked in.
- `privacy.html` — full privacy policy ready to point Apple at as the **Privacy Policy URL**.
- `support.html` — FAQ + contact info ready to point Apple at as the **Support URL**.

Plus a shared `style.css` (dark theme matching the app icon) and a copy of `appicon.png` used as favicon and hero image.

## Files

```
site/
├── README.md          # this file
├── appicon.png        # 1024x1024 RGB sRGB, no alpha
├── index.html         # /
├── privacy.html       # /privacy.html
├── style.css          # shared stylesheet
└── support.html       # /support.html
```

## Before you publish: fill in the placeholders

Search the site folder for `[YOUR-EMAIL]` and replace it with the real email address you want users (and Apple's reviewers) to contact you at. There are several occurrences across `privacy.html` and `support.html`.

On Windows / PowerShell, from `ios/metadata/site/`:

```powershell
(Get-ChildItem -Filter *.html) | ForEach-Object {
    (Get-Content $_.FullName -Raw) -replace '\[YOUR-EMAIL\]', 'you@example.com' |
        Set-Content $_.FullName -NoNewline
}
```

Or just open the files in your editor and find/replace.

---

## Option A — GitHub Pages (free, recommended)

The whole flow takes about 5 minutes.

### 1. Create a new public GitHub repository

Name it something stable; the bundle ID `com.andreiharin.pokerodds` suggests `pokerodds` or `pokerodds-site`. **The name becomes part of the URL** (you can also rename later).

### 2. Push the contents of this `site/` folder to the repo

From the repo root on disk (a fresh clone of the empty repo):

```bash
# copy the contents (not the folder itself) of ios/metadata/site/ into the repo root
git add .
git commit -m "Initial site"
git push origin main
```

### 3. Turn on GitHub Pages

On github.com, in the repo:

1. Settings → Pages.
2. **Source:** Deploy from a branch.
3. **Branch:** `main`, folder `/ (root)`.
4. Save.

After 30–90 seconds, Pages publishes at:

```
https://<your-github-username>.github.io/<repo-name>/
```

For example: `https://andreiharin.github.io/pokerodds/`

### 4. Use these URLs in App Store Connect

| App Store Connect field | URL |
|---|---|
| Marketing URL (optional) | `https://andreiharin.github.io/pokerodds/` |
| **Support URL** (required) | `https://andreiharin.github.io/pokerodds/support.html` |
| **Privacy Policy URL** (required) | `https://andreiharin.github.io/pokerodds/privacy.html` |

Done. Apple will accept these URLs.

### Optional: custom domain

If you own a domain (e.g. `pokerodds.app`), in Pages settings add it under **Custom domain**, then add a `CNAME` record at your DNS provider pointing to `<username>.github.io`. Pages auto-provisions HTTPS via Let's Encrypt.

---

## Option B — Netlify drop (also free, even faster)

1. Go to <https://app.netlify.com/drop>.
2. Drag the entire `site/` folder onto the page.
3. You instantly get a URL like `https://random-name.netlify.app/`.
4. Optional: rename the site under Site settings → Change site name → e.g. `pokerodds`.

URLs to use in App Store Connect:

| Field | URL |
|---|---|
| Support URL | `https://pokerodds.netlify.app/support.html` |
| Privacy Policy URL | `https://pokerodds.netlify.app/privacy.html` |

---

## Option C — Cloudflare Pages

1. Push the `site/` contents to a GitHub repo (same as Option A step 2).
2. Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git.
3. Pick the repo. **Build command:** leave empty. **Output directory:** `/` (root).
4. Deploy.

You get `https://pokerodds.pages.dev/` (or similar).

---

## Local preview

To check the pages render correctly before publishing, you can serve them locally with Python's built-in server:

```powershell
cd ios\metadata\site
python -m http.server 8000
```

Then open <http://localhost:8000/> in a browser. All three pages and the icon will render as they will live.

---

## Updating

The site is plain HTML — edit any file in this folder, commit and push (Option A), or re-drag the folder (Option B). Changes go live in seconds.

If the privacy policy needs to change in a way that materially affects users, also update the **Effective date** at the top of `privacy.html` and `PrivacyPolicy.md` in the parent folder.
