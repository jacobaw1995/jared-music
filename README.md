# jcountrymusic.com

Static site for country artist **Jared Walker**. Hand-written HTML/CSS/JS — no build
step, no framework. Deployed by GitHub Pages from `main`; `CNAME` points the repo at
`jcountrymusic.com`.

## URLs

Every page is a folder with an `index.html` so URLs are clean (`/press/`, not
`/press.html`). The old `*.html` paths still exist as redirect stubs so links already
shared in promo keep working — don't delete them.

| URL | File |
|---|---|
| `/` | `index.html` |
| `/i-cant-love-anymore/` | `i-cant-love-anymore/index.html` |
| `/runnin/` | `runnin/index.html` |
| `/press/` | `press/index.html` |
| `/booking/` | `booking/index.html` |
| `/contact/` | `contact/index.html` |

All asset references are root-absolute (`/assets/...`) so they resolve from any depth.

## Layout

```
assets/
  audio/    web-encoded singles (MP3 256k / M4A)
  covers/   single artwork, web sizes
  logos/    wordmarks + monogram
  og/       social share cards (1200x630)
  photos/   press and hero photography
masters/    NOT COMMITTED — see .gitignore
```

`masters/` holds the full-resolution originals: WAV masters, 3000x3000 cover art,
untouched photography. Git-ignored on purpose — a 76 MB WAV does not belong in a
Pages repo. Back it up somewhere that isn't this folder.

## Adding a release

1. Drop the master + 3000x3000 art in `masters/`.
2. Encode: `ffmpeg -i masters/<song>.wav -b:a 256k assets/audio/<slug>.mp3`
3. Resize art to `assets/covers/<slug>-1400.jpg` and `-700.jpg`.
4. Copy `i-cant-love-anymore/` to `<slug>/`, update the title, date, art and audio paths,
   and paste the store URLs into the `LINKS` object at the top of its `<script>`.
   An empty string renders that platform button greyed out until the link exists.
5. On `index.html`: point the hero CTA at the new page, update the featured release
   card, and add a track row (`data-audio="..."` makes it play inline).
