# CLI Reference

The AgentPreso CLI is a standalone binary that works with local files and cloud storage. No Node.js required.

## Install

```bash
curl -fsSL https://agentpreso.com/install.sh | sh
```

## Global Options

| Option | Description |
|--------|-------------|
| `--help`, `-h` | Show help for a command |
| `--version`, `-v` | Show CLI version |
| `--quiet`, `-q` | Suppress non-error output |
| `--verbose` | Show detailed output |

## Authentication Commands

### `agentpreso login`

Authenticate with the AgentPreso server and store your API key locally.

```bash
agentpreso login
```

Opens a browser window for authentication. After successful login, your API key is stored in `~/.agentpreso/credentials`.

**Options:**

| Option | Description |
|--------|-------------|
| `--server <url>` | Use a custom server URL |
| `--key <api-key>` | Provide an API key directly (non-interactive) |

### `agentpreso logout`

Remove stored credentials.

```bash
agentpreso logout
```

### `agentpreso whoami`

Display the currently authenticated user and server.

```bash
agentpreso whoami
```

**Output:**

```
Logged in as: user@example.com
Server: https://api.agentpreso.com
```

## Deck Commands

### `agentpreso create <name>`

Create a new presentation from a theme.

```bash
agentpreso create quarterly-review
```

**Options:**

| Option | Description |
|--------|-------------|
| `--theme`, `-t` | Theme to use (default: `minimal`) |
| `--output`, `-o` | Output directory (default: current directory) |

**Examples:**

```bash
# Create with corporate theme
agentpreso create sales-deck --theme corporate

# Create in a specific directory
agentpreso create pitch --output ./presentations
```

### `agentpreso render <file>`

Render a presentation to HTML, PDF, or editable PowerPoint.

```bash
agentpreso render presentation.md
```

**Options:**

| Option | Description |
|--------|-------------|
| `--format`, `-f` | Output format: `html`, `pdf`, `pptx` (default: `html`) |
| `--output`, `-o` | Output file path |
| `--theme`, `-t` | Override theme from frontmatter |
| `--watch`, `-w` | Watch for changes and re-render |
| `--vars <file>` | Load template variables from a YAML or JSON file |
| `--var <key=value>` | Set a template variable (repeatable, overrides `--vars` file) |

**Examples:**

```bash
# Render to PDF
agentpreso render deck.md --format pdf

# Render to editable PowerPoint
agentpreso render deck.md --format pptx

# Custom output path
agentpreso render deck.md --format pdf --output ./output/final.pdf

# Watch mode
agentpreso render deck.md --watch

# Render with template variables from a file
agentpreso render proposal.md --vars client-data.yaml

# Render with inline variable overrides
agentpreso render proposal.md --var company="Contoso" --var deal_size="\$1.2M"

# Combine file + inline overrides (inline wins)
agentpreso render proposal.md --vars defaults.yaml --var company="Override"
```

**PPTX Export Notes:**

- PPTX exports produce **editable slides** -- text, bullets, and tables can be modified directly in PowerPoint
- Diagrams (Mermaid) and charts are embedded as high-quality PNG images
- Theme colors and fonts are applied to the PPTX theme
- Powered by Pandoc for reliable conversion

### `agentpreso serve <file>`

Start a local development server with hot-reload preview.

```bash
agentpreso serve presentation.md
```

**Options:**

| Option | Description |
|--------|-------------|
| `--port`, `-p` | Server port (default: `3000`) |
| `--host` | Host to bind to (default: `localhost`) |
| `--open` | Open browser automatically |

**Examples:**

```bash
# Custom port
agentpreso serve deck.md --port 8080

# Open browser automatically
agentpreso serve deck.md --open
```

### `agentpreso push [file]`

Upload a local deck to cloud storage.

```bash
agentpreso push presentation.md
```

If no file is specified, pushes all `.md` files in the current directory that have AgentPreso frontmatter.

**Options:**

| Option | Description |
|--------|-------------|
| `--slug` | Override the deck slug (default: filename) |
| `--force` | Overwrite existing deck without confirmation |

**Examples:**

```bash
# Push with custom slug
agentpreso push deck.md --slug q3-results

# Force overwrite
agentpreso push deck.md --force
```

### `agentpreso pull <slug>`

Download a cloud deck to a local file.

```bash
agentpreso pull quarterly-review
```

**Options:**

| Option | Description |
|--------|-------------|
| `--output`, `-o` | Output file path (default: `<slug>.md`) |
| `--force` | Overwrite existing local file |

**Examples:**

```bash
# Custom output path
agentpreso pull q3-results --output ./decks/q3.md
```

### `agentpreso list`

List your cloud decks.

```bash
agentpreso list
```

**Options:**

| Option | Description |
|--------|-------------|
| `--json` | Output as JSON |
| `--limit`, `-n` | Maximum number of results |

**Output:**

```
SLUG              TITLE                    UPDATED
quarterly-review  Q3 2024 Review           2 hours ago
sales-pitch       Enterprise Sales Deck    3 days ago
onboarding        New Hire Onboarding      1 week ago
```

### `agentpreso preview <file> -s <slide>`

Preview a single slide as PNG image.

## Theme Commands

### `agentpreso themes`

List available themes.

```bash
agentpreso themes
```

**Options:**

| Option | Description |
|--------|-------------|
| `--json` | Output as JSON |

### `agentpreso themes add <path>`

Upload a custom theme to your account.

```bash
agentpreso themes add ./my-theme/
```

The path should be a directory containing:
- `theme.yaml` - manifest file
- `overrides.css` - optional CSS overrides
- `scaffold.md` - optional starter content
- `assets/` - optional directory with images

**Logo Options:**

| Option | Description |
|--------|-------------|
| `--logo <file>` | Path to primary logo file |
| `--logo-light <file>` | Path to light variant logo (for dark backgrounds) |
| `--logo-position <pos>` | Logo position: `top-left`, `top-center`, `top-right`, `left-center`, `center`, `right-center`, `bottom-left`, `bottom-center`, `bottom-right`, `none` |
| `--logo-size <size>` | Logo size: `small`, `medium`, `large`, or `WIDTHxHEIGHT` (e.g., `80x60`) |
| `--logo-pages <pages>` | Which pages to show logo: `all`, `first`, `last`, `first-and-last`, `content` |
| `--logo-placement <file>` | Path to JSON file with advanced placement rules |
| `--logo-placement-json <json>` | Inline JSON with advanced placement rules |

**Examples:**

```bash
# Upload theme with logo
agentpreso themes add ./my-theme --logo ./assets/logo.png

# Upload with logo position and size
agentpreso themes add ./my-theme \
  --logo ./assets/logo.svg \
  --logo-position bottom-right \
  --logo-size small

# Upload with light variant for dark backgrounds
agentpreso themes add ./my-theme \
  --logo ./assets/logo-dark.png \
  --logo-light ./assets/logo-light.png

# Upload with advanced placement rules
agentpreso themes add ./my-theme \
  --logo ./assets/logo.png \
  --logo-placement-json '{"default":{"position":"bottom-right","size":"small"},"lead":{"position":"top-left","size":"large"}}'
```

### `agentpreso themes update <name>`

Update a custom theme's logo configuration.

```bash
agentpreso themes update my-brand --logo ./new-logo.png
```

**Logo Options:** Same as `themes add` above.

**Examples:**

```bash
# Update logo position
agentpreso themes update my-brand --logo-position top-left

# Update with new logo file and size
agentpreso themes update my-brand \
  --logo ./updated-logo.svg \
  --logo-size medium
```

### `agentpreso themes show <name>`

Show theme details including logo configuration.

```bash
agentpreso themes show my-brand
```

### `agentpreso themes rename <old-name> <new-name>`

Rename a custom theme.

```bash
agentpreso themes rename my-brand my-company-brand
```

### `agentpreso themes delete <name>`

Delete a custom theme.

```bash
agentpreso themes delete my-brand
```

## Asset Commands

### `agentpreso assets upload <file>`

Upload image for use in slides. Returns asset URI.

### `agentpreso assets`

List uploaded assets.

## Content Generation

### `agentpreso add-graphic <slug> "prompt"`

AI-generate image into deck.

### `agentpreso render-chart <file>`

Render chart YAML to SVG.

### `agentpreso render-diagram <file>`

Render Mermaid to SVG.

## Sharing

### `agentpreso share <slug>`

Generate public share link.

### `agentpreso share <slug> --private`

Revoke public access.

## Update

### `agentpreso update`

Check for and install CLI updates.

## Configuration Files

### `~/.agentpreso/config.yaml`

Global configuration:

```yaml
server:
  url: https://api.agentpreso.com
defaults:
  theme: minimal
  format: html
```

### `~/.agentpreso/credentials`

API key storage (do not commit to version control):

```yaml
api_key: ap_a1b2c3d4e5f6...
```

## Exit Codes

| Code | Description |
|------|-------------|
| `0` | Success |
| `1` | General error |
| `2` | Invalid arguments |
| `3` | Authentication required |
| `4` | Network error |
| `5` | File not found |
