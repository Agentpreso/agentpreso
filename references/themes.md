# Themes

Themes control the visual appearance of your presentations - layouts, typography, colors, and branding. AgentPreso comes with five built-in themes and supports custom themes for your brand.

## Built-in Themes

### Minimal

Clean and simple with lots of whitespace. Perfect for technical talks and developer content.

- Light background with dark text
- Sans-serif typography (Inter)
- Subtle accents
- Focused layouts that don't distract from content

```markdown
---
marp: true
agentpreso:
  theme: minimal
---
```

### Dark

High contrast with a dark background. Great for presentations in dimly lit rooms or for a modern aesthetic.

- Dark background (#1a1a2e) with light text
- Monospace accent font (JetBrains Mono)
- Vibrant accent colors that pop
- Code blocks that blend naturally

```markdown
---
marp: true
agentpreso:
  theme: dark
---
```

### Corporate

Professional and structured. Ideal for business presentations, quarterly reviews, and client pitches.

- Muted blues and grays
- Well-defined table styles
- Multiple column layouts
- Logo and branding placeholders

```markdown
---
marp: true
agentpreso:
  theme: corporate
---
```

### Creative

Bold and modern. Perfect for marketing, product launches, and creative projects.

- Vibrant color palette
- Asymmetric layouts
- Large typography
- Dynamic visual hierarchy

```markdown
---
marp: true
agentpreso:
  theme: creative
---
```

### AgentPreso

The official AgentPreso brand theme with navy and tangerine accents on an ivory background.

- Navy primary (#1e3a5f) with tangerine accent (#fb923c)
- Warm ivory background (#fdf7ef)
- Clean, professional typography (Inter)
- Great for product demos and internal presentations

```markdown
---
marp: true
agentpreso:
  theme: agentpreso
---
```

## Theme Layouts

Each theme provides slide layouts that you activate with the `_class` directive:

```markdown
---

<!-- _class: lead -->

# Welcome

Subtitle goes here

---

<!-- _class: two-column -->

## Two Column Layout

::left::
Content on the left side

::right::
Content on the right side

---
```

### Common Layouts

| Layout | Description |
|--------|-------------|
| `lead` | Centered title slide, often with distinct background |
| `two-column` | Side-by-side content columns |
| `section` | Section divider with large heading |
| `image-right` | Content left, full-bleed image right |
| `image-left` | Full-bleed image left, content right |
| `quote` | Large centered blockquote |
| `comparison` | Two-column with headers for comparing options |

### Example: Section Divider

```markdown
---

<!-- _class: section -->

# Part Two
## Getting Started

---
```

### Example: Image Layout

```markdown
---

<!-- _class: image-right -->

## Our Team

We're a distributed team of engineers,
designers, and product people building
the future of presentations.

![Team photo](asset://team-photo)

---
```

## Brand Customization

Override theme defaults with your brand colors and fonts using the `brand` object in frontmatter:

```markdown
---
marp: true
agentpreso:
  theme: corporate
  brand:
    --primary-color: "#dc2626"
    --secondary-color: "#f59e0b"
    --font-heading: "Georgia, serif"
    --font-body: "Helvetica, sans-serif"
    logo: asset://company-logo
---
```

### Available CSS Variables

Themes expose these CSS custom properties for customization:

| Variable | Description | Default (Corporate) |
|----------|-------------|---------------------|
| `--primary-color` | Main brand color | `#1e40af` |
| `--secondary-color` | Secondary/muted color | `#6b7280` |
| `--accent-color` | Highlights and links | `#2563eb` |
| `--bg-color` | Slide background | `#ffffff` |
| `--text-color` | Body text | `#1f2937` |
| `--font-heading` | Heading font family | `Inter, sans-serif` |
| `--font-body` | Body font family | `Inter, sans-serif` |
| `--font-code` | Code font family | `JetBrains Mono, monospace` |

## Creating Custom Themes

Custom themes let you build a complete visual system for your organization.

### Theme Structure

A theme is a directory with these files:

```
my-theme/
├── theme.yaml          # Manifest with metadata and declarations
├── overrides.css       # Optional CSS overrides
├── scaffold.md         # Starter deck showing all layouts
└── assets/             # Optional logos, backgrounds, icons
    ├── logo.svg
    └── bg-pattern.png
```

### theme.yaml

The manifest declares your theme's identity, fonts, colors, and style parameters:

```yaml
meta:
  name: my-brand
  description: Company branding with our colors and logo
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
  dark:  # Optional dark mode palette
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

### Manifest sections

| Section | Required | Description |
|---------|----------|-------------|
| `meta` | Yes | Name, description, version |
| `fonts` | Yes | Heading, body, code font families + metrics |
| `colors` | Yes | Light palette (required) + dark palette (optional). Each needs: `primary`, `secondary`, `accent`, `bg`, `text`, `muted` |
| `style` | Yes | Visual params: border radius, density, heading style, accent style |
| `imagery` | No | AI image generation style guidance |
| `logo` | No | Default logo placement |

### overrides.css

Optional CSS overrides for advanced customization beyond variables:

```css
/* Override specific styles beyond what variables provide */

/* Custom lead slide background gradient */
section.lead {
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
}

/* Custom table header styling */
section th {
  background: var(--primary-color);
  color: white;
  padding: 12px 16px;
  text-align: left;
}
```

### scaffold.md

A starter deck that demonstrates all available layouts:

```markdown
---
marp: true
agentpreso:
  theme: my-brand
paginate: true
---

<!-- _class: lead -->

# Presentation Title

Subtitle or tagline

**Your Name** - Date

---

## Regular Slide

This is a standard content slide with body text.

- Bullet point one
- Bullet point two
- Bullet point three

---

<!-- _class: two-column -->

## Two Column Layout

::left::

Content on the left side of the slide.

::right::

Content on the right side of the slide.

---

<!-- _class: section -->

# Section Title

A new section begins

---

## Table Example

| Feature | Free | Pro |
|---------|------|-----|
| Decks | 5 | Unlimited |
| Themes | 5 | All |
| Renders | 10/mo | 100/mo |

---

## Questions?

Contact us at hello@example.com
```

### Uploading Your Theme

Use the CLI to upload your custom theme:

```bash
agentpreso themes add ./my-theme/
```

Or upload via the API:

```bash
curl -X POST https://api.agentpreso.com/api/themes \
  -H "Authorization: Bearer ap_..." \
  -F "manifest=@my-theme/theme.yaml" \
  -F "css=@my-theme/overrides.css" \
  -F "scaffold=@my-theme/scaffold.md" \
  -F "assets=@my-theme/assets/logo.svg"
```

Once uploaded, use your theme in any presentation:

```markdown
---
marp: true
agentpreso:
  theme: my-brand
---
```

## Theme Logos

Themes can include automatic logo placement that applies your logo consistently across all slides. See the [Theme Logos guide](./theme-logos.md) for:

- Position and size options
- Light/dark variants for different backgrounds
- Per-slide-type rules (title, content, section slides)
- CLI and API examples

## Per-Slide Dark Mode (Invert)

Any slide can be flipped to a dark palette using the `invert` class:

```markdown
---

<!-- _class: invert -->

## Dark Slide

This slide renders with a dark background and light text.

---
```

### How it works

Themes can define both a `colors.light` and `colors.dark` palette in their manifest. When a slide has `_class: invert`, the dark palette is applied to that slide:

```yaml
colors:
  light:
    primary: "#0066cc"
    secondary: "#333333"
    accent: "#ff6600"
    bg: "#ffffff"
    text: "#222222"
    muted: "#666666"
  dark:
    primary: "#66b3ff"
    secondary: "#cccccc"
    accent: "#ff9933"
    bg: "#1a1a2e"
    text: "#f0f0f0"
    muted: "#888888"
```

If a theme does not define `colors.dark`, the `invert` class falls back to CSS `filter: invert(1)` for basic dark mode support.

### Embedded content adapts automatically

Charts, Mermaid diagrams, Excalidraw drawings, and AI-generated images detect the slide's background mode and render with appropriate colors. No additional configuration is needed — place content on an inverted slide and it adapts.

### Combining with layouts

The `invert` class works alongside any layout class:

```markdown
<!-- _class: invert title-hero -->

# Dark Title Slide
```

## Theme Resolution

When rendering, AgentPreso resolves themes in this order:

1. User's custom themes (by name)
2. Built-in themes (by name)

If a theme isn't found, rendering falls back to `minimal`.
