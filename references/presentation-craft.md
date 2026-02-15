# Presentation Craft

Principles for building world-class slide decks. These guidelines apply to any presentation tool but include specific advice for getting the most out of AgentPreso.

## Core Principles

1. **One Idea Per Slide** -- if you need "and" to describe the slide's purpose, split it into two slides.
2. **Signal-to-Noise Ratio** -- every element on the slide earns its place. White space is a feature, not wasted real estate.
3. **Progressive Disclosure** -- build complexity gradually across slides. Don't front-load information.
4. **3-Second Test** -- the audience should grasp the slide's main point within 3 seconds of seeing it.

## Typography Rules

- **Titles**: one line, action-oriented. Write "Revenue grew 40%" not just "Revenue".
- **Body**: maximum 3-5 bullet points per slide.
- **Bullets**: maximum 7 words each. Use phrases, not sentences.
- **Hierarchy**: use heading levels consistently. H2 for slide titles, H3 for section labels within a slide.

## Color Usage

- Use your primary color for emphasis only -- overusing it dilutes its impact.
- Limit to 2-3 colors per slide. More creates visual noise.
- Assign consistent meaning to colors (green = positive, red = concern, accent = key point).
- Let the theme handle color decisions. Override only when you have a specific reason.

## Content Types and Layout Guidance

### Data Slides
- One chart per slide. If you need two charts, use two slides.
- The title should state the insight, not describe the data: "Revenue grew 40%" not "Revenue by Quarter".
- Remove chart junk: gridlines, excessive labels, decorative elements.
- Use the `stats-grid` layout for headline numbers, `two-col` for chart + commentary.

### Text Slides
- Headlines, not sentences. The slide is a visual aid, not a document.
- Parallel structure in bullet lists (all start with verbs, or all are noun phrases).
- Use the `bullets` layout for standard content, `focus` for a single key message.

### Comparison Slides
- Two-column layout with visual balance between sides.
- Keep the same number of points on each side.
- Use `two-col` for equal comparisons, `two-col-wide-right` when one side has a diagram or chart.

### Flow and Process Slides
- Use Mermaid diagrams over text descriptions of processes.
- Keep diagrams to 5-7 nodes maximum. More than that belongs on multiple slides.
- Use the `steps` layout for linear sequences.

## Narrative Structure

### Opening (10% of slides)
- **Hook**: a surprising fact, bold statement, or compelling question.
- **Context**: briefly frame the problem or opportunity.
- **Preview**: what the audience will learn or decide by the end.
- Use `title-hero` for the hook, `focus` for the key question.

### Body (80% of slides)
- Follow the arc: **Problem** then **Analysis** then **Solution**.
- Each section starts with a `chapter` slide as a clear signpost.
- Alternate between data slides and text slides to maintain engagement.
- Place `quote` slides strategically for social proof or emphasis.

### Closing (10% of slides)
- **Summarize**: maximum 3 takeaways on a `summary` slide.
- **Call to action**: one clear next step. Be specific ("Schedule a pilot by Friday" not "Let's discuss").
- End memorably. The last slide should not be "Any questions?" -- make it a strong closing statement or your call to action.

## Common Anti-Patterns

| Anti-Pattern | Fix |
|-------------|-----|
| Wall of text | Move details to speaker notes; show only key phrases on screen |
| Clip art and stock photos | Use theme-appropriate generated images or clean diagrams |
| Reading slides verbatim | Slides are visual anchors; speaker notes carry the detail |
| "Any questions?" as final slide | End with a clear call to action or memorable closing statement |
| Every slide looks the same | Vary layouts: mix `bullets`, `two-col`, `stats-grid`, `img-right` |
| Too many fonts/colors | Let the theme enforce consistency; avoid scoped style overrides |
| Data without insight | Title every chart with the takeaway, not the metric name |

## AgentPreso-Specific Tips

### Theme Selection Guide

| Audience | Recommended Themes |
|----------|-------------------|
| Board / executives | `maison`, `glacier`, `ink` |
| Engineering team | `blueprint`, `terminal`, `neon` |
| Sales / clients | `agentpreso`, `ember`, `glacier` |
| Education / workshops | `chalk`, `botanica` |
| Creative / marketing | `ember`, `neon`, `ink` |
| All-purpose / safe default | `agentpreso`, `glacier` |

### Layout Selection Guide

| Content | Layout |
|---------|--------|
| Opening slide | `title-hero` |
| Section divider | `chapter` |
| Key message | `focus` |
| Bullet points | `bullets` |
| Process / steps | `steps` |
| KPI dashboard | `stats-grid` |
| Side-by-side comparison | `two-col` |
| Diagram + explanation | `two-col-wide-right` |
| Pricing / three options | `three-col` |
| Image + text | `img-right` or `img-left` |
| Full-screen visual | `full-bleed` |
| Testimonial | `quote` |
| Final takeaways | `summary` |

### Charts vs Tables

| Use Charts When | Use Tables When |
|-----------------|-----------------|
| Showing trends over time | Showing precise values |
| Comparing proportions | Readers need to look up specific numbers |
| Highlighting outliers | Fewer than 6 data points |
| Audience sees the slide briefly | Audience will study the slide |

### Diagram Complexity

- **5-7 nodes maximum** per diagram. If your flowchart has 15 nodes, split it across slides.
- Use `graph LR` (left-to-right) for processes and `graph TD` (top-down) for hierarchies.
- Label edges when the relationship isn't obvious.
- For complex architectures, show the high-level view first, then drill into subsystems on subsequent slides.
