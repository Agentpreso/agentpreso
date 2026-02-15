---
description: Create a full custom AgentPreso theme with your organization's branding
---

# Create Custom Theme

## Arguments

$ARGUMENTS may contain brand details, color preferences, or a company name.

## Process

1. **Gather brand requirements**:
   - Primary, secondary, accent colors (hex values)
   - Light and dark palette (optional)
   - Heading and body fonts
   - Style preferences: sharp/rounded/pill borders, compact/comfortable/spacious density
   - Logo file (optional)

2. **Create theme directory**:
   ```bash
   mkdir <theme-name>
   ```

3. **Write theme.yaml**:
   ```yaml
   meta:
     name: <theme-name>
     description: <description>
     version: 1.0.0
   fonts:
     heading: "'Font', sans-serif"
     body: "'Font', sans-serif"
     code: "'Fira Code', monospace"
   colors:
     light:
       primary: "#hex"
       secondary: "#hex"
       accent: "#hex"
       bg: "#ffffff"
       text: "#222222"
       muted: "#666666"
   style:
     radius: rounded
     density: comfortable
     headingStyle: normal
     accentStyle: solid
   ```

4. **Write overrides.css** (optional): For custom styling beyond variables

5. **Write scaffold.md**: Starter deck demonstrating all layouts with the theme

6. **Upload**: `agentpreso themes add ./<theme-name>/`

7. **Preview**: Create a test deck with the theme and preview each slide

8. **Iterate**: Adjust colors, fonts, or styles based on preview
