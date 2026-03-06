# 📊 Matplotlib: Complete Tutorial & Case Study

Welcome to the ultimate Matplotlib tutorial! This repository contains two comprehensive Jupyter notebooks that will take you from absolute beginner to a confident user of Matplotlib — one of the most popular data visualization libraries in Python.

| Notebook | Description |
|----------|-------------|
| `matplotlib_T.ipynb` | Step-by-step tutorial covering all essential plot types, customization, subplots, saving figures, and a first taste of real-world data analysis with Netflix titles |
| `Netflix_Data_Visualization.ipynb` | An extended case study that applies everything from the tutorial to explore the Netflix dataset in depth |

---

## 📖 Table of Contents

1. [Introduction](#introduction)
2. [Setup and Imports](#setup-and-imports)
3. [Your First Line Plot](#1-your-first-line-plot)
4. [Understanding Key Terms](#2-understanding-key-terms)
5. [Customizing Line Plots](#3-customizing-line-plots)
6. [Bar Plots](#4-bar-plots)
7. [Pie Charts](#5-pie-charts)
8. [Histograms](#6-histograms)
9. [Scatter Plots](#7-scatter-plots)
10. [Subplots](#8-subplots)
11. [Saving Figures](#9-saving-figures)
12. [Real-World Example: Netflix Data Analysis](#10-real-world-example-netflix-data-analysis)
13. [Extended Netflix Data Analysis](#11-extended-netflix-data-analysis)
14. [Key Takeaways](#key-takeaways)
15. [Further Resources](#further-resources)
16. [License](#license)

---

## Introduction

Matplotlib is the most widely used data visualization library in Python. It provides both a MATLAB-like interface (`pyplot`) and a powerful object-oriented API. This repository offers two complementary notebooks:

- The **tutorial notebook** introduces essential plot types, customization options, and basic real-world usage.
- The **case study notebook** dives deep into a real dataset (Netflix titles), demonstrating how to clean data, choose the right visualizations, and draw meaningful insights.

---

## Setup and Imports

Every plotting session starts with importing the necessary libraries:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

| Library | Purpose |
|---------|---------|
| `numpy` | Numerical arrays and mathematical operations |
| `pandas` | Data manipulation and analysis |
| `matplotlib.pyplot` | Main plotting module (MATLAB-like interface) |

---

## 1. Your First Line Plot

```python
x = [1, 2, 3, 4]
y = [10, 20, 15, 25]

plt.plot(x, y)
plt.show()
```

**What happens:**
- `plt.plot(x, y)` draws a line connecting the points (1,10), (2,20), (3,15), (4,25).
- By default, it renders a solid blue line.
- `plt.show()` displays the plot inline in Jupyter or in a separate window.

---

## 2. Understanding Key Terms

| Term | Description |
|------|-------------|
| **Data point** | A single pair (x, y) in your dataset |
| **x-axis / y-axis** | Horizontal (independent) and vertical (dependent) axes |
| **Figure** | The entire canvas or window containing one or more plots |
| **Axes** | The area where data is plotted (a single plot inside a figure) |
| **Plot** | The visual representation (line, bars, markers, etc.) |
| **Marker** | A symbol (circle, square, triangle) highlighting individual data points |
| **Line style** | The pattern of the line (solid, dashed, dotted) |
| **Color** | The color of the line or markers |
| **Legend** | A box explaining what each line/color represents |
| **Label** | Text describing the x-axis or y-axis |
| **Title** | A headline for the chart |
| **Grid** | Background grid lines to improve readability |
| **Method** | A function that belongs to an object (e.g., `ax.plot()`) |
| **Parameter** | An argument passed to a function (e.g., `color='red'`) |

---

## 3. Customizing Line Plots

```python
months = [1, 2, 3, 4]
sales = [1000, 1500, 1200, 1800]

plt.plot(months, sales,
         color='blue',          # line color
         linestyle='--',        # dashed line
         linewidth=2,           # thickness of the line
         marker='o',            # circle markers at data points
         label='2025 sales data')

plt.xlabel('Months')
plt.ylabel('Sales per month')
plt.title('Monthly Sales Data Report')
plt.legend(loc='upper left', fontsize=12)
plt.grid(color='gray', linestyle=':', linewidth=1)
plt.xlim(1, 4)
plt.ylim(0, 2000)
plt.xticks([1, 2, 3, 4], ['M1', 'M2', 'M3', 'M4'])

plt.show()
```

**Parameter Reference:**

| Parameter | Description |
|-----------|-------------|
| `color` | Named color (e.g. `'blue'`) or hex code |
| `linestyle` | `'-'` solid, `'--'` dashed, `':'` dotted, `'-.'` dash-dot |
| `linewidth` | Numeric value controlling line thickness |
| `marker` | `'o'` circle, `'s'` square, `'^'` triangle, `'D'` diamond |
| `label` | Text that appears in the legend |
| `xlabel` / `ylabel` | Axis descriptions |
| `title` | Chart headline |
| `legend` | Places a legend; `loc` accepts `'upper left'`, `'lower right'`, `'best'`, etc. |
| `grid` | Adds a grid with customisable color, line style, and width |
| `xlim` / `ylim` | Forces the axis to display a specific range |
| `xticks` | Replaces numeric tick positions with custom labels |

---

## 4. Bar Plots

Bar charts are perfect for comparing categories.

### Vertical Bar Chart

```python
product = ['A', 'B', 'C', 'D']
sales2 = [1000, 1500, 800, 1200]

plt.bar(product, sales2, color='red', label='Sales 2026')
plt.xlabel('Product')
plt.ylabel('Sales')
plt.title('Product Sale Comparison')
plt.legend()
plt.show()
```

### Horizontal Bar Chart

```python
plt.barh(product, sales2, color='red', label='Sales 2026')
plt.xlabel('Product')
plt.ylabel('Sales')
plt.title('Product Sale Comparison')
plt.legend()
plt.show()
```

> **Note:** `barh` draws horizontal bars — categories appear on the y-axis and values on the x-axis.

---

## 5. Pie Charts

Pie charts show proportions of a whole.

```python
regions = ['North', 'South', 'East', 'West']
revenue = [3000, 2000, 1500, 1000]

plt.pie(revenue, labels=regions, autopct='%1.1f%%',
        colors=['red', 'green', 'blue', 'yellow'])
plt.title('Revenue contribution by region')
plt.show()
```

| Parameter | Description |
|-----------|-------------|
| `labels` | Names for each slice |
| `autopct` | Percentage format string (e.g. `'%1.1f%%'` = one decimal place) |
| `colors` | List of colors for the slices |

---

## 6. Histograms

Histograms visualise the distribution of a continuous variable.

```python
scores = [12, 43, 53, 57, 87, 45, 49, 78, 32, 11, 65, 93, 71, 54, 25, 84, 54]

plt.hist(scores, bins=5, color='purple', edgecolor='black')
plt.xlabel('Score range')
plt.ylabel('Number of students')
plt.title('Score Distribution of students')
plt.show()
```

| Parameter | Description |
|-----------|-------------|
| `bins` | Number of equal-width bins (or a sequence of bin edges) |
| `edgecolor` | Color of the bin borders |

---

## 7. Scatter Plots

Scatter plots reveal relationships between two numerical variables.

### Single Group

```python
hours_studied = [1, 2, 3, 4, 5, 6, 7, 8]
exam_score    = [99, 55, 60, 65, 70, 75, 80, 85]

plt.scatter(hours_studied, exam_score,
            color='green', marker='o', label='Student Data')
plt.xlabel('Hours studied')
plt.ylabel('Exam score')
plt.title('Relationship between study time and exam score')
plt.legend()
plt.grid(True)
plt.show()
```

### Multiple Groups

```python
plt.scatter([1, 2, 3], [50, 60, 70], color='blue', label='Class A')
plt.scatter([1, 2, 3], [45, 68, 99], color='red',  label='Class B')
plt.xlabel('Hours studied')
plt.ylabel('Exam score')
plt.title('Comparison of two classes')
plt.legend()
plt.grid(True)
plt.show()
```

> Each call to `scatter` adds a new set of points with its own color and label.

---

## 8. Subplots

Subplots allow you to place multiple plots inside a single figure.

### Using `plt.subplot`

```python
x = [1, 2, 3, 4]
y = [10, 20, 15, 25]

plt.subplot(1, 2, 1)   # 1 row, 2 columns, first subplot
plt.plot(x, y)
plt.title('Line chart')

plt.subplot(1, 2, 2)   # second subplot
plt.bar(x, y)
plt.title('Bar chart')

plt.tight_layout()
plt.show()
```

### Using `plt.subplots` — Object-Oriented Style

```python
fig, ax = plt.subplots(1, 2, figsize=(10, 5))

ax[0].plot(x, y)
ax[0].set_title('Line plot')

ax[1].bar(x, y)
ax[1].set_title('Bar chart')

plt.tight_layout()
plt.suptitle('Comparison of line and bar chart')
plt.show()
```

> **Why object-oriented?** It gives fine-grained control over each axes object. Use `set_title` and `set_xlabel` instead of `plt.title` and `plt.xlabel`.

---

## 9. Saving Figures

Save your plots as image files (PNG, PDF, SVG, etc.) using `savefig`.

```python
plt.plot(x, y, color='blue', marker='o')
plt.title('Simple Line Plot')
plt.xlabel('X Axis')
plt.ylabel('Y Axis')

plt.savefig('line_plot.png', dpi=300, bbox_inches='tight')
plt.show()
```

| Parameter | Description |
|-----------|-------------|
| `dpi` | Dots per inch — higher value = better quality |
| `bbox_inches='tight'` | Trims white space around the plot |

---

## 10. Real-World Example: Netflix Data Analysis

The tutorial notebook applies basic Matplotlib to the Netflix dataset. It covers:

- **Loading and cleaning** the data (dropping rows with missing values).
- **Bar chart** — comparing the number of Movies vs. TV Shows.
- **Pie chart** — content ratings distribution.
- **Histogram** — distribution of movie durations.
- **Scatter plot** — release year vs. number of shows.

```python
df = pd.read_csv('Data_sets/netflix_titles.csv')
df = df.dropna(subset=['type', 'release_year', 'rating', 'country', 'duration'])
```

These examples demonstrate how to quickly turn raw data into meaningful visualizations.

---

## 11. Extended Netflix Data Analysis

The second notebook, `Netflix_Data_Visualization.ipynb`, expands the case study significantly. It uses the same dataset but produces a wider variety of plots with more advanced data preparation. Highlights include:

- **Top 10 Countries by Number of Shows** — A horizontal bar chart highlighting the most prolific Netflix content-producing countries.
- **Movies and TV Shows Released Over Time** — A two-panel subplot with separate line charts for Movies and TV Shows, making growth trends easy to compare.
- All plots from the tutorial are re-created with clean, well-annotated code, serving as a solid reference for building a complete data analysis report.

> This notebook is ideal for anyone who wants to see how individual techniques come together to answer real-world questions.

---

## Key Takeaways

- **Matplotlib is flexible** — you can customise almost every visual element.
- **Use `pyplot` for quick plots**, but switch to the object-oriented API for complex layouts.
- **Always label your axes and add a title** — your plots should be self-explanatory.
- **Choose the right plot type** for your data:

  | Plot Type | Best Used For |
  |-----------|--------------|
  | 📈 Line | Trends over time |
  | 📊 Bar | Comparisons between categories |
  | 🥧 Pie | Proportions of a whole |
  | 📉 Histogram | Distribution of a variable |
  | 🔵 Scatter | Relationships between two variables |

- **Clean your data before plotting** — missing values can break your code or produce misleading charts.
- **Save figures** with appropriate `dpi` and `bbox_inches='tight'` for publications or reports.
- **Real-world datasets require iteration** — the extended Netflix notebook shows how to explore a dataset from multiple angles.

---

## Further Resources

- 📘 [Official Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- 🖼️ [Matplotlib Gallery](https://matplotlib.org/stable/gallery/index.html) — hundreds of examples
- 🎨 [Seaborn](https://seaborn.pydata.org/) — a high-level interface for statistical graphics built on Matplotlib
- 🐼 [Pandas Visualization](https://pandas.pydata.org/docs/user_guide/visualization.html) — quick plotting directly from DataFrames

---

## License

This repository and the accompanying notebooks are provided under the **MIT License**.
Feel free to use, modify, and share them with proper attribution.

---

<div align="center">Happy plotting! 📈</div>
