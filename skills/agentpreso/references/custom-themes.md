# Custom Themes

Create a custom theme to apply your organization's visual identity -- colors, fonts, logo, and layout styling -- to every presentation.

## What You'll Need

- The AgentPreso CLI installed and authenticated
- Your brand colors (hex values), fonts, and logo file (SVG or PNG)

## Theme Directory Structure

```
my-brand/
├── theme.yaml      # Required: metadata, fonts, colors, style params
├── overrides.css   # Optional: CSS escape hatch for custom styling
└── scaffold.md     # Optional: sample deck showing all layouts
```

## theme.yaml Manifest

The manifest declares your theme's metadata, fonts, colors, and style parameters:

```yaml
meta:
  name: my-brand
  description: Acme Corp brand theme
  version: 1.0.0

fonts:
  heading: "'Montserrat', sans-serif"
  body: "'Open Sans', sans-serif"
  code: "'Fira Code', monospace"
  metrics:
    bodyAvgCharWidthRatio: 0.45  # Used by text fitting system

colors:
  light:
    primary: "#0066cc"
    secondary: "#333333"
    accent: "#ff6600"
    bg: "#ffffff"
    text: "#222222"
    muted: "#666666"
    # Optional derived colors (inherit from core if omitted):
    # heading, subheading, border, codeBg, inlineCodeBg, heroBg, heroText, chapterBg
  dark:  # Optional -- omit if no dark mode
    primary: "#66b3ff"
    secondary: "#cccccc"
    accent: "#ff9933"
    bg: "#1a1a2e"
    text: "#f0f0f0"
    muted: "#888888"

style:
  radius: rounded       # sharp | rounded | pill
  density: comfortable  # compact | comfortable | spacious
  headingStyle: normal  # normal | uppercase
  accentStyle: solid    # solid | gradient

# Optional: AI image generation guidance
imagery:
  style: "flat illustration"
  guidance: "Use brand colors, clean lines"
  palette: theme  # "theme" or list of hex colors

# Optional: default logo placement
logo:
  placement: bottom-right  # top-left | top-right | bottom-left | bottom-right
  maxHeight: "40px"
```

### Manifest Sections

| Section | Required | Description |
|---------|----------|-------------|
| `meta` | Yes | Name, description, version |
| `fonts` | Yes | Heading, body, code font families. `metrics.bodyAvgCharWidthRatio` powers the text fitting system |
| `colors` | Yes | Light palette required, dark palette optional. Each palette needs 6 required colors: `primary`, `secondary`, `accent`, `bg`, `text`, `muted`. Plus 8 optional derived colors |
| `style` | Yes | Border radius (`sharp` / `rounded` / `pill`), density (`compact` / `comfortable` / `spacious`), heading style (`normal` / `uppercase`), accent style (`solid` / `gradient`) |
| `imagery` | No | AI image generation style guidance |
| `logo` | No | Default logo placement |

## overrides.css

Optional CSS overrides for styling beyond what `theme.yaml` variables provide:

```css
/* Custom lead slide background gradient */
section.title-hero {
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
}

/* Custom table header styling */
section th {
  background: var(--primary-color);
  color: white;
  padding: 12px 16px;
  text-align: left;
}

/* Custom blockquote styling */
section.quote blockquote {
  border: none;
  font-size: 1.4em;
  font-style: italic;
  color: var(--secondary-color);
  max-width: 80%;
}
```

Use `!important` on `display` and `padding` properties in layout classes -- this is required to override Marpit's scaffold styles.

## scaffold.md

A starter deck that demonstrates all available layouts:

```markdown
---
marp: true
agentpreso:
  theme: my-brand
paginate: true
---

<!-- _class: title-hero -->

# Presentation Title

Subtitle or tagline

**Your Name** -- Date

---

<!-- _class: bullets -->

## Agenda

- First topic
- Second topic
- Third topic

---

<!-- _class: two-col -->

## Two Columns

::left::
Content on the left side.

::right::
Content on the right side.

---

<!-- _class: summary -->

## Key Takeaways

- First takeaway
- Second takeaway
- Third takeaway
```

## Upload the Theme

```bash
agentpreso themes add ./my-brand/
```

To upload with a logo, add logo flags:

```bash
agentpreso themes add ./my-brand/ \
  --logo ./my-brand/assets/logo.svg \
  --logo-position bottom-right \
  --logo-size small
```

See [./brand-logos.md](./brand-logos.md) for full logo configuration.

## Use Your Theme

Create a new deck with your theme:

```bash
agentpreso create my-deck --theme my-brand
```

Or set it in any deck's frontmatter:

```markdown
---
marp: true
agentpreso:
  theme: my-brand
---
```

## Updating a Theme

After uploading, update the CSS or logo:

```bash
agentpreso themes update my-brand --logo ./new-logo.png
```

## Deleting a Theme

```bash
agentpreso themes delete my-brand
```

Built-in themes cannot be deleted.
