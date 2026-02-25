# How to Export to PDF and PowerPoint

AgentPreso renders your markdown deck to three formats: HTML for web viewing, PDF for sharing and printing, and PPTX for editing in PowerPoint or Google Slides.

## Export from the CLI

### HTML (default)

```bash
agentpreso render deck.md
```

Produces `deck.html` — a self-contained file you can open in any browser.

### PDF

```bash
agentpreso render deck.md --format pdf
```

Produces `deck.pdf` — print-ready with all charts, diagrams, and theme styling baked in.

### Editable PowerPoint

```bash
agentpreso render deck.md --format pptx
```

Produces `deck.pptx` — an editable file where text, bullets, and tables can be modified directly in PowerPoint or Google Slides.

### Custom output path

```bash
agentpreso render deck.md --format pdf --output ./exports/final.pdf
```

### Render with template variables

If your deck uses `{{variable}}` placeholders, supply values at render time:

```bash
agentpreso render proposal.md --format pdf --vars client-data.yaml
agentpreso render proposal.md --format pdf --var company="Contoso" --var deal_size="\$1.2M"
```

See [Use Template Variables](./template-variables.md) for details.

## Export from the API

### Render a stored deck

```bash
curl -X POST https://api.agentpreso.com/api/decks/DECK_ID/render \
  -H "Authorization: Bearer ap_..." \
  -H "Content-Type: application/json" \
  -d '{"format": "pdf"}'
```

Returns a presigned download URL:

```json
{
  "data": {
    "url": "https://storage.agentpreso.com/renders/abc123.pdf",
    "format": "pdf",
    "expiresAt": "2025-01-15T11:30:00Z"
  }
}
```

### Render raw markdown

Render without storing a deck first:

```bash
curl -X POST https://api.agentpreso.com/api/render \
  -H "Authorization: Bearer ap_..." \
  -H "Content-Type: application/json" \
  -d '{
    "markdown": "---\ntheme: minimal\n---\n\n# Slide 1\n\nContent",
    "format": "pdf",
    "themeId": "corporate"
  }'
```

### Render with variables via API

```json
{
  "markdown": "...",
  "format": "pdf",
  "vars": {
    "company": "Contoso Ltd",
    "revenue_data": [4.2, 5.1, 6.3, 7.8]
  }
}
```

## Export via MCP

Ask your AI agent:

> "Export my presentation as a PDF"

Or programmatically:

```json
{
  "tool": "render_deck",
  "arguments": {
    "deckId": "deck-abc123",
    "format": "pptx"
  }
}
```

The agent receives a download URL and can share it with the user.

## What to know about each format

### HTML

- Self-contained single file — works offline
- Interactive slide navigation (arrow keys, click)
- Smallest file size
- Best for web sharing and embedding

### PDF

- All slides rendered as vector graphics
- Charts and diagrams embedded at full quality
- Print-ready with correct page sizes (16:9)
- Theme colors, fonts, and layout preserved exactly
- Best for sharing, printing, and archiving

### PPTX (PowerPoint)

- **Text, bullets, and tables are editable** — recipients can modify content in PowerPoint or Google Slides
- Charts and diagrams are embedded as high-quality PNG images (not editable as native chart objects)
- Theme colors and fonts are applied to the PPTX theme
- Compatible with PowerPoint, Google Slides, Keynote, and LibreOffice Impress
- Best for handoff to non-technical collaborators who need to make edits
