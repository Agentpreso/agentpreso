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
6. **Push and preview**: Run `agentpreso push <file>` then `agentpreso preview <file> -s 1` to verify
7. **Iterate**: Ask if adjustments are needed
