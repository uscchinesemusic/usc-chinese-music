# Chinese Music Ensemble at USC: Website

Official website for the Chinese Music Ensemble at USC (民乐团), hosted on GitHub Pages.

**Live site:** [uscchinesemusic.org](https://uscchinesemusic.org)
GitHub Pages URL (also works): [uscchinesemusic.github.io/usc-chinese-music](https://uscchinesemusic.github.io/usc-chinese-music/)

---

## About

USC's ensemble for traditional Chinese instruments, founded Spring 2026 and reborn from Eastern Chamber (东方室内乐队). We play 新民乐: traditional Chinese instruments fused with pop, rock, electronic and more. New members can join anytime, with no audition.

- Instagram: [@usc_chinesemusic](https://www.instagram.com/usc_chinesemusic/)
- Discord: [discord.gg/fxAmAMBeqC](https://discord.gg/fxAmAMBeqC)
- YouTube: [@uscchinesemusicensemble](https://www.youtube.com/@uscchinesemusicensemble)
- Email: usc.chinesemusic@gmail.com
- Linktree: [linktr.ee/uscchinesemusic](https://linktr.ee/uscchinesemusic)

---

## Structure

```
/
├── index.html        # Single-page site (all CSS, JS and logos inline)
├── photos/           # Event photos (each in a full size and a smaller phone size)
│   ├── cover.jpg, cover-1000.jpg            # Cover photo
│   └── recording.jpg, recording-800.jpg     # Filmmakers section photo (short film recording session)
└── README.md
```

The site has no build step and no framework. Styles, scripts, the logos and the tab icon are all inside `index.html` (the logos are embedded as base64 images). The event photos live in `photos/`, so **always upload the `photos` folder along with `index.html`** when it changes, or the photos will show as broken. Two things load from outside: the fonts (Newsreader and Noto Serif SC from Google Fonts) and the video thumbnails (straight from YouTube).

To swap a photo, replace the file in `photos/` with a new one of the same name (landscape, about 2000px wide for the cover and 1400 to 1600px for the others, under about 300 KB), or point the `src` and `srcset` in `index.html` at a new file. Strip location data from phone photos before uploading.

Photo sources: the cover photo is from USC Spoon's Crazy Rich Asians event; the Filmmakers photo is from the ensemble recording for a short film in Spring 2026.

The page is designed like a bilingual concert program. Sections in order: cover, Past performances, Instruments, Our story, Filmmakers and composers, Support the ensemble, Instagram, Join us (with the sign-up form and FAQ), footer.

---

## Deployment (already set up)

- **Source:** Settings → Pages → Deploy from branch → `main` / `/ (root)`
- **Custom domain:** `uscchinesemusic.org`, registered on Porkbun. DNS points to GitHub Pages through 4 A records (apex) and 1 CNAME record (`www`). A `CNAME` file in this repo (created by GitHub when the custom domain was set) tells Pages which domain to serve. Don't delete it.
- **HTTPS:** enforced (certificate issued automatically by GitHub Pages)

If DNS or the domain ever needs to be redone: 4 A records at the apex host pointing to `185.199.108.153`, `.109.153`, `.110.153`, `.111.153`, and a CNAME for `www` pointing to `uscchinesemusic.github.io`.

---

## Updating the site

Everything lives in `index.html`. Edit the file on your computer, then on this repo click **Add file → Upload files**, drop in the new `index.html`, and click **Commit changes**. It goes live in about a minute. Hard refresh (Ctrl+Shift+R, or Cmd+Shift+R on a Mac) to see it, since tab icons and some files cache aggressively.

The file is large (about 230 KB) because the logos are embedded in it. That's expected. If you edit it in GitHub's pencil editor, search for the text you want instead of scrolling.

Common edits:

| What | Where in `index.html` |
|------|------|
| Semester wording (currently Spring 2027) | Search for `2027` |
| Rehearsal times | The "Join us" lede and the FAQ answer "When are rehearsals?" |
| Videos | The `<ol class="pieces">` list. Each piece has a YouTube ID in `href` and `data-id`, plus its titles. The first piece is also set as the default in the player above the list. |
| FAQ | Search for `class="faq"` |

Still worth doing at some point:

| What | Notes |
|------|-------|
| Officer/member names | No team section yet. Consider adding one. |
| Social preview image | No link preview image yet. Add a 1200×630px `og-image.png` and reference it with `<meta property="og:image">` for clean previews on Discord, iMessage and Instagram. |

---

## Forms (all through Google Forms, no backend)

The site posts directly to Google Forms using `fetch(..., { mode: 'no-cors' })`, with no third-party form service. Three separate forms, three separate response spreadsheets:

| Form | Triggered by | Google Form ID |
|------|--------------|-----------------|
| Musician sign-up | "I want to play" tab | `1FAIpQLScWUibBb_xB6FarLHZunNh411-Jsz1KCYHBMRXa8zWOJdYAAQ` |
| Film scorer inquiry | "I want to hire you" tab | `1FAIpQLSdJrAoR--ASEK9MmtYuiYY677UnSpZWKNmBx-jaE0HAgRguoQ` |
| Donations | Support section links | `1FAIpQLSfPK3t-XyqNk2vHaqffb2Iq9cbmW-MgimpLb71ZevWIPX0K1Q` |

Field mappings live in the `MUSICIAN_FIELDS` and `SCORER_FIELDS` constants in the `<script>` block, and in the donate links' `entry.429818479` parameter.

**Important:** each Google Form must stay **Published**, with **"Collect email addresses" set to "Do not collect"**, no organization restriction, and no "limit to 1 response." If any of these change, submissions fail silently with a 401. The page still shows "Received!" because a `no-cors` request can't read the real response, so check the response spreadsheets now and then to confirm submissions are arriving.

To add or change a field: add the question to the Google Form, use "Get pre-filled link" to find its `entry.XXXXXXX` ID, then add it to the matching `_FIELDS` object and the `body.append(...)` calls in `handleSubmit()`.

---

## Known quirks

- **YouTube and Instagram embeds need a real web address.** Opening `index.html` straight from your computer (`file://`) breaks them (YouTube error 153). Test on the live site, or serve the file locally.
- **Logos:** the tab icon is the black and white CME logo on a white circle; the header uses the red circle CME logo; the footer uses the black, red and gold version; Our story shows the old Eastern Chamber logo next to the new one. All are embedded as base64 inside `index.html`. Keep the original logo files somewhere the club can find them, in case they need to be swapped.
