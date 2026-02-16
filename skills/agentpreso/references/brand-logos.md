# Brand Logos

Add your logo to a theme so it appears automatically on every slide -- with control over position, size, and different variants for light and dark backgrounds.

## Quick Setup with the CLI

The simplest way to add a logo to a theme:

```bash
agentpreso themes add ./my-theme/ \
  --logo ./logo.svg \
  --logo-position bottom-right \
  --logo-size small
```

Or update an existing theme:

```bash
agentpreso themes update my-brand --logo ./logo.svg
```

## Light and Dark Variants

If your slides use both light and dark backgrounds, provide two logo versions:

```bash
agentpreso themes add ./my-theme/ \
  --logo ./logo-dark.svg \
  --logo-light ./logo-white.svg \
  --logo-position bottom-right \
  --logo-size medium
```

- **Primary logo** (`--logo`) -- for light backgrounds (typically a dark/colored logo)
- **Light variant** (`--logo-light`) -- for dark backgrounds (typically a white/light logo)

The `variant` property in placement rules controls which is used per slide type.

## Position Options

Logos can be placed in 9 positions:

```
+------------+------------+------------+
| top-left   | top-center | top-right  |
+------------+------------+------------+
| left-center|   center   |right-center|
+------------+------------+------------+
|bottom-left |bottom-center|bottom-right|
+------------+------------+------------+
```

Set via the CLI flag:

```bash
agentpreso themes update my-brand --logo-position top-left
```

**Recommended placements:**

| Slide type | Position | Why |
|------------|----------|-----|
| Content slides | `bottom-right` | Unobtrusive, professional standard |
| Title slides | `top-left` or `center` | Prominent brand presence |
| Section dividers | `none` or `bottom-center` | Clean, focused |
| Dark slides | Same position, `light` variant | Consistent placement |

## Size Options

**Preset sizes:**

| Size | Height |
|------|--------|
| `small` | 40px |
| `medium` | 80px |
| `large` | 120px |

**Custom dimensions:**

```bash
agentpreso themes add ./my-theme/ --logo ./logo.svg --logo-size 80x40
```

Width and height maintain aspect ratio if only one is specified.

## Page Filtering

Control which slides show the logo:

```bash
agentpreso themes add ./my-theme/ --logo ./logo.svg --logo-pages content
```

| Option | Shows logo on |
|--------|--------------|
| `all` | Every slide |
| `first` | First slide only |
| `last` | Last slide only |
| `first-and-last` | First and last slides |
| `content` | All slides except first and last |

## Advanced: Per-Slide-Type Rules

For fine-grained control, use a JSON placement configuration. Different slide types (based on their `_class` directive) get different logo behavior:

```json
{
  "default": {
    "position": "bottom-right",
    "size": "small",
    "opacity": 0.9,
    "margin": 16
  },
  "title-hero": {
    "position": "top-left",
    "size": "large",
    "margin": { "top": 40, "left": 60 }
  },
  "chapter": {
    "position": "bottom-center",
    "size": "medium",
    "opacity": 0.5
  },
  "quote": {
    "position": "none"
  },
  "full-bleed": {
    "position": "bottom-right",
    "size": "small",
    "variant": "light",
    "opacity": 0.9
  }
}
```

Apply via CLI:

```bash
# From a file
agentpreso themes add ./my-theme/ \
  --logo ./logo.svg \
  --logo-light ./logo-white.svg \
  --logo-placement ./logo-rules.json

# Inline
agentpreso themes update my-brand --logo-placement-json '{
  "default": {"position": "bottom-right", "size": "small"},
  "title-hero": {"position": "top-left", "size": "large"}
}'
```

### Placement Rule Properties

| Property | Type | Description |
|----------|------|-------------|
| `position` | string | One of the 9 positions, or `none` to hide |
| `size` | string or object | `small`, `medium`, `large`, or `{ "width": N, "height": N }` |
| `opacity` | number | 0.0 to 1.0 (default: 1.0) |
| `margin` | number or object | Pixels from edge -- single number or `{ "top", "right", "bottom", "left" }` |
| `variant` | string | `"default"` or `"light"` -- which logo asset to use |

The `default` rule is required. Other rules are optional overrides for specific slide classes.

## Set Up Logos via MCP

```json
{
  "name": "create_theme",
  "arguments": {
    "name": "my-brand",
    "css": "...",
    "logoAssetId": "asset_abc123",
    "logoLightAssetId": "asset_def456",
    "logoPlacement": "{\"default\":{\"position\":\"bottom-right\",\"size\":\"small\"},\"title-hero\":{\"position\":\"top-left\",\"size\":\"large\"}}"
  }
}
```

## Best Practices

- **Use SVG** for logos -- they render crisp at any size
- **Small (40px)** for content slides -- subtle, professional
- **Provide both variants** if your deck uses dark backgrounds or `full-bleed` layouts
- **Hide on quote slides** -- `"quote": { "position": "none" }` keeps the focus on the quote
- **Consistent margins** -- use the same margin value across all rules for alignment
