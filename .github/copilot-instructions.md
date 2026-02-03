# Pastor Plus Web - AI Coding Instructions

## Project Overview
A static website for Pastor Plus, built with **Hugo** and deployed to GitHub Pages. The site connects US supporters with pastors in Poland, offering monthly theological book partnerships. Single-page site with minimal custom theme and no external JavaScript dependencies.

## Architecture

### Static Site Generation (Hugo)
- **Single entry point**: `content/_index.md` - the only content file, generates the homepage
- **Custom minimal theme**: `themes/pastor-plus-minimal/` (no external dependencies)
- **Theme structure**:
  - `layouts/_default/baseof.html` - base HTML template with header, footer, container
  - `layouts/index.html` - homepage content block (uses `{{ .Content }}` from markdown)
  - `static/css/style.css` - all styling (141 lines, utilities + page layout)
- **Build output**: `hugo` command generates static HTML to `public/`
- **Configuration**: `config.toml` - sets baseURL, title, logo path, menu items

### Key Design Patterns
1. **Content-driven**: All site content lives in markdown frontmatter + body of `content/_index.md`
2. **Logo path pattern**: Dynamic logo via `config.toml` → `baseof.html` uses `relURL` filter
3. **Container-based layout**: `.container` max-width 900px, used in header/main/footer sections
4. **Minimal CSS**: System font stack, no CSS framework; color scheme uses `#1a5490` (blue) for headings

## Developer Workflows

### Local Development
```bash
# Install Hugo (https://gohugo.io/installation/)
hugo server
# Site watches for changes, available at http://localhost:1313
```

### Production Build
```bash
hugo  # Generates public/ directory for GitHub Pages deployment
```

### Build & CSS Processing
- `package.json` includes PostCSS + Autoprefixer (not currently used in build)
- CSS is currently static; if adding PostCSS, integrate into Hugo build process

## Common Tasks

### Edit Site Content
Modify `content/_index.md` only. Hugo watches for changes during `hugo server`.

### Update Styling
Edit `themes/pastor-plus-minimal/static/css/style.css`. Changes apply immediately in dev mode.

### Change Logo
1. Add image to `static/images/` 
2. Update `params.logo` path in `config.toml`
3. The `baseof.html` template automatically handles display with `relURL` filter

### Customize Theme
- Modify HTML: `themes/pastor-plus-minimal/layouts/_default/baseof.html` or `layouts/index.html`
- Modify CSS: `themes/pastor-plus-minimal/static/css/style.css`
- HTML color palette: `#1a5490` (header), `#333` (text), `#666` (muted), `#fafafa` (background)

## Important Conventions

1. **Markdown frontmatter**: `title` and `description` in `_index.md` are used in `<title>` tag and meta description
2. **Hugo relURL filter**: Used for all asset paths (logo, CSS) to handle baseURL correctly for GitHub Pages subdirectory
3. **No component complexity**: Single-page site means no complex templating—keep changes simple
4. **GitHub Pages deployment**: Happens automatically on push to `main` via Actions; builds Hugo and deploys `public/` to `gh-pages` branch

## File Reference
- Content: [content/_index.md](content/_index.md)
- Theme base: [themes/pastor-plus-minimal/layouts/_default/baseof.html](themes/pastor-plus-minimal/layouts/_default/baseof.html)
- Styles: [themes/pastor-plus-minimal/static/css/style.css](themes/pastor-plus-minimal/static/css/style.css)
- Config: [config.toml](config.toml)
