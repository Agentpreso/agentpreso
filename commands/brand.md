---
description: Set up brand customization for presentations (colors, fonts, logo)
---

# Brand Setup

## Arguments

$ARGUMENTS may contain brand name, colors, website URL, or other preferences.

## Process

1. **Gather brand info**: Ask the user for:
   - Primary color (hex) — main brand color
   - Secondary color (optional)
   - Logo file (optional) — SVG preferred
   - Font preference (optional)
2. **If user doesn't have brand colors**, suggest based on tone:
   - Professional/corporate: Blues (#2563eb)
   - Energetic/startup: Oranges (#f97316)
   - Trustworthy/finance: Deep teal (#0f766e)
   - Creative/design: Purples (#7c3aed)
3. **Choose base theme**: Recommend a theme that works well with their colors
4. **Upload logo** (if provided):
   ```bash
   agentpreso assets upload logo.svg
   ```
5. **Generate frontmatter**: Create brand override configuration:
   ```yaml
   agentpreso:
     theme: glacier
     brand:
       --primary-color: "#hex"
       --secondary-color: "#hex"
       --font-heading: "Font, sans-serif"
   ```
6. **Create sample deck** to preview the brand
7. **Preview**: `agentpreso preview sample.md -s 1`
