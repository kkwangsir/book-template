# Children's Book Template (桥梁书)

Zero-dependency book builder for children's early readers. Outputs a single scrollable HTML page → print/save as PDF.

## Quick Start

```bash
git clone git@github.com:kkwangsir/book-template.git my-book
cd my-book/template

# 1. Put images in images/ (1024×1536 JPG)
# 2. Edit book.json with your story
# 3. Build
node ../build.js .

# Output: docs/index.html — open in browser → Ctrl+P → Save as PDF
```

## Layout (pages[] mode)

```
Cover → Vocabulary → Story pages → Questions → Answer Key
```

## Layout (chapters[] mode)

```
Cover → Ch1 Title → Vocab → Pages → Ch2 Title → Vocab → Pages → ... → All Questions → All Answers
```

## Single Chapter Build

```bash
node ../build.js . --chapter 1   # → docs/chapter-01.html
node ../build.js . --chapter 2   # → docs/chapter-02.html
```

Each chapter gets its own vocabulary and title page. Questions accumulate across chapters and appear at the end.

## PDF Export

```bash
# Full book PDF
weasyprint docs/index.html "My Book.pdf"

# Single chapter PDF
weasyprint docs/chapter-01.html "Chapter 1.pdf"

# Or just open the HTML in Chrome → Ctrl+P → Save as PDF
```

## Structure

```
my-book/
├── images/            # page_01.jpg, ch01_01.jpg, etc.
├── book.json          # Story data (pages[] or chapters[])
└── build.js           # Build script (from parent dir)
```

## book.json Format

See `template/book.json` for a full example.

Two modes:

**Simple (pages[]):**
```json
{
  "pages": [...],
  "vocabulary": [...],
  "questions": [...]
}
```

**Chapter book (chapters[]):**
```json
{
  "chapters": [
    {
      "title": "Chapter Name",
      "subtitle": "Optional subtitle",
      "pages": [...],
      "vocabulary": [...],
      "questions": [...]
    }
  ]
}
```

## Image Guidelines

- **Size:** 1024×1536 (portrait, Letter ratio)
- **Format:** JPG quality 85 (~400KB/page)
- **Style:** Western comic book art

## Tech

- **Standalone Node.js** — just `node build.js`, no npm install
- **WeasyPrint** — `pip install weasyprint` for server-side PDF
- **Letter size** — `@page{size:Letter;margin:0}`
- **Code in this repo** — content repos gitignore build.js
