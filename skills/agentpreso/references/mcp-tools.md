# MCP Tools Reference

AgentPreso exposes a Model Context Protocol (MCP) endpoint that AI agents use to create, edit, and manage presentations programmatically.

## Endpoint

```
https://api.agentpreso.com/mcp
```

Transport: **Streamable HTTP**

## Authentication

Include your API key in the MCP client headers:

```json
{
  "mcpServers": {
    "agentpreso": {
      "url": "https://api.agentpreso.com/mcp",
      "headers": {
        "Authorization": "Bearer ap_your_api_key_here"
      }
    }
  }
}
```

**Claude Desktop config paths:**

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

## Theme Tools

### `list_themes`

Browse available presentation themes.

**Parameters:** None

**Returns:**

```json
{
  "themes": [
    {
      "id": "minimal",
      "name": "minimal",
      "description": "Clean, lots of whitespace",
      "layouts": ["title-hero", "bullets", "two-col", "chapter", "quote", "summary"]
    }
  ]
}
```

**Example conversation:**

> "What themes are available?"

---

### `create_theme`

Create a new custom presentation theme with optional logo configuration.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | Yes | Theme name (must be unique) |
| `css` | string | Yes | CSS content defining theme styles |
| `description` | string | No | Human-readable description |
| `manifest` | string | No | JSON manifest with metadata |
| `logoAssetId` | string | No | Asset ID of primary logo |
| `logoLightAssetId` | string | No | Asset ID of light logo variant |
| `logoPlacement` | string | No | JSON string with placement rules |

**Logo placement JSON format:**

```json
{
  "default": { "position": "bottom-right", "size": "small" },
  "title-hero": { "position": "top-left", "size": "large" },
  "full-bleed": { "position": "bottom-right", "size": "small", "variant": "light" }
}
```

**Position values:** `top-left`, `top-center`, `top-right`, `left-center`, `center`, `right-center`, `bottom-left`, `bottom-center`, `bottom-right`, `none`

**Size values:** `small` (40px), `medium` (80px), `large` (120px), or `{ "width": N, "height": N }`

**Returns:**

```json
{
  "id": "tmpl_abc123",
  "name": "my-brand",
  "created": true
}
```

**Example conversation:**

> "Create a theme called 'my-brand' with our company logo in the bottom-right corner."

---

### `update_theme`

Update a custom theme's properties including logo configuration.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | Yes | Current theme name |
| `newName` | string | No | New name for the theme |
| `description` | string | No | New description |
| `css` | string | No | New CSS content |
| `logoAssetId` | string/null | No | New logo asset ID, or null to remove |
| `logoLightAssetId` | string/null | No | New light logo asset ID, or null to remove |
| `logoPlacement` | string/null | No | New placement rules JSON, or null to remove |

**Returns:**

```json
{
  "id": "tmpl_abc123",
  "name": "my-brand",
  "updated": true
}
```

**Example conversation:**

> "Update the my-brand theme to put the logo in the top-left corner."

---

### `delete_theme`

Delete a custom theme. Cannot delete built-in themes.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | Yes | Name of theme to delete |

**Returns:**

```json
{
  "name": "my-brand",
  "deleted": true
}
```

**Example conversation:**

> "Delete the my-brand theme."

---

## Deck Tools

### `create_deck`

Create a new presentation in cloud storage.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `slug` | string | Yes | URL-friendly identifier |
| `title` | string | No | Display title |
| `markdown` | string | Yes | Full markdown content |
| `themeId` | string | No | Theme to use (default: `minimal`) |

**Returns:**

```json
{
  "id": "deck_abc123",
  "slug": "my-presentation",
  "title": "My Presentation"
}
```

---

### `get_deck`

Retrieve a deck's full content.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | No | Deck ID |
| `slug` | string | No | Deck slug |

One of `id` or `slug` must be provided.

**Returns:**

```json
{
  "id": "deck_abc123",
  "slug": "my-presentation",
  "title": "My Presentation",
  "markdown": "---\nmarp: true\n...",
  "themeId": "minimal"
}
```

---

### `update_deck`

Replace the entire deck content.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Deck ID |
| `markdown` | string | Yes | New markdown content |
| `title` | string | No | New title |
| `themeId` | string | No | New theme |

**Returns:**

```json
{
  "id": "deck_abc123",
  "updated": true
}
```

---

### `edit_slide`

Modify a single slide by index.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `deckId` | string | Yes | Deck ID |
| `slideIndex` | number | Yes | 0-based slide index |
| `content` | string | Yes | New slide content |

**Returns:**

```json
{
  "deckId": "deck_abc123",
  "slideIndex": 2,
  "updated": true
}
```

---

### `add_slide`

Insert a new slide at a specific position.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `deckId` | string | Yes | Deck ID |
| `position` | number | Yes | Insert position (0-based) |
| `content` | string | Yes | Slide content |

**Returns:**

```json
{
  "deckId": "deck_abc123",
  "position": 3,
  "totalSlides": 8
}
```

---

### `remove_slide`

Delete a slide by index.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `deckId` | string | Yes | Deck ID |
| `slideIndex` | number | Yes | 0-based slide index |

**Returns:**

```json
{
  "deckId": "deck_abc123",
  "removed": true,
  "totalSlides": 6
}
```

---

### `apply_theme`

Change the theme for a deck.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `deckId` | string | Yes | Deck ID |
| `themeId` | string | Yes | New theme ID |

**Returns:**

```json
{
  "deckId": "deck_abc123",
  "themeId": "corporate",
  "applied": true
}
```

**Example conversation:**

> "Switch this presentation to use the corporate theme."

---

### `render_deck`

Export a deck to HTML, PDF, or editable PowerPoint.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `deckId` | string | Yes | Deck ID |
| `format` | string | Yes | `html`, `pdf`, or `pptx` |
| `vars` | object | No | Variables to substitute `{{key}}` placeholders |

**Returns:**

```json
{
  "url": "https://storage.agentpreso.com/renders/abc123.pdf",
  "format": "pdf",
  "expiresAt": "2024-01-15T12:00:00Z"
}
```

**PPTX Format Notes:**

- PPTX exports produce **editable slides** -- text, bullets, and tables can be modified directly in PowerPoint
- Diagrams and charts are embedded as high-quality PNG images
- Theme colors and fonts are applied to the PPTX theme

**Example conversation:**

> "Export my presentation as a PDF."
> "Give me an editable PowerPoint version."

---

### `preview_deck`

Open an interactive slide viewer/editor.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `deckId` | string | Yes | Deck ID |

**Returns:**

This tool returns a UI resource that renders an interactive presenter in the MCP client:

```json
{
  "content": [{ "type": "text", "text": "Opening presenter..." }],
  "_meta": {
    "ui": { "resourceUri": "ui://agentpreso/presenter" }
  }
}
```

The presenter UI allows:
- Slide-by-slide navigation
- Theme switching
- Live editing with instant preview
- Export actions

**Example conversation:**

> "Open a preview of my presentation."

---

### `list_decks`

List all presentations in your account.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `limit` | number | No | Max results (default: 20) |
| `offset` | number | No | Pagination offset |

**Returns:**

```json
{
  "decks": [
    {
      "id": "deck_abc123",
      "slug": "quarterly-review",
      "title": "Q3 2024 Review",
      "updatedAt": "2024-01-15T14:22:00Z"
    }
  ],
  "total": 15
}
```

---

## Asset Tools

### `upload_asset`

Upload an image or other file for use in presentations.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `filename` | string | Yes | Filename with extension |
| `content` | string | Yes | Base64-encoded file content |
| `mimeType` | string | Yes | MIME type (e.g., `image/png`) |

**Returns:**

```json
{
  "id": "asset_xyz789",
  "uri": "asset://asset_xyz789",
  "filename": "logo.png"
}
```

Use the returned URI in markdown: `![Logo](asset://asset_xyz789)`

---

## Example Workflows

### Creating a Complete Presentation

1. User: "Create a presentation about our new product launch"
2. Agent uses `list_themes` to show options
3. User: "Use the corporate theme"
4. Agent uses `create_deck` with generated content
5. User: "Add a slide with a comparison table"
6. Agent uses `add_slide` to insert new content
7. User: "Preview it"
8. Agent uses `preview_deck` to open the viewer
9. User: "Export as PDF"
10. Agent uses `render_deck` and provides download link

### Editing an Existing Presentation

1. User: "Open my quarterly review presentation"
2. Agent uses `get_deck` with slug `quarterly-review`
3. User: "Update the revenue numbers on slide 3"
4. Agent uses `edit_slide` with new content
5. User: "Change to the dark theme"
6. Agent uses `apply_theme`
7. User: "Show me the preview"
8. Agent uses `preview_deck`

## Error Handling

MCP tools return standard JSON-RPC errors:

```json
{
  "error": {
    "code": -32602,
    "message": "Deck not found",
    "data": {
      "deckId": "deck_invalid"
    }
  }
}
```

Common error codes:

| Code | Description |
|------|-------------|
| `-32600` | Invalid request |
| `-32601` | Method not found |
| `-32602` | Invalid params |
| `-32603` | Internal error |
