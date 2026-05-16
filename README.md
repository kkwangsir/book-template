# Book Template

Svelte-based children's book template. Write content in `book.json`, build to static HTML.

## Quick Start

```bash
# Create a new book from this template
npx degit kkwangsir/book-template my-new-book
cd my-new-book

# Install dependencies (first time only)
npm install

# Edit your book content
vim book.json

# Add images to images/
cp /path/to/images/*.png images/

# Build
npm run build

# Preview locally
npx serve dist
```

## book.json Structure

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Book title (cover + page title) |
| `subtitle` | string | Subtitle (can include `<br>` for line breaks) |
| `author` | string | Author credit |
| `pages[]` | array | Story pages |
| `pages[].title` | string | Page title (for table of contents) |
| `pages[].layout` | string | Layout type: `bottom-overlay`, `left-right`, `full-bleed` |
| `pages[].img` | string | Image filename (must be in `images/`) |
| `pages[].text` | string | Page text. `\n\n` = paragraph break, `\n` = line break |
| `vocabulary[]` | array | (Optional) Vocabulary list |
| `questions[]` | array | (Optional) Multiple choice questions |

## Available Layouts

| Layout | Description |
|--------|-------------|
| `bottom-overlay` | Full-bleed image with text box at bottom (default) |
| `left-right` | Image left 60%, text right 40% |
| `full-bleed` | Full-page image, no text |

## Deploy to GitHub Pages

```bash
npm run build
cd dist
git init
git add -A
git commit -m "deploy"
git remote add origin git@github.com:kkwangsir/my-new-book.git
git push -u origin master
# Enable Pages → deploy from master branch / (root)
```

## Development

```bash
npm run dev    # Start Vite dev server with Svelte component preview
npm run build  # Build static HTML from book.json
```

## License

MIT
