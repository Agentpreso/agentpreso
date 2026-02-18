# How to Create a Custom Theme

Create a custom theme to apply your organization's visual identity — colors, fonts, logo, and layout styling — to every presentation.

## What you'll need

- The AgentPreso CLI installed and authenticated
- Your brand colors (hex values), fonts, and logo file (SVG or PNG)

## 1. Create the theme directory

```bash
mkdir my-brand
```

A theme directory needs these files:

```
my-brand/
├── theme.yaml      # Required: metadata, fonts, colors, style params
├── overrides.css   # Optional: CSS escape hatch for custom styling
└── scaffold.md     # Optional: sample deck showing all layouts
```

## 2. Write the manifest (`theme.yaml`)

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
  dark:  # Optional — omit if no dark mode
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
```

### Manifest sections

| Section | Required | Description |
|---------|----------|-------------|
| `meta` | Yes | Name, description, version |
| `fonts` | Yes | Heading, body, code font families. `metrics.bodyAvgCharWidthRatio` powers the text fitting system |
| `colors` | Yes | Light palette required, dark palette optional. Each palette needs 6 required colors: `primary`, `secondary`, `accent`, `bg`, `text`, `muted`. Plus 8 optional derived colors |
| `style` | Yes | Border radius (`sharp` / `rounded` / `pill`), density (`compact` / `comfortable` / `spacious`), heading style (`normal` / `uppercase`), accent style (`solid` / `gradient`) |

## 3. Write overrides CSS (optional)

For styling that goes beyond what `theme.yaml` variables provide, add an `overrides.css` file:

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

Use `!important` on `display` and `padding` properties in layout classes — this is required to override Marpit's scaffold styles.

## 4. Write a scaffold deck (optional)

A `scaffold.md` gives users a starting point when they create a deck with your theme:

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

**Your Name** — Date

---

<!-- _class: bullets -->

## Agenda

- First topic
- Second topic
- Third topic

---

<!-- _class: two-col -->

## Two Columns

::: left
Content on the left side.
:::

::: right
Content on the right side.
:::

---

<!-- _class: summary -->

## Key Takeaways

- First takeaway
- Second takeaway
- Third takeaway
```

## 5. Upload the theme

```bash
agentpreso themes add ./my-brand/
```

You should see:

```
Uploaded theme: my-brand
```

To upload with a logo, add logo flags:

```bash
agentpreso themes add ./my-brand/ \
  --logo ./my-brand/assets/logo.svg \
  --logo-position bottom-right \
  --logo-size small
```

See [Set Up Brand Logos](./brand-logos.md) for full logo configuration.

## 6. Use your theme

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

## Updating a theme

Update a theme by pointing to the `theme.yaml` file. This re-assembles CSS from the manifest and auto-discovers `overrides.css` and logo files from the same directory:

```bash
agentpreso themes update my-brand ./my-theme/theme.yaml
```

You can also update just the CSS or logo independently:

```bash
agentpreso themes update my-brand --css ./overrides.css
agentpreso themes update my-brand --logo ./new-logo.png
```

## Deleting a theme

```bash
agentpreso themes delete my-brand
```

Built-in themes cannot be deleted.
