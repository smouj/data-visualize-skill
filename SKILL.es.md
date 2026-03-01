---
name: Data Visualize
category: analysis
purpose: Creates data visualizations and charts from datasets using matplotlib, plotly, seaborn
tags: visualization, charts, data, matplotlib, plotly, seaborn, graphs, plots
version: 1.0.0
requires:
  - python
  - matplotlib
  - plotly
  - seaborn
  - pandas
commands:
  - /visualize
  - /chart
  - /plot
  - /graph
---

# Data Visualize (ES) Skill

## Overview

This skill generates professional data visualizations and charts from datasets using Python's most powerful plotting libraries: matplotlib, plotly, and seaborn.

## Supported Chart Types

| Command | Library | Best For |
|---------|---------|----------|
| `/visualize line` | matplotlib | Time series, trends |
| `/visualize bar` | matplotlib/seaborn | Comparisons, categorical data |
| `/visualize scatter` | matplotlib/plotly | Correlations, distributions |
| `/visualize heatmap` | seaborn | Correlation matrices, density |
| `/visualize pie` | matplotlib | Proportions, percentages |
| `/visualize histogram` | matplotlib | Frequency distributions |
| `/visualize box` | seaborn | Statistical summaries, outliers |
| `/visualize interactive` | plotly | Web dashboards, hover data |

## Real Use Cases

### 1. Analyze Server Logs Response Times
```
/visualize line --data /var/log/nginx/access.log --time-col timestamp --val-col response_time --output response_times.png
```
Creates a time-series line chart showing response times over the log period.

### 2. Sales by Category Comparison
```
/visualize bar --data sales_q4.csv --x category --y revenue --agg sum --palette viridis --output sales_by_category.png
```
Generates grouped bar chart comparing revenue across product categories.

### 3. User Engagement Correlation Matrix
```
/visualize heatmap --data user_metrics.csv --cols login_count,page_views,session_duration,purchases --output correlation.png
```
Creates correlation heatmap to identify relationships between user engagement metrics.

### 4. Website Traffic Distribution
```
/visualize histogram --data google_analytics.csv --col visitors --bins 30 --kde true --output traffic_dist.png
```
Shows distribution of daily visitors with KDE overlay.

### 5. A/B Test Results with Statistical Summary
```
/visualize box --data ab_test_results.csv --x variant --y conversion_rate --output ab_test.png
```
Compares conversion rates across test variants showing quartiles and outliers.

### 6. Interactive Revenue Dashboard
```
/visualize interactive --data revenue_data.csv --type scatter --x month --y revenue --color product_line --output dashboard.html
```
Creates interactive HTML chart with zoom, pan, and hover details.

## Commands

### /visualize
Main command for all visualizations.

```
/visualize <chart_type> [options]
```

**Options:**
- `--data <path>` - Path to CSV/JSON file (required)
- `--x <column>` - X-axis column name
- `--y <column>` - Y-axis column name(s), comma-separated for multiple
- `--color <column>` - Column for color encoding
- `--agg <sum|mean|count|min|max>` - Aggregation function for grouped data
- `--bins <n>` - Number of bins for histogram
- `--palette <name>` - Color palette (viridis, plasma, inferno, magma, coolwarm,Set2)
- `--title <text>` - Chart title
- `--output <filename>` - Output filename (PNG/HTML)
- `--width <px>` - Figure width
- `--height <px>` - Figure height
- `--dpi <n>` - Resolution (default 300)
- `--interactive` - Force plotly interactive output

### /chart
Alias for /visualize with default matplotlib rendering.

### /plot
Alias for /visualize optimized for scientific plotting styles.

### /graph
Alias for /visualize with network/graph support.

## Troubleshooting

### Error: "No data found in file"
- Verify CSV has headers: `--header true`
- Check delimiter: `--delimiter ,` (comma) or `--delimiter \t` (tab)
- Confirm file encoding: `--encoding utf-8`

### Error: "Column not found"
- List available columns: `--list-cols`
- Check exact column names: `--preview 5`

### Chart too cluttered
- Reduce categories: `--top-n 10`
- Enable sampling: `--sample 1000`
- Rotate labels: `--rotate-x 45`

### Memory error with large datasets
- Enable sampling: `--sample 10000`
- Use chunked processing: `--chunk 5000`

### Interactive plot not rendering
- Install kaleido: `pip install kaleido`
- Export static: `--format png`

## Examples

### Minimal
```
/visualize line --data data.csv --x date --y sales
```

### Full Options
```
/visualize scatter --data metrics.csv --x cpu_usage --y response_time --color region --palette coolwarm --title "Performance by Region" --width 1200 --height 800 --output performance.png
```

### Statistical with Aggregation
```
/visualize bar --data transactions.csv --x category --y amount --agg sum --top-n 15 --palette Set2 --output top_categories.png
```

### Multi-series
```
/visualize line --data metrics.csv --x date --y revenue,cost,profit --title "Financial Overview" --output financials.png
```

## Configuration

Default settings can be customized in `~/.openclaw/config/data-visualize.json`:

```json
{
  "default_palette": "viridis",
  "default_dpi": 300,
  "default_width": 800,
  "default_height": 600,
  "theme": "seaborn-v0_8-darkgrid",
  "interactive_format": "html"
}
```