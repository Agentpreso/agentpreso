---
description: Add a data chart to an AgentPreso presentation
---

# Add Chart

## Arguments

$ARGUMENTS may contain the chart type, data description, or target slide.

## Process

1. **Determine chart type**: Ask if not specified:
   - `bar` — comparisons across categories
   - `line` — trends over time
   - `pie` / `donut` — proportions of a whole
   - `area` — volume over time
   - `stacked` — composition across categories
2. **Gather data**: Ask for labels and values, or accept a description and generate sample data
3. **Generate chart block**:
   ````
   ```chart
   type: bar
   data:
     labels: [Q1, Q2, Q3, Q4]
     datasets:
       - label: Revenue ($M)
         data: [4.2, 5.1, 6.3, 7.8]
   ```
   ````
4. **Insert into deck**: Add the chart block to the appropriate slide. Consider placing it in a `two-col` layout with commentary on the left and chart on the right.
5. **Push and preview**: `agentpreso push <file>` then preview the slide
