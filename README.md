# Children's Book Template (桥梁书)

Zero-dependency book builder for children's early readers. Outputs a single scrollable HTML page → print/save as PDF.

## Quick Start

```bash
git clone git@github.com:kkwangsir/book-template.git my-book
cd my-book

# 1. Put your images in images/ (1024×1536 JPG recommended)
# 2. Edit template/book.json with your story
# 3. Build
node build.js template

# Output: template/docs/index.html
```

## Layout

One scrollable page, ready to print:
```
Cover → Vocabulary List → Story Pages → Reading Comprehension → Answer Key
```

Letter size (215.9×279.4mm). Open `docs/index.html` → Ctrl+P → Save as PDF.

## Structure

```
my-book/
├── images/            # page_01.jpg, page_02.jpg ...
├── book.json          # Story data
└── build.js           # Build script (stands alone, no npm install)
```

## book.json Format

See `template/book.json` for the full schema.

Required fields:
- `pages[]` — title, img (filename), text (use `\n\n` for paragraphs), layout ("bottom-overlay" or "left-right")
- `vocabulary[]` — word, pron (IPA), type, zh, en
- `questions[]` — n, q, opts[4], ans, text, exp

## Image Guidelines

- **Size:** 1024×1536 (portrait, matches Letter)
- **Format:** JPG quality 85 (~400KB/page recommended)
- **Content:** Use GPT Image 2 ("Western comic book art, American graphic novel style")
- **Character:** Keep consistent appearance across pages

## Build & Deploy

```bash
# Build outputs to docs/
node build.js .

# Deploy to GitHub Pages
git init
git add -A
git commit -m "initial book"
git remote add origin git@github.com:<USER>/<REPO>.git
git push -u origin master

# Settings → Pages → branch: master, folder: /docs
```

## Tech

- **Standalone Node.js** — just `node build.js`, no npm install needed
- **WeasyPrint** (optional) — `pip install weasyprint && weasyprint docs/index.html book.pdf`
- **Letter size** — `@page{size:Letter;margin:0}` for exact PDF output
- **Print colors** — `print-color-adjust:exact` preserves backgrounds in Chrome
