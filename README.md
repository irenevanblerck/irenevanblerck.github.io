# Academic site on GitHub Pages

A one-page academic site for an early-career researcher with teaching and professional
experience. Plain HTML and CSS, no build step. A few lines of JavaScript at the bottom of
`index.html` handle the "Copy BibTeX" buttons, the highlighted section in the contents, the
folding contents on phones and the "Top" button. The page also works without them.

```
index.html      the page
style.css       layout and colours
fonts/          the typefaces, served from the site itself (no Google Fonts, so no visitor data
                goes to Google). Source Serif 4 and Schibsted Grotesk, SIL Open Font License 1.1
404.html        shown for broken links
favicon.svg     browser-tab icon (a serif "I"; edit the letter if you like)
.nojekyll       tells GitHub Pages to serve the files as they are
images/         portrait, figures, share image; images/blog/ for post images
blog/           blog index and one page per post
```

## 1. Fill it in

Replace every `[bracketed text]` in `index.html` (search for `[`). Each section has a short
comment above it saying what belongs there.

**Structure**

| # | Section | What to put in |
|---|---|---|
| — | Header | Name, Google Scholar keywords, both positions |
| — | Sidebar | Portrait, email and CV button first, then the contents, then profile links |
| — | Intro | The BUas bio in two short paragraphs, a "Latest" line, the Roosevelt quote with her photo, and your personal quote |
| 1 | News | At most 4 dated items, newest first. Outputs only (papers, talks, milestones). |
| 2 | Research | PhD focus, first study, ICEC photo, PhD project |
| 3 | Publications | Peer-reviewed (with abstract and Cite) · Reports · Theses |
| 4 | Teaching | Short introduction, current courses, previously taught |
| 5 | Talks & Socratic dialogues | Talks, newest first, plus "In the media" |
| 6 | Blog | The newest 2–3 posts with thumbnails |
| 7 | Curriculum vitae | Positions · Other experience · Education · Expertise |
| — | Closing note | What you are open to, and your email |

**Tips for an early-career page**
- **A short list that is complete beats a long list that is padded.** Delete any sub-section you
  cannot fill with real items. Empty headings look worse than none.
- **Work in progress is fine** under "Under review & in preparation", as long as the label is
  honest. Do not list a journal name for a paper that has not been accepted there.
- **Teaching is a strength, so be concrete:** your role (lecturer, coordinator), level, and
  roughly how many students.
- **Experience outside academia goes under "Other professional experience",** with one line
  on what you did. It explains your profile; it does not need defending.
- **Bold your own name** in references: `<b class="me">Surname, I.</b>`.
- **Margin notes:** `<span class="sn">…</span>` at the end of a sentence appears in the right
  margin on wide screens and inline on small ones. Use it for funders or sources.
- **Removing a section:** delete the `<section>` and its line in the sidebar contents, then
  renumber the `<span>N</span>` in the remaining headings. The sidebar numbers itself, and the
  highlight while scrolling follows automatically.

## 2. Images

Put files in `images/` and change `src` and `alt` in `index.html`.

| Slot | Where | Size |
|---|---|---|
| Portrait | Sidebar (`images/irene-van-blerck.jpg`) | Shown as a circle. To use another photo, replace the file. `object-position` under `.portrait` in `style.css` sets which part stays in view. |
| Figure 1 | Research, the ICEC 2025 photo (`images/icec-2025-talk.jpg`) | A larger original would look sharper |
| Result figure | Research (optional, see the comment there) | 16:9, about 1600×900 px |
| Eleanor Roosevelt | Beside the quote (`images/eleanor-roosevelt-1933.jpg`) | Portrait from 1933, Library of Congress, public domain (via Wikimedia Commons). Shown small and in black and white. |
| `share.jpg` | Preview card when the link is shared on LinkedIn etc. Already made: name, roles, keywords and portrait. | 1200×630 px |

JPG or WebP for photos, PNG or SVG for diagrams, under ~400 KB each. Always write a real `alt`.
Only show people who agreed to it.

## Blog

The two "Back from Tokyo" posts are copied word for word from Substack into `blog/`. Each page
points search engines to the Substack original (`<link rel="canonical">`), so the copies do not
count as duplicate content.

To add a new post:
1. Copy `blog/back-from-tokyo-2.html` and give it a new name, e.g. `blog/my-new-post.html`.
2. Change the `<title>`, the description, the canonical link (the Substack URL of the post),
   the date (both the `datetime="2026-01-31"` attribute and the visible text), the `<h1>`, the
   subtitle, the image and the paragraphs. Each paragraph goes in its own `<p>…</p>`.
3. Fix the Previous/Next links at the bottom of the new post and of the post before it.
4. Add the post at the top of the list in `blog/index.html` and in the Blog section of
   `index.html`. Keep the 2–3 newest posts on the main page. The rest stay reachable through
   "All posts" on every post page.

Images for posts go in `images/blog/`. Save them as JPG of about 1200 px wide.

## Publications: abstract and "Cite"

Each paper has a fold-out abstract and a "Cite" panel with BibTeX and a copy button. To add a
paper, copy a whole `<li>…</li>` in the Publications section and change the reference, the
abstract and the BibTeX. The copy button only works on the published site (https) or on
localhost; opened as a plain file, it selects the text so you can copy it yourself.

## 3. Preview locally

    cd ~/Documents/cv-website
    python3 -m http.server 8000

Open http://localhost:8000. Try a narrow browser window too: on phones the sidebar turns
into a header.

## 4. Publish

1. Create a **public** GitHub repository named exactly `YOURUSERNAME.github.io`.
2. Push the files:

       cd ~/Documents/cv-website
       git init
       git add .
       git commit -m "Initial version"
       git branch -M main
       git remote add origin https://github.com/YOURUSERNAME/YOURUSERNAME.github.io.git
       git push -u origin main

3. Repository → Settings → Pages → Source: *Deploy from a branch* → `main`, `/ (root)`.
4. After about a minute the site is live at `https://YOURUSERNAME.github.io`.
5. In `index.html`, replace `[username]` in the `<head>` (canonical link, og:url, og:image and
   the JSON-LD block) with your GitHub username. Without this, link previews will not work.
   In the two `blog/back-from-tokyo-*.html` pages, make the `og:image` address absolute too
   (`https://YOURUSERNAME.github.io/images/blog/...`), so the post photo shows when shared.
6. `404.html` uses addresses that start with `/`. That works for a `YOURUSERNAME.github.io`
   repository. If you publish under a project address instead, make them relative.

**Custom domain (optional):** Settings → Pages → Custom domain, add a CNAME record at your
registrar pointing to `YOURUSERNAME.github.io`, then tick "Enforce HTTPS". Update the URLs
in the `<head>` to match.

## 5. Keeping it current

- Add a News item when something happens, and drop the oldest.
- Update "Last updated" in the footer when you change something.
- Add your site URL to your ORCID, Google Scholar and LinkedIn profiles, and to your email signature.

## 6. Other things it already does

- Dark mode that follows the visitor's system setting.
- **Print:** in the browser, choose Print / Save as PDF for a clean text-only CV. Navigation,
  images and news are left out.
- Keyboard and screen-reader basics: a skip link, visible focus outlines, `alt` text slots.
- Structured data (`application/ld+json` in the `<head>`) so search engines can connect the
  page to your ORCID and Scholar profiles. Fill it in or delete the block.

## Notes

- Links are kept to what visitors actually use: your profiles, the CV, the papers and the blog
  posts. Avoid linking the same thing twice on one page.

- The footer has a short colophon saying the site was built with help from Claude (Anthropic).
  Edit or remove it in `index.html` (and in the `blog/` pages) as you see fit.
- Check your institution's rules on personal pages before using its name or logo.
- Do not publish details of participants in your Socratic sessions; anonymise or get consent.
