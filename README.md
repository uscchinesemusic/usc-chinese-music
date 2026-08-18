# USC Chinese Music Ensemble — Website

Official website for the USC Chinese Music Ensemble (中国音乐乐团), hosted via GitHub Pages.

**Live site:** [uscchinesemusic.org](https://uscchinesemusic.org)
GitHub Pages URL (also works): [uscchinesemusic.github.io/usc-chinese-music](https://uscchinesemusic.github.io/usc-chinese-music/)

---

## About

USC's Chinese traditional music ensemble, founded Spring 2026. Reborn from Eastern Chamber (东方室内乐队). We play 新民乐 — traditional Chinese instruments fused with pop, rock, electronic, and more.

- Instagram: [@usc_chinesemusic](https://www.instagram.com/usc_chinesemusic/)
- Discord: [discord.gg/fxAmAMBeqC](https://discord.gg/fxAmAMBeqC)
- Email: usc.chinesemusic@gmail.com
- Linktree: [linktr.ee/uscchinesemusic](https://linktr.ee/uscchinesemusic)

---

## Structure

```
/
├── index.html        # Single-page site (all CSS and JS inline, favicon embedded as base64)
└── README.md
```

The site is a single self-contained HTML file — no build step, no dependencies, no framework. Everything (styles, scripts, favicon) is inline in `index.html`.

---

## Deployment (already set up)

- **Source:** Settings → Pages → Deploy from branch → `main` / `/ (root)`
- **Custom domain:** `uscchinesemusic.org`, registered on Porkbun. DNS points to GitHub Pages via 4 A records (apex) + 1 CNAME record (`www`). A `CNAME` file in this repo (auto-created by GitHub when the custom domain was set) tells Pages which domain to serve.
- **HTTPS:** enforced (auto-issued cert via GitHub Pages)

If DNS or the domain ever needs to be redone: 4 A records at the apex host pointing to `185.199.108.153`, `.109.153`, `.110.153`, `.111.153`, and a CNAME for `www` pointing to `uscchinesemusic.github.io`.

---

## Updating the site

Everything lives in `index.html`. Easiest update method: edit the file locally, then **Add file → Upload files** on this repo (or edit in place via the pencil icon) → **Commit changes**. Live in about a minute; hard-refresh (Ctrl/Cmd+Shift+R) to see it, since favicons and some assets cache aggressively.

Still worth doing at some point:

| What | Notes |
|------|-------|
| Rehearsal times | Currently listed as TBD in the Join section — update once scheduled |
| First performance | Once the revived ensemble plays its first show, update the Listen section framing (currently notes performances are from the Eastern Chamber legacy only) |
| Officer/member names | No team section yet — consider adding one |
| OG image | No social link preview image yet — add a 1200×630px `og-image.png` and reference it via `<meta property="og:image">` for clean previews on Discord/iMessage/Instagram |

---

## Forms (all via Google Forms, no backend needed)

The site posts directly to Google Forms using `fetch(..., { mode: 'no-cors' })` — no third-party form service. Three separate forms, three separate response spreadsheets:

| Form | Triggered by | Google Form ID |
|------|--------------|-----------------|
| Musician sign-up | "I want to play" tab | `1FAIpQLScWUibBb_xB6FarLHZunNh411-Jsz1KCYHBMRXa8zWOJdYAAQ` |
| Film scorer inquiry | "I want to hire you" tab | `1FAIpQLSdJrAoR--ASEK9MmtYuiYY677UnSpZWKNmBx-jaE0HAgRguoQ` |
| Donations | Donate section buttons | `1FAIpQLSfPK3t-XyqNk2vHaqffb2Iq9cbmW-MgimpLb71ZevWIPX0K1Q` |

Field mappings live in the `MUSICIAN_FIELDS` / `SCORER_FIELDS` constants near the top of the `<script>` block, and the donate buttons' `entry.429818479` query param.

**Important:** each Google Form must stay **Published**, with **"Collect email addresses" set to "Do not collect"**, no organization restriction, and no "limit to 1 response." If any of these get changed, submissions will silently fail with a 401 — the page still shows "Received!" (a `no-cors` request can't read the real response), so check the response spreadsheets occasionally to confirm submissions are actually arriving.

To add/change a field: add the question to the relevant Google Form, use "Get pre-filled link" to find its `entry.XXXXXXX` ID, then add it to the matching `_FIELDS` object and the `body.append(...)` calls in `handleSubmit()`.

---

## Known quirks

- **YouTube/Instagram embeds require a real HTTP origin.** Opening `index.html` directly from disk (`file://`) breaks them (YouTube error 153). Serve it locally (e.g. a simple HTTP server) or just use the live site to test embeds.
- **Favicon is a hand-processed circular crop** of `easternchamberlogo1.jpg`, embedded as base64 PNG directly in the `<link rel="icon">` tag — no separate image file. If it ever needs regenerating, source art lives wherever the club keeps its logo files.
