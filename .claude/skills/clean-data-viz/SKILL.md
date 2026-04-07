---
name: clean-data-viz
description: Use when creating any chart, plot, graph, or data visualization in ANY language (R, Python, JavaScript, Observable, etc.). Triggers on words like plot, chart, graph, visualize, histogram, scatter, heatmap, bar chart, time series, facet, small multiples, dashboard, figure, dataviz. Also use when the user asks to "show data", "compare trends", "make a figure", or any request that involves turning data into a visual form. Even if the user doesn't explicitly say "visualization", if they are working with data and a chart would serve them well, consult this skill.
---

# Data Visualization Skill

A principled approach to data visualization rooted in Edward Tufte's analytical design philosophy and Kieran Healy's perceptual and practical framework. This skill produces clear, honest, publication-quality graphics across R, Python, and other languages.

## Core Philosophy

Visualization is a reasoning tool, not decoration. Every chart should help the viewer think about the substance of the data — not about the design, the software, or the cleverness of the creator. The two intellectual traditions this skill draws from are complementary:

- **Tufte** asks: Is this chart honest? Is every drop of ink earning its place? Could we erase something without losing information?
- **Healy** asks: Can the viewer actually *perceive* what we're encoding? Are we mapping data to visual channels that human vision decodes accurately?

Together they produce charts that are truthful, minimal, perceptible, and informative.

---

## Principles (apply to ALL visualizations, in any language)

### 1. Graphical Integrity — Tell the Truth

- The Lie Factor (ratio of visual effect size to data effect size) must be 1. Never exaggerate or compress effects through distorted axes, perspective, or area scaling.
- Start y-axes at zero for bar charts and area charts. For line charts and scatterplots, choose axes that show the data's structure honestly.
- Never cherry-pick data. Show full context: complete time ranges, relevant baselines, comparison groups.
- Label clearly. Write explanations directly on the chart. Annotate important events in the data.
- Show data variation, not design variation. Changes in the chart should reflect changes in the data, never changes in the graphic style.

### 2. Maximize Data-Ink — Above All Else, Show the Data

- **Data-ink ratio** = proportion of ink devoted to data ÷ total ink. Push this toward 1.
- Remove all gridlines by default. If essential, use only faint horizontal major gridlines.
- Remove top and right spines (borders). Keep left and bottom spines thin.
- No backgrounds, gradients, 3D effects, drop shadows, or decorative elements.
- No redundant encoding (e.g., coloring bars AND adding value labels AND using a legend for the same dimension).
- Every mark on the chart must encode data. If you can erase it without losing information, erase it.

### 3. Respect Perceptual Hierarchy — Encode Data in Channels Humans Read Accurately

This is Healy's (via Cleveland & McGill) key contribution. Humans decode visual channels with dramatically different accuracy. Prefer channels higher in this ranking:

1. **Position along a common scale** (best — scatterplots, dot plots, line charts)
2. **Position along non-aligned scales** (small multiples with shared axes)
3. **Length** (bar charts — but only from a common baseline)
4. **Direction / Angle** (slope judgments — usable but less precise)
5. **Area** (bubble charts, treemaps — use sparingly, humans underestimate area)
6. **Volume, curvature** (almost never appropriate for quantitative comparison)
7. **Color saturation / shading** (worst for quantity — fine for categories)

**Practical consequence**: Prefer dot plots and bar charts over pie charts. Prefer line charts over stacked areas. Prefer small multiples over dual-axis charts. Never use 3D.

### 4. Direct Labeling — No Legend Lookup

- Label data series directly on or beside the data. The viewer's eye should never bounce between plot and legend.
- If a legend is absolutely unavoidable, place it at the bottom with no title box.
- Use color *and* direct text labels together for accessibility.
- Annotations (key events, inflection points, outlier explanations) belong ON the chart.

### 5. Small Multiples — The Best Design Solution for Multivariate Data

- When comparing across categories, use faceted/small-multiple panels — the same chart repeated for each subset.
- Reorder panels by a meaningful metric (never alphabetically unless the alphabet IS the variable).
- Use free scales only when the comparison is within-panel. Use fixed scales when the comparison is across panels.
- Small multiples leverage the most accurate perceptual channel (position on a common scale) while showing many dimensions.

### 6. Aesthetics Serve Perception — Three Sources of Bad Figures

Healy identifies three distinct ways charts fail:

- **Aesthetic failures**: Ugly or cluttered design — gratuitous 3D, garish colors, chartjunk. Fix by reducing to essentials.
- **Substantive failures**: The data itself is misleading — cherry-picked, truncated axes, wrong chart type. Fix by showing full context and choosing honest encodings.
- **Perceptual failures**: The chart is "correct" but the human visual system can't decode it — e.g., comparing areas in a bubble chart, reading slight hue differences in a choropleth. Fix by choosing higher-ranked perceptual channels.

A good chart avoids all three failure modes simultaneously.

---

## Visual Style Defaults

These defaults produce a clean, warm, publication-quality aesthetic. They can be customized, but deviations should be deliberate.

### Color Palette (Colorblind-Safe by Default)

This palette is derived from the **Okabe-Ito** universal design standard, which is distinguishable under deuteranopia, protanopia, and tritanopia. All colors have been tested for mutual discriminability under simulated color vision deficiencies.

| Role | Hex | Name | CVD note |
|------|-----|------|----------|
| Background (panel + plot) | `#f8f5f0` | warm off-white | — |
| Primary data | `#0072B2` | deep blue | Safe across all CVD types |
| Secondary data | `#E69F00` | golden amber | Distinct from blue under all CVD |
| Accent / highlight | `#D55E00` | vermillion | Distinct from blue and gold under all CVD |
| Contrast accent | `#56B4E9` | sky blue | Distinct from deep blue via lightness |
| Additional category | `#009E73` | bluish green | Safe; avoid pairing with vermillion for protan |
| Additional category | `#CC79A7` | reddish purple | Safe across all CVD types |
| All text | `#3C3C3C` | charcoal (never pure black) | — |
| Subtle dividers | `#d4cfc4` | warm gray | — |
| De-emphasis / baseline | `#b0aaaa` | mid gray | — |

**Colorblind design rules:**
- Never encode meaning with red vs. green alone. Use blue vs. orange or blue vs. vermillion instead.
- Always pair color with a second channel: direct labels, line dash patterns, point shapes, or fill patterns.
- For sequential/continuous data: use **viridis**, **cividis** (specifically designed for CVD), or a single-hue luminance ramp. Never use rainbow or jet.
- For categorical data (>6 categories): use ColorBrewer qualitative palettes that pass CVD simulation (Set2, Dark2, or Paired). Never use default software color cycles.
- Test your palette: use tools like [Coblis](https://www.color-blindness.com/coblis-color-blindness-simulator/) or R's `colorspace::cvd_emulator()` or Python's `colorspacious` to verify.

### Typography

- Title: bold, `#3C3C3C`, largest text on the chart
- Subtitle: regular weight, muted color (e.g., `#6b6b6b`), smaller than title. Use for methodology notes or key takeaway.
- Axis labels: bold, `#3C3C3C`
- Axis titles: remove when obvious from context (e.g., "Year" on a time series x-axis). Keep when the variable name isn't self-evident.
- Annotations: smaller than axis text, same charcoal color

### Chart Chrome

- No gridlines (default). If a reader needs to trace values, add faint horizontal gridlines only (`#e8e4dd`, linewidth ~0.2).
- Remove top and right spines.
- Left and bottom spines: thin (`0.2–0.3` linewidth), `#3C3C3C`.
- Tick marks: minimal. Remove x-axis ticks when labels suffice.

### Output

- Prefer static output (PNG at 150+ DPI, SVG, or PDF) for publication and reproducibility.
- Interactive charts (Plotly, D3, Observable) are appropriate for dashboards and exploratory tools, but apply the same principles of integrity, data-ink ratio, and perceptual hierarchy.

---

## Chart Type Selection Guide

Choose chart types that map data to the highest-accuracy perceptual channels:

### Distributions
- **One variable**: histogram, density plot, or strip/jitter plot
- **Compare distributions**: faceted histograms, overlaid densities (max 3), box plots, or violin plots
- Avoid: pie charts, donut charts for distributional data

### Comparisons
- **Ranked categories**: horizontal bar chart or Cleveland dot plot (dot plot preferred — less ink)
- **Few groups, one measure**: bar chart with direct labels
- **Many groups**: lollipop chart or dot plot
- Avoid: grouped 3D bars, radar/spider charts

### Time Series
- **Single series**: line chart (with points at data if n < ~30)
- **Multiple series**: line chart with direct labeling, or small multiples
- **Highlighting a range**: ribbon/band for historical range, line for current
- Avoid: stacked area charts (hard to read individual series), dual-axis charts

### Relationships
- **Two continuous variables**: scatterplot
- **Three variables**: scatterplot + color or size (but beware area perception)
- **Many variables**: scatterplot matrix (pairs plot) or parallel coordinates
- Avoid: bubble charts for precise comparison, 3D scatterplots

### Part-to-Whole
- **Few parts**: horizontal stacked bar (max 3–4 segments) or grouped bars
- **Many parts**: treemap (if approximate reading is acceptable)
- Avoid: pie charts, donut charts, stacked bars with many segments

### Spatial
- **Geographic**: choropleth (be aware of area-size bias), cartogram, or dot-density map
- **Matrix data**: heatmap with a sequential color scale (viridis)

### Hierarchy of Preference
1. Dot plot / Cleveland dot plot
2. Line + point (time series)
3. Bar chart (horizontal preferred for categories)
4. Small multiples / faceted panels
5. Scatterplot
6. Heatmap
7. Box plot / violin

Charts to avoid entirely: pie, donut, 3D anything, radar/spider, stacked bars with >3 segments, dual-axis, exploded charts.

---

## Implementation

### R (ggplot2) — Canonical Implementation

R with ggplot2 is the primary recommended tool. It implements the grammar of graphics, making it natural to layer data mappings, statistics, and annotations.

```r
library(ggplot2)

theme_principled <- function(base_size = 11, base_family = "") {
  theme_minimal(base_size = base_size, base_family = base_family) %+replace%
    theme(
      # Background
      panel.background = element_rect(fill = "#f8f5f0", color = NA),
      plot.background = element_rect(fill = "#f8f5f0", color = NA),
      
      # Grid: remove all
      panel.grid = element_blank(),
      
      # Axes
      axis.line.x = element_line(colour = "#3C3C3C", linewidth = 0.25),
      axis.line.y = element_line(colour = "#3C3C3C", linewidth = 0.25),
      axis.text = element_text(face = "bold", color = "#3C3C3C", size = rel(0.9)),
      axis.title = element_text(color = "#3C3C3C", size = rel(1)),
      axis.ticks = element_line(colour = "#3C3C3C", linewidth = 0.2),
      axis.ticks.length = unit(3, "pt"),
      
      # Titles
      plot.title = element_text(
        face = "bold", color = "#3C3C3C", size = rel(1.3),
        hjust = 0, margin = margin(b = 4)
      ),
      plot.subtitle = element_text(
        color = "#6b6b6b", size = rel(0.9),
        hjust = 0, margin = margin(b = 10)
      ),
      plot.caption = element_text(
        color = "#999999", size = rel(0.7), hjust = 1
      ),
      
      # Legend (disabled by default — use direct labels)
      legend.position = "none",
      
      # Facets
      strip.text = element_text(
        face = "bold", color = "#3C3C3C", size = rel(0.95)
      ),
      strip.background = element_blank(),
      
      # Margins
      plot.margin = margin(10, 15, 10, 10)
    )
}

# Primary palette — Okabe-Ito derived, colorblind-safe
palette_principled <- c(
  primary   = "#0072B2",
  secondary = "#E69F00",
  accent    = "#D55E00",
  contrast  = "#56B4E9",
  green     = "#009E73",
  purple    = "#CC79A7",
  muted     = "#b0aaaa"
)
```

Usage example:
```r
ggplot(data, aes(x = year, y = value)) +
  geom_line(color = palette_principled["primary"], linewidth = 0.8) +
  geom_point(color = palette_principled["primary"], size = 2) +
  annotate("text", x = 2020, y = 85, label = "Pandemic peak",
           color = "#3C3C3C", size = 3, hjust = 0) +
  labs(
    title = "Clear, Informative Title",
    subtitle = "Subtitle with context or methodology note",
    x = NULL,  # Remove obvious axis title
    y = "Measure (units)"
  ) +
  theme_principled()
```

### Python (matplotlib + seaborn)

```python
import matplotlib.pyplot as plt
import matplotlib as mpl

# Style configuration — Okabe-Ito derived, colorblind-safe
STYLE = {
    "bg": "#f8f5f0",
    "text": "#3C3C3C",
    "primary": "#0072B2",
    "secondary": "#E69F00",
    "accent": "#D55E00",
    "contrast": "#56B4E9",
    "green": "#009E73",
    "purple": "#CC79A7",
    "muted": "#b0aaaa",
    "divider": "#d4cfc4",
}

def apply_principled_style(ax, fig=None):
    """Apply principled visualization style to a matplotlib axes."""
    if fig is None:
        fig = ax.get_figure()
    
    # Backgrounds
    fig.patch.set_facecolor(STYLE["bg"])
    ax.set_facecolor(STYLE["bg"])
    
    # Spines: remove top/right, thin left/bottom
    ax.spines["top"].set_visible(False)
    ax.spines["right"].set_visible(False)
    ax.spines["left"].set_linewidth(0.3)
    ax.spines["bottom"].set_linewidth(0.3)
    ax.spines["left"].set_color(STYLE["text"])
    ax.spines["bottom"].set_color(STYLE["text"])
    
    # Ticks
    ax.tick_params(colors=STYLE["text"], labelsize=9, width=0.3)
    for label in ax.get_xticklabels() + ax.get_yticklabels():
        label.set_fontweight("bold")
    
    # Grid: off
    ax.grid(False)


def save_principled(fig, filename, dpi=150):
    """Save with correct background color."""
    fig.savefig(filename, dpi=dpi, facecolor=STYLE["bg"],
                bbox_inches="tight", pad_inches=0.3)


# Usage example:
# fig, ax = plt.subplots(figsize=(8, 5))
# ax.plot(x, y, color=STYLE["primary"], linewidth=1.2)
# ax.set_title("Title", fontweight="bold", color=STYLE["text"], fontsize=14, loc="left")
# ax.set_xlabel("")  # Remove if obvious
# apply_principled_style(ax, fig)
# save_principled(fig, "output.png")
```

For **plotnine** (ggplot2 port to Python, preferred when available):

```python
from plotnine import *

theme_principled = (
    theme_minimal(base_size=11) +
    theme(
        panel_grid=element_blank(),
        panel_background=element_rect(fill="#f8f5f0", size=0),
        plot_background=element_rect(fill="#f8f5f0", size=0),
        axis_text=element_text(weight="bold", color="#3C3C3C"),
        axis_line_x=element_line(color="#3C3C3C", size=0.25),
        axis_line_y=element_line(color="#3C3C3C", size=0.25),
        axis_ticks_major_x=element_blank(),
        legend_position="none",
        plot_title=element_text(weight="bold", color="#3C3C3C", size=14),
        plot_subtitle=element_text(size=9, color="#6b6b6b"),
        strip_text=element_text(weight="bold", color="#3C3C3C"),
        strip_background=element_blank(),
    )
)
```

### Observable / JavaScript / D3

Apply the same principles programmatically:
- Set SVG background to `#f8f5f0`
- Use `#3C3C3C` for all text, bold axis labels
- Remove all gridlines or use very faint horizontal rules
- Remove top/right axis lines
- Direct-label data series; avoid tooltip-only labels for key comparisons
- Use the same color palette

---

## Checklist Before Finalizing Any Chart

Run through this before delivering any visualization:

- [ ] **Integrity**: Does the visual faithfully represent the data? Lie Factor ≈ 1?
- [ ] **Data-ink**: Can I remove anything without losing information?
- [ ] **Perception**: Am I using the highest-accuracy visual channel available for this data?
- [ ] **No chartjunk**: No 3D, shadows, gradients, decorative images, or unnecessary color?
- [ ] **Direct labels**: Is the viewer forced to consult a legend? Can I label directly instead?
- [ ] **Context**: Are axes labeled? Units clear? Baselines honest? Key events annotated?
- [ ] **Small multiples**: If comparing many categories, am I using facets instead of overplotting?
- [ ] **Color**: Is the palette colorblind-safe? No red-vs-green? Color paired with a second channel (label, shape, dash)? Sequential data uses viridis/cividis?
- [ ] **Order**: Are categories ordered by the data (not alphabetically)?
- [ ] **Title**: Does the title tell the reader what to see, not just what the chart shows?

---

## Common Mistakes to Catch

| Mistake | Why it's bad | Fix |
|---------|-------------|-----|
| Pie chart | Angle/area perception is poor | Horizontal bar or dot plot |
| Dual y-axes | Implies false correlation, confuses scales | Two separate panels |
| Rainbow color scale | Not perceptually uniform, bad for colorblind | viridis, cividis, or single-hue ramp |
| Red vs. green encoding | Indistinguishable for ~8% of men | Blue vs. orange, or add shape/dash |
| Color as sole differentiator | Fails under CVD and B&W printing | Always pair color with labels, shapes, or patterns |
| Alphabetical facet order | Meaningless ordering hides patterns | Reorder by metric |
| Legend for 2–3 series | Forces eye to bounce | Direct label on data |
| Stacked bars (>3 segments) | Only bottom segment is readable | Small multiples or grouped bars |
| Default software theme | Wastes ink on grid, borders, heavy ticks | Apply theme_principled |
| Truncated y-axis on bar chart | Exaggerates differences | Start at zero |
| 3D effects | Distorts perception, adds no information | Use 2D always |

---

## References

This skill synthesizes principles from the following works:

- Tufte, Edward R. (1983). *The Visual Display of Quantitative Information*. Graphics Press.
- Tufte, Edward R. (1990). *Envisioning Information*. Graphics Press.
- Tufte, Edward R. (1997). *Visual Explanations*. Graphics Press.
- Tufte, Edward R. (2006). *Beautiful Evidence*. Graphics Press.
- Healy, Kieran (2018). *Data Visualization: A Practical Introduction*. Princeton University Press. Draft at [socviz.co](https://socviz.co).
- Cleveland, William S. and Robert McGill (1984). "Graphical Perception: Theory, Experimentation, and Application to the Development of Graphical Methods." *JASA* 79(387): 531–554.
- Cleveland, William S. (1985). *The Elements of Graphing Data*. Wadsworth.
- Okabe, Masataka and Kei Ito (2008). "Color Universal Design (CUD)."
- Wilke, Claus O. (2019). *Fundamentals of Data Visualization*. O'Reilly.

## Acknowledgment

This skill builds on the original [data-visualization skill](https://github.com/skthewimp/claude-skills) by [@skthewimp](https://github.com/skthewimp).
