---
description: Create a new AgentPreso presentation from a topic or outline
---

# Create Presentation

## Arguments

$ARGUMENTS contains the topic, title, or outline for the presentation.

## Process

1. **Check prerequisites**: Verify `agentpreso` CLI is installed (`agentpreso --version`). If not, install with `curl -fsSL https://agentpreso.com/install.sh | sh`
2. **Understand the request**: If user provided a topic, generate an outline. If they provided an outline, use it directly.
3. **Choose theme**: Ask the user about audience and tone, then recommend a theme:
   - Technical/developer → terminal, blueprint, ink
   - Corporate/business → glacier, maison
   - Creative/marketing → neon, ember, botanica
   - General/clean → agentpreso, chalk
4. **Create the markdown file**: Write a valid AgentPreso `.md` file with:
   - Frontmatter: `marp: true`, `agentpreso.theme`, `paginate: true`
   - Title slide with `<!-- _class: title-hero -->` and `<!-- _paginate: skip -->`
   - 5-10 content slides using varied layouts
   - Closing slide
   - Every slide should have a visual element (chart, diagram, or image placeholder)
5. **Apply presentation craft**:
   - One idea per slide
   - Action-oriented titles ("Revenue grew 40%" not "Revenue")
   - Max 3-5 bullets per slide, 7 words per bullet
   - Vary layouts — don't repeat the same layout consecutively
6. **Push and generate previews**: Run `agentpreso push <file>`, then preview every slide:
   ```bash
   agentpreso preview <file> -s 1
   agentpreso preview <file> -s 2
   # ... for each slide
   ```
7. **Review slides** — use the strategy that fits your environment:

### Parallel review (if subagents are available)

If you can spawn subagents (e.g. Claude Code `Task` tool), review slides in parallel:

1. **Spawn one subagent per slide** (or per batch of 2-3 slides). Each subagent receives the slide PNG and reviews against these criteria:
   - **3-second test** — can someone grasp the point in 3 seconds?
   - **One idea** — does the slide try to say two things?
   - **Title quality** — is it action-oriented ("Revenue grew 40%") or just descriptive ("Revenue")?
   - **Text density** — more than 5 bullets or 7 words per bullet?
   - **Visual element** — does the slide have a chart, diagram, image, or graphic?
   - **Layout fit** — does the layout match the content type?
2. Each subagent returns findings as structured text:
   ```
   Slide 3: issues found
   - Title is descriptive, not action-oriented
   - 8 bullets — split into two slides
   Suggested fix: Change title to "Customer base doubled in Q3", move items 5-8 to a new slide
   ```
3. **Parent agent collects all findings**, edits the `.md` file once, re-pushes
4. **Re-preview only changed slides**, optionally re-review in parallel until no issues remain

Subagents must be **read-only** — they analyze PNGs and return text findings. Only the parent agent edits the markdown file. This avoids file contention.

### Sequential review (default)

If subagents are not available, review each slide yourself:
1. Look at each preview PNG
2. Check against the same criteria above
3. Fix issues in the `.md` file
4. Re-push and re-preview changed slides

8. **Deliver**: Share the final file with the user and offer to render to PDF/PPTX
