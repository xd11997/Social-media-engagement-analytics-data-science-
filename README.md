# Content Engagement Analysis on RedNote (Xiaohongshu)

## Executive Summary
This project analyzes what drives engagement on **RedNote (Xiaohongshu)**, a major Chinese social media platform, and translates data insights into **practical posting strategies** for content creators.

Using ~4,000 real posts, I built an end-to-end analytics workflow combining:
- Exploratory data analysis
- Non-linear modeling (Random Forest)
- Model interpretation
- Conditional analysis

**Key outcome:**  
By applying the insights from this analysis, I adjusted my own posting strategy and observed an approximate **25% increase in engagement rate**, with a post reaching **~3,000–4,000 views within two weeks**.

Although the data is limited to one content domain, the **methodological framework is generalizable** to other social media platforms and topics.

---

## Background
As a data practitioner, I originally built a web scraper tool to automate parts of my research workflow, which proved useful not only to myself but also to colleagues. **Wanting to share this tool more broadly**, I decided to publish a post on RedNote (a Chinese social media platform) and quickly realized that content reach and engagement depended heavily on posting time, context, and presentation. This motivated me to move beyond intuition and systematically analyze **what actually drives engagement on the platform**.

Content creators often rely on intuition when deciding:
- When to post
- How to write titles
- Whether to use emojis

As an active content creator, I wanted to replace intuition with a **data-driven and repeatable decision framework**.

---

## Objective
The objectives of this project are to:
- Identify factors associated with post engagement (likes)
- Distinguish **structural factors** (content context) from **actionable levers** (timing and presentation)
- Build a framework that supports **real-world posting decisions**, not just predictive accuracy

The emphasis is on **interpretability, robustness, and applicability**, rather than maximizing model performance.

---

## Data
- ~4,000 public posts scraped from RedNote under multiple programming-related tags (#programming, #python, #CS, #pythonlearning)
- Each post includes:
  - Posting time
  - Topic tags (multi-label)
  - Title characteristics (presence, length)
  - Emoji usage
  - Engagement metrics (likes)

> Engagement is measured using likes as a proxy due to the lack of impression-level data.

---

## Approach

### 1. Data Cleaning and Transformation
- Deduplicated posts across overlapping tag-based searches
- Applied platform-specific rules (e.g., valid title length constraints)
- Converted the data type of the time-level data

### 2. Feature Engineering
- Time features: posting hour
- Text features: title length, title presence
- Emoji features: emoji usage and count
- Topic features: multi-hot encoded tags

### 3. Exploratory Data Analysis (EDA)
- Examined engagement distributions and non-linear patterns
- Identified candidate drivers, such as timing and presentation features
- Found that no single feature guarantees high engagement

### 4. Modeling
- Trained a Random Forest regression model to capture non-linear relationships and interactions
- Evaluated performance using R² and RMSE (moderate performance expected due to high noise)
- Used **permutation importance** to diagnose which features the model structurally depends on

### 5. Model Interpretation & Conditional Analysis
- Interpreted feature importance as **structural dependency**, not marginal or causal effect
- Performed targeted conditional analyses (e.g., time × emoji, time × title)
- Translated patterns into **context-aware posting strategies**

#### Ablation Analysis: Structural vs Actionable Factors
To further interpret feature importance results, I conducted an ablation analysis by retraining the model after removing the most structurally important topic tag.

Despite its high permutation importance, removing this tag resulted in only a marginal change in model performance. This indicates that:
- The tag functions as a **structural indicator** of content context rather than a unique driver of engagement.
- Its information can be partially reconstructed by correlated features such as posting time, other tags, and presentation characteristics.

This finding supports the hypothesis that different topic tags correspond to **different exposure pools** on the platform. While these pools have different engagement baselines, performance within each pool is primarily influenced by actionable factors such as timing and presentation, rather than tag choice alone.

---

## Key Insights

- **Posting time is the strongest driver of engagement**, defining a high- vs low-exposure baseline.
- **Emoji usage provides larger marginal gains during off-peak hours**, when competition for attention is lower.
- **Title clarity matters more during peak hours**, when baseline visibility is already high.
- **Moderate emoji usage (1–2 emojis) enhances short titles**, while excessive usage shows diminishing returns.
- Topic tags define the **content context and engagement baseline**, but do not guarantee performance on their own.

Overall, engagement is driven by the **alignment of timing, context, and presentation**, rather than any single tactic.

---

## Results & Practical Impact
After applying these insights to my own posting behavior:
- Engagement rate increased by approximately **25%** compared to prior posts
- A post reached **~3,000–4,000 views within two weeks**

> These results are observational and not from controlled A/B testing, but serve as a real-world sanity check of the framework’s usefulness.

---

## Generalization
While this analysis focuses on programming-related content on RedNote, the framework is applicable to:
- Other content domains on RedNote
- Other feed-based social media platforms

The core idea is to combine:
1. Non-linear modeling to identify structural dependencies
2. Conditional analysis to translate insights into actionable strategies

---

## Limitations
- RedNote does not publicly expose impression or exposure data
- Only the author can view their own post-level analytics
- Follower count of post authors is not available due to platform and scraping constraints
- Results are correlational rather than causal

Future work could incorporate controlled experiments or platform-level exposure metrics.

---

## Tools
Python, pandas, scikit-learn, seaborn, matplotlib, Jupyter Notebook

## Author & Attribution
This project was independently developed by **[Iris Xia]**.

All analyses, code, and visualizations are original.  
Reuse or adaptation is permitted with proper attribution.
