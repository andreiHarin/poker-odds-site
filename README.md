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


## Updating

The site is plain HTML — edit any file in this folder, commit and push (Option A), or re-drag the folder (Option B). Changes go live in seconds.

If the privacy policy needs to change in a way that materially affects users, also update the **Effective date** at the top of `privacy.html` and `PrivacyPolicy.md` in the parent folder.
