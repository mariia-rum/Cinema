# EVOS FILM website

This is the website of **EVOS FILM**, a film company from Kyiv, Ukraine.
It lives at **[evosfilm.com](https://evosfilm.com)**.

EVOS FILM does two things, and the site is split the same way:

- **Production.** The films EVOS FILM has made, such as *How Is Katia?*
  (Locarno, 2022) and *My Magical World* (2025), and the ones in development.
- **Distribution.** As **Ukrajina Cinema**, EVOS FILM brings new Ukrainian
  films to cinemas across Germany.

There is also an About page (the company and producer Olha Matat) and a page
for the short film in development, *It's All Soderbergh's Fault*.

It is a simple, hand-made site: a few web pages, their styles and the images.
No website builder and nothing to install. Change a file here and the live site
updates a minute later.

---

## For whoever looks after the site

Plain static HTML and CSS, plus a little vanilla JavaScript (the door intro on
the film page, the trailer preview). No framework, no build step, no tracking.

```
index.html                 company home
soderbergh/index.html      It's All Soderbergh's Fault (the link for emails)
about/index.html           company and producer
assets/                    all images
assets/css/site.css        company shell styles
assets/css/home.css        home only: Production | Distribution split, Ukrajina Cinema section
assets/css/soderbergh.css  film page styles (palette, night-to-morning)
assets/ukrajina-cinema/    distributed films' posters (640 px wide), logo, poster-wall.jpg
```

To add a film to Ukrajina Cinema: save its poster as
`assets/ukrajina-cinema/<slug>.jpg` (640 px wide JPEG), then copy one
`<li class="uc-film">` block in `index.html` and change the slug (it appears
twice), the titles, the facts and the synopsis. Posters of any shape are shown
whole, never cropped.

### Before publishing: three find-and-replace jobs

Search the whole folder (VS Code: Ctrl/Cmd + Shift + F) and replace:

1. `PLACEHOLDER-SITE-URL` → the live address without a trailing slash,
   e.g. `evosfilm.github.io/evos-film` or `evosfilm.com`. Used only in the
   canonical and preview-card tags, which must be absolute URLs.
2. `PLACEHOLDER-EMAIL` → the public email address (used in every `mailto:` link).
3. `<span class="ph">[PLACEHOLDER: public email]</span>` → the same email as plain text.

Then search for `[PLACEHOLDER` to find every remaining gap. Each one shows on
the page as a yellow highlight, so nothing missing can go live unnoticed.

### Replacing images

To change an image, save the new one over the old file in `assets/` with
**exactly the same filename** and it appears on the site. No HTML edits needed.

| File | What goes there | Suggested size |
|---|---|---|
| `soderbergh-key.jpg` | Key art (metro, Dnipro, two windows) | 2400 px wide, JPEG quality ~75, under 400 KB |
| `soderbergh-og.jpg` | Link-preview card: a crop of the key art | exactly 1200 × 630 |
| `og-evos.jpg` | Link-preview card for home and about | exactly 1200 × 630 |
| `how-is-katia-poster.jpg`, `my-magical-world-poster.jpg`, `all-clear-poster.jpg` | Posters | 800 × 1200 |
| `team-*.jpg` | Portraits (cropped to 4:5 on the page) | 800 × 1000 |

`soderbergh-og.jpg` and `og-evos.jpg` are currently type-only cards (title and
palette, no imagery) so that link previews work from day one. Replace
`soderbergh-og.jpg` with a key-art crop once the photo is in.

If the key art is not 3:2, update `width` and `height` on its `<img>` tags
(home and film page) to the real pixel size. This prevents layout jumps.

Compress before adding: [squoosh.app](https://squoosh.app) (MozJPEG, quality
70–80) works in the browser.

### Adding a new film page

1. Copy the `soderbergh/` folder and rename it, e.g. `katia/`.
2. Copy `assets/css/soderbergh.css` to `assets/css/katia.css` and change the
   palette variables at the top to the new film's colours. Rename the
   `.film-soderbergh` class in both files (e.g. `.film-katia`).
3. In `katia/index.html`: change the stylesheet link, the `<body>` class, the
   `<title>`, meta description, every `og:` and `twitter:` tag (including the
   URL `/katia/`), and the content. Remove sections that do not apply.
4. Add images to `assets/` with a clear prefix (`katia-key.jpg`, `katia-og.jpg`).
5. On `index.html`, link the film's entry in the Films list to `katia/`.

Links are relative (`../assets/...`), so pages work in any folder and on any
GitHub Pages address.

### Deploying to GitHub Pages

1. Create a repository on GitHub. Upload the **contents** of this folder so
   that `index.html` sits at the repository root (web: "Add file → Upload
   files", drag everything in; or push with git).
2. Repository → Settings → Pages → Source: "Deploy from a branch",
   Branch: `main`, folder `/ (root)`. Save.
3. After a minute the site is live at `https://<username>.github.io/<repo>/`.
   The film link is that address plus `soderbergh/`.
4. Custom domain (optional): Settings → Pages → Custom domain, then follow
   GitHub's DNS instructions.

Check the preview card after deploying by pasting the film link into
LinkedIn's Post Inspector (linkedin.com/post-inspector). It also refreshes a
cached card after you change an image.

### Optional sections (director's statement, Danya and Khvylovyi)

These are **not** in this folder. They are in
`PRIVATE_soderbergh-optional-sections.html`, delivered separately. Keep that
file out of the repository: a public repository and the page source are both
readable by anyone, including text inside HTML comments. To switch a section
on after approval, paste its block where `soderbergh/index.html` says
`OPTIONAL SECTIONS SWITCH`.

### Rules that keep this site credible

- No stills from other films. Reference films are named in text only.
- No public video player or screener link for It's All Soderbergh's Fault
  (premiere eligibility). Screeners go out privately.
- No analytics, cookie banner, pop-ups or embeds.
