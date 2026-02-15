# AgentPreso

**AI-native presentations from markdown.**

<!-- TODO: Add badges (npm, CI, license, discord) -->

## What is AgentPreso?

AgentPreso lets you create professional slide decks from markdown files with built-in support for charts, diagrams, and AI-generated graphics. Everything renders in the cloud — you write markdown locally or through an AI agent, push to AgentPreso, and get back polished HTML, PDF, or PPTX. The interface is a CLI and MCP server, designed for humans and AI agents alike.

## 30-Second Quickstart

```bash
# Install the CLI
curl -fsSL https://agentpreso.com/install.sh | sh

# Authenticate
agentpreso login

# Create your first deck
agentpreso create my-deck --theme glacier

# Edit my-deck.md, then render
agentpreso render my-deck.md --format pdf
```

## Install as Agent Skill

For [Claude Code](https://docs.anthropic.com/en/docs/claude-code):

```
claude mcp add-skill agentpreso/agentpreso
```

This teaches Claude Code how to create presentations on your behalf — it learns the markdown format, available themes and layouts, chart syntax, and rendering workflow. When you ask Claude to "make a presentation about X", it will use AgentPreso automatically.

## Features

- **10 built-in themes** — from corporate to creative, dark to light
- **15 slide layouts** — title, bullets, columns, image splits, stats grids, and more
- **Inline charts** — bar, line, pie, donut, area, and stacked charts via simple YAML
- **Mermaid diagrams** — flowcharts, sequence diagrams, mind maps, Gantt charts, and more
- **AI image generation** — describe an image in a code block, get a professional graphic
- **Template variables** — `{{variable}}` syntax for reusable, parameterized decks
- **Export to HTML, PDF, PPTX** — cloud rendering, no local dependencies
- **Dark mode per slide** — `<!-- _class: invert -->` on any slide
- **Custom themes with logos** — upload your brand theme with CSS and logo assets
- **MCP integration** — AI agents create and manage presentations via the Model Context Protocol

## Themes

| Theme | Description |
|-------|-------------|
| `agentpreso` | Navy & tangerine on warm ivory |
| `blueprint` | Technical, precise, engineering-focused |
| `botanica` | Nature-inspired, organic, warm greens |
| `chalk` | Blackboard-style, handwritten feel |
| `ember` | Warm, bold, fire-inspired gradients |
| `glacier` | Cool blues, icy, clean, corporate |
| `ink` | High-contrast black & white, editorial |
| `maison` | Elegant, luxury, sophisticated serif |
| `neon` | Vibrant, futuristic, dark with bright accents |
| `terminal` | Monospace, developer-focused, green on black |

## Documentation

Full documentation is available at [agentpreso.com/docs](https://agentpreso.com/docs).

## License

[MIT](./LICENSE) -- Copyright 2026 AgentPreso
