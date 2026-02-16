---
description: Export an AgentPreso presentation to HTML, PDF, or PowerPoint
---

# Render Presentation

## Arguments

$ARGUMENTS may contain the file path and/or desired format.

## Process

1. **Identify the deck file**: Look for `.md` files in the current directory with AgentPreso frontmatter. If $ARGUMENTS specifies a file, use that.
2. **Choose format**: If not specified, ask the user:
   - **PDF** — for sharing, printing, archiving (recommended default)
   - **PPTX** — for handing off to collaborators who need to edit
   - **HTML** — for web viewing, smallest file size
3. **Check for template variables**: If the deck uses `{{variable}}` placeholders, ask if the user wants to provide values via `--var` flags or a `--vars` YAML file.
4. **Push first**: Run `agentpreso push <file>` to ensure cloud has latest version
5. **Render**: Run `agentpreso render <file> --format <format>`
6. **Deliver**: Share the output file path with the user
