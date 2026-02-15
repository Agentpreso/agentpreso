---
description: Browse available AgentPreso themes and get help choosing one
---

# Theme Browser

## Arguments

$ARGUMENTS may contain a style preference or audience description.

## Process

1. **List themes**: Run `agentpreso themes` to show available themes
2. **Help choose**: If user needs guidance, recommend based on context:

   | Audience / Style | Recommended Themes |
   |------------------|--------------------|
   | Technical, developers | terminal, blueprint, ink |
   | Corporate, business | glacier, maison |
   | Creative, marketing | neon, ember, botanica |
   | Academic, education | chalk, botanica |
   | General purpose | agentpreso, glacier |
   | Presentations in dark rooms | neon, terminal, ember |

3. **Show theme details**: `agentpreso themes show <name>` for the recommended theme
4. **Apply to deck**: If user has an existing deck, update the frontmatter:
   ```yaml
   agentpreso:
     theme: <chosen-theme>
   ```
5. **Preview**: Push and preview to see the theme applied
