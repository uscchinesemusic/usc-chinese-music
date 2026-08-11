# USC Chinese Music Ensemble — Website

Official website for the USC Chinese Music Ensemble (中国音乐乐团), hosted via GitHub Pages.

**Live site:** [uscchinesemusic.github.io](https://uscchinesemusic.github.io)

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
├── index.html        # Single-page site (all CSS and JS inline)
└── README.md
```

The site is a single self-contained HTML file — no build step, no dependencies, no framework. Everything is inline.

---

## Deploying via GitHub Pages

1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Under **Source**, select `main` branch and `/ (root)` folder
4. Save — your site will be live at `https://<your-username>.github.io/<repo-name>` within a minute or two

### Custom domain (optional)

If you have a domain (e.g. `uscchinesemusic.com`):

1. Add a file called `CNAME` to this repo containing just your domain name:
   ```
   uscchinesemusic.com
   ```
2. In your domain registrar's DNS settings, add a CNAME record pointing to `<your-username>.github.io`
3. Back in GitHub Pages settings, enter your custom domain and enable "Enforce HTTPS"

---

## Updating the site

All content is in `index.html`. Things you'll want to update over time:

| What | Where in the file |
|------|------------------|
| Rehearsal times | Join section perks, hero card |
| Performance/event dates | Add an events section |
| Officer names | Add a team section |
| YouTube videos | Replace placeholder video cards with `<iframe>` embeds |
| Join form backend | Wire the form to a Google Form or Formspree endpoint |

### Wiring the join form to Google Forms

1. Create a Google Form with matching fields
2. Get the form's POST URL (inspect the form action on the published form)
3. Replace the `handleSubmit()` function in the `<script>` tag with a proper `fetch()` POST to that URL

Or use [Formspree](https://formspree.io) — free for low volume, just swap the form action to your Formspree endpoint.

---

## OG Image

For link previews (iMessage, Discord, Instagram DMs), add a file called `og-image.png` to the repo root — recommended size is 1200×630px. Use one of your existing flyers scaled to that size.
