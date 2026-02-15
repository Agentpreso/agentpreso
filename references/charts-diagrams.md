# Charts and Diagrams

AgentPreso renders charts and diagrams directly from code blocks in your markdown. No screenshots, no external tools -- write the data inline and it renders on the slide.

## Charts

Use a fenced code block with the `chart` language tag. Chart data is written in YAML:

````markdown
```chart
type: bar
data:
  labels: [Q1, Q2, Q3, Q4]
  datasets:
    - label: Revenue ($M)
      data: [4.2, 5.1, 6.3, 7.8]
```
````

### Supported Chart Types

| Type | Description |
|------|-------------|
| `bar` | Vertical bar chart |
| `line` | Line chart with data points |
| `pie` | Pie chart |
| `donut` | Donut (ring) chart |
| `area` | Filled area chart |
| `stacked` | Stacked bar chart |

### Multiple Datasets

Add multiple datasets for comparison:

````markdown
```chart
type: bar
data:
  labels: [Q1, Q2, Q3, Q4]
  datasets:
    - label: Revenue
      data: [4.2, 5.1, 6.3, 7.8]
    - label: Costs
      data: [3.1, 3.5, 4.0, 4.2]
```
````

### Custom Colors

Specify colors per dataset:

````markdown
```chart
type: line
data:
  labels: [Jan, Feb, Mar, Apr, May]
  datasets:
    - label: Users
      data: [100, 150, 300, 450, 600]
      color: "#2563eb"
    - label: Sessions
      data: [200, 350, 500, 800, 1200]
      color: "#16a34a"
```
````

If you omit `color`, the chart uses your theme's color palette (primary, accent, secondary).

### Template Variables in Charts

Charts support `{{variable}}` substitution -- useful for data-driven decks:

````markdown
```chart
type: bar
data:
  labels: {{quarter_labels}}
  datasets:
    - label: Revenue
      data: {{revenue_data}}
```
````

Supply the data when rendering:

```bash
agentpreso render deck.md --var quarter_labels='["Q1","Q2","Q3","Q4"]' --var revenue_data='[4.2,5.1,6.3,7.8]'
```

## Diagrams

Use a fenced code block with the `mermaid` language tag. AgentPreso renders Mermaid diagrams server-side as SVGs.

### Flowchart

````markdown
```mermaid
graph LR
    A[Input] --> B{Decision}
    B -->|Yes| C[Process]
    B -->|No| D[Skip]
    C --> E[Output]
    D --> E
```
````

### Sequence Diagram

````markdown
```mermaid
sequenceDiagram
    participant Client
    participant API
    participant DB
    Client->>API: POST /decks
    API->>DB: INSERT deck
    DB-->>API: OK
    API-->>Client: 201 Created
```
````

### Supported Diagram Types

| Type | Mermaid Syntax | Use Case |
|------|---------------|----------|
| Flowchart | `graph TD` or `graph LR` | Processes, pipelines |
| Sequence | `sequenceDiagram` | API flows, interactions |
| Class | `classDiagram` | Data models |
| State | `stateDiagram-v2` | State machines |
| Gantt | `gantt` | Timelines, project plans |
| Entity Relationship | `erDiagram` | Database schemas |
| Pie | `pie` | Simple proportions |
| Mindmap | `mindmap` | Brainstorming |

### Theme Integration

Diagrams automatically use your theme's colors. Mermaid inherits `--primary-color`, `--secondary-color`, and `--accent-color` from the active theme, so diagrams match the rest of your slides.

## Combining with Layouts

Charts and diagrams work in any layout. Place them alongside text using column layouts:

````markdown
<!-- _class: two-col -->

## Performance Overview

::left::

Our API response times improved 40% after the
infrastructure migration.

Key improvements:
- p50 latency: 45ms to 28ms
- p99 latency: 200ms to 120ms

::right::

```chart
type: line
data:
  labels: [Jan, Feb, Mar, Apr, May, Jun]
  datasets:
    - label: p50 (ms)
      data: [45, 42, 38, 32, 30, 28]
    - label: p99 (ms)
      data: [200, 180, 160, 140, 130, 120]
```
````
