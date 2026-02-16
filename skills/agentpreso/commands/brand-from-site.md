---
description: Extract brand identity from a company website to create AgentPreso brand settings
---

# Extract Brand from Website

## Arguments

$ARGUMENTS should contain the company website URL.

## Process

1. **Fetch the website**: Use web fetch to retrieve the homepage
2. **Extract colors**: Look for:
   - CSS custom properties (--primary-color, --brand-color, etc.)
   - Button background colors
   - Link colors, header/nav colors
   - Identify primary, secondary, accent, text, and background colors
3. **Extract logo**: Look in header for images with "logo" in filename/alt, prefer SVG
4. **Identify fonts**: Check Google Fonts links, @font-face declarations, CSS font-family on body and headings
5. **Recommend theme**: Match the website's aesthetic:
   - Dark website → neon or terminal
   - Corporate/formal → glacier or maison
   - Colorful/bold → ember or botanica
   - Clean/minimal → agentpreso or ink
6. **Present findings**: Show extracted colors, fonts, logo URL in a summary table
7. **Generate configuration**: Create the `agentpreso.brand` frontmatter block
8. **Guide logo upload**: If logo found, instruct user to download and upload via `agentpreso assets upload`
