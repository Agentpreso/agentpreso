# Themes

Themes control the visual appearance of your presentations -- layouts, typography, colors, and branding. AgentPreso comes with 10 built-in themes and supports custom themes for your brand.

## Built-in Themes

### agentpreso

Official AgentPreso brand theme with Geist font and Navy/Tangerine colors.

- Navy primary (#1e3a5f) with tangerine accent (#fb923c)
- Warm ivory background (#fdf7ef)
- Clean, professional typography (Geist)
- Rounded corners, comfortable density
- Best for: product demos, internal presentations

```markdown
---
marp: true
agentpreso:
  theme: agentpreso
---
```

### blueprint

Engineering theme with grid overlay, blueprint-blue backgrounds, and technical precision.

- Deep engineering blue background (#1e3a5c) with light text (#c8d6e5)
- Yellow accent (#fbbf24) for emphasis
- Monospace headings (Space Mono), sharp corners, uppercase heading style
- Grid overlay, numeric table alignment
- Best for: technical architecture, engineering reviews, system design

```markdown
---
marp: true
agentpreso:
  theme: blueprint
---
```

### botanica

Nature-inspired theme with forest greens, gold accents, and elegant serif headings.

- Forest green primary (#2d5016) with gold accent (#c9952b)
- Warm parchment background (#f7f3eb)
- Serif headings (DM Serif Display), botanical illustration style
- Dark mode palette available
- Best for: sustainability, education, natural products, organic brands

```markdown
---
marp: true
agentpreso:
  theme: botanica
---
```

### chalk

Educational theme with handwriting headings, friendly colors, and hand-drawn feel.

- Charcoal primary (#2d3436) with teal accent (#00b894)
- Near-white background (#fefefe)
- Handwritten headings (Caveat), friendly body text (Nunito)
- Checkmark list markers, dashed borders
- Best for: workshops, tutorials, educational content, informal talks

```markdown
---
marp: true
agentpreso:
  theme: chalk
---
```

### ember

Cinematic keynote theme with warm gradients, dramatic typography on dark backgrounds.

- Dark chocolate background (#1c1210) with orange accent (#f97316)
- Warm copper secondary (#d4a574), gradient accents
- Bold headings (Sora) with text glow effects
- Best for: product launches, keynotes, startup pitches, high-impact talks

```markdown
---
marp: true
agentpreso:
  theme: ember
---
```

### glacier

Data-focused theme with IBM Plex, cool blues, and enhanced table styling.

- Cool blue-gray background (#f0f4f8) with navy text (#1b2a4a)
- Cyan accent (#0891b2), sharp corners
- IBM Plex font family throughout, striped/bordered tables
- Numeric table alignment, stat numbers in monospace
- Best for: data presentations, quarterly reports, analytics, financial reviews

```markdown
---
marp: true
agentpreso:
  theme: glacier
---
```

### ink

Editorial theme with serif typography, sharp lines, and newspaper-red accent.

- Near-black primary (#1a1a1a) on warm white (#faf9f6)
- Red accent (#c0392b) for editorial emphasis
- Serif headings (Playfair Display), serif body (Source Serif 4)
- Drop caps, bordered headings, high contrast
- Best for: thought leadership, editorial content, long-form narratives

```markdown
---
marp: true
agentpreso:
  theme: ink
---
```

### maison

Luxury minimalist theme with extreme restraint, confident whitespace, and matte gold.

- Pure black on white with matte gold accent (#b8960c)
- Elegant serif headings (Cormorant Garamond), light weight (300)
- Uppercase headings with wide letter spacing
- Generous margins, hairline rules, dash list markers
- Best for: luxury brands, executive summaries, investor presentations

```markdown
---
marp: true
agentpreso:
  theme: maison
---
```

### neon

Electric startup theme with cyan glow on near-black, gradient accents.

- Near-black background (#0a0a0f) with electric cyan accent (#00e5ff)
- Text glow effects, gradient accents
- Modern headings (Space Grotesk), rounded corners
- Radial gradient hero backgrounds
- Best for: tech launches, developer conferences, startup pitches, gaming

```markdown
---
marp: true
agentpreso:
  theme: neon
---
```

### terminal

Retro terminal theme with CRT aesthetic, monospace everything, green-on-black.

- Black background (#0d0d0d) with phosphor green text (#00dd35)
- Amber accent (#ffb000), sharp corners
- All monospace (JetBrains Mono), CRT scanlines, cursor blink
- Prompt-style list markers, outline code blocks
- Best for: developer talks, CLI demos, hacker culture, retro aesthetics

```markdown
---
marp: true
agentpreso:
  theme: terminal
---
```

## CSS Variables

Themes expose these CSS custom properties for customization:

| Variable | Description | Example |
|----------|-------------|---------|
| `--primary-color` | Main brand color | `#1e40af` |
| `--secondary-color` | Secondary/muted color | `#6b7280` |
| `--accent-color` | Highlights and links | `#2563eb` |
| `--bg-color` | Slide background | `#ffffff` |
| `--text-color` | Body text | `#1f2937` |
| `--font-heading` | Heading font family | `Inter, sans-serif` |
| `--font-body` | Body font family | `Inter, sans-serif` |
| `--font-code` | Code font family | `JetBrains Mono, monospace` |

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

## Dark Mode with `invert`

Any slide can be flipped to a dark palette using the `invert` class:

```markdown
---

<!-- _class: invert -->

## Dark Slide

This slide renders with a dark background and light text.

---
```

### How it works

Themes that define both `colors.light` and `colors.dark` palettes in their manifest apply the dark palette when `_class: invert` is present. If a theme does not define `colors.dark`, `invert` falls back to CSS `filter: invert(1)`.

### Combining with layouts

The `invert` class works alongside any layout class:

```markdown
<!-- _class: invert title-hero -->

# Dark Title Slide
```

Embedded content (charts, diagrams, generated images) automatically adapts to the slide's background mode.

## Theme Resolution Order

When rendering, AgentPreso resolves themes in this order:

1. User's custom themes (by name)
2. Built-in themes (by name)
3. Falls back to `minimal` if not found
