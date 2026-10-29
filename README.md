# soul // it

The Italian sibling of [`soul`](https://github.com/thesouldevotional/soul) — a personal, static devotional site: bible verses, prayers, saint biographies, and short "commonplace" quotes, some with a short personal reflection. Same structure and build as `soul`, translated content, CEI 2008 as the bible source instead of NLT. Plain HTML + `.txt` content files, no build step, no framework, no database. Live at:

**https://thesouldevotional.github.io/soul-it/**

## How it's built

Identical mechanics to `soul`: no static site generator, a handful of hand-written HTML pages, one `.txt` file per piece of content, and a tiny client-side script in `post.html` that fetches a `.txt` file and renders it with a small custom markup engine. Adding content is just adding a `.txt` file (plus updating a couple of index pages) — no rebuild, just `git push`.

## Deploy

`.github/workflows/deploy-pages.yml` deploys the repo to GitHub Pages on every push to `main` (same workflow as `soul`). The whole repo root is uploaded as-is — whatever is on `main` is what's live, usually within a minute or two of pushing.

## Repo structure

```
index.html                    homepage — title "soul // it" + description, links to the archives
post.html                     single-post viewer — renders any .txt file passed via ?p=
archive.html                  ALL verses + prayers in one page, with two anchor-based indexes
all-prayers-archive.html      flat list of every prayer, newest first (drives the prayers loop)
all-verses-archive.html       flat list of every verse, newest first (drives the verses loop)
all-commonplace-archive.html  flat list of every commonplace entry, newest first (drives its own loop)
saints.html                   list of every saint, linking to their individual page
saints-index.txt              internal-only lookup index of saint connections
topics.html                   topic index — generated at load time from archive.html's topic sections
books-of-the-bible.html       every book with an explainer, grouped in ten canonical sections
guides/                       long-form guides (e.g. how to read the bible)
path-for-the-skeptical.html   a six-question path through scripture
soulfavicon.png / soulfavicon_dark.png   favicon light/dark (S, editorial style)
apple-touch-icon.png          iOS Home icon (180×180)

bible/          {book}_{chapter}-{verse}.txt   e.g. isaiah_60-22.txt — English slug shared with soul, Italian content
prayers/        {title-slug}.txt               Italian slug, e.g. sei-tutto-cio-di-cui-ho-bisogno.txt
commonplace/    {title-slug}.txt                Italian slug
what-is-it/     {book-slug}.txt                 same English book-slug as soul, Italian content
saints/         {name-slug}.txt                 Italian/canonical saint name slug
```

## Language selector

Every page links to its exact counterpart on `soul` (English), and vice versa — a page-by-page correspondence, not just homepage-to-homepage. Bible and book-explainer files share the same filename across both repos (no mapping needed); prayers, commonplace, and saints use the actual translated filename on each side.

## Content types

Same shapes as `soul` — bible verse, prayer, commonplace, book explainer, saint bio — with Italian fixed phrasing (`↳ vedi altri versetti sullo stesso argomento`, `~ ↳ fonte:`, etc.) and the loop link reading `leggi [un altro](...)` / `vedi [un altro](...)` instead of `read`/`see another one`.

## The "leggi/vedi un altro" loop

Same closed-loop mechanics as `soul` — three independent rings (verses, prayers, commonplace), each tracked by its own flat "all" page, newest first.

## Archive & topic system

Same as `soul`: `archive.html` is the single hub for all verses and prayers, with a `↳ autore / libro` index and an `↳ argomento` link to `topics.html`. Topics are chosen independently per site — an Italian topic doesn't need to match its English counterpart's slug, only the underlying grouping.

## Content creation

New content is added the same way as on `soul`: whenever a verse, prayer, saint, or commonplace entry is added to `soul` via its Claude Code skill, that skill also drafts and writes the Italian counterpart here in the same run — translation, archive updates, saint connections, and the loop chain. Changes are committed and pushed together with `soul`, at the end of a working session. Book explainers (`what-is-it/`) follow the same three-paragraph format as `soul`, with a `se di questo libro leggi poco, leggi questo` footer.

## Style rules (content)

Same lowercase rule as `soul`, applied to Italian — everything lowercase, including sentence-initial words, **except**:
- words referring directly to God (`Signore`, `Dio`, `Lui`, `Suo`, `Cielo`, `Tu`/`Tuo` when addressing God directly, …)
- words referring to a saint (`Lui`, `Suo`, …) anywhere the saint is discussed
- proper names (people, places, bible books, "CEI 2008")
