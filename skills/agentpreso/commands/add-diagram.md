---
description: Add a Mermaid diagram to an AgentPreso presentation
---

# Add Diagram

## Arguments

$ARGUMENTS may contain the diagram type, description, or target slide.

## Process

1. **Determine diagram type**: Ask if not specified:
   - `graph LR` or `graph TD` — flowcharts, processes
   - `sequenceDiagram` — API flows, interactions
   - `classDiagram` — data models
   - `stateDiagram-v2` — state machines
   - `gantt` — timelines, project plans
   - `erDiagram` — database schemas
   - `mindmap` — brainstorming
2. **Gather requirements**: What process/flow/relationship to show
3. **Generate diagram**:
   ````
   ```mermaid
   graph LR
       A[Input] --> B{Decision}
       B -->|Yes| C[Process]
       B -->|No| D[Skip]
   ```
   ````
4. **Keep it simple**: Max 5-7 nodes for readability
5. **Insert into deck**: Add to appropriate slide
6. **Push and preview**: Verify rendering
