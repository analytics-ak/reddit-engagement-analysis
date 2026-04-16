<div align="center">

# Reddit Community Engagement Analysis

**Python | Pandas | Matplotlib | Seaborn | Scikit-learn**

Analyzed 4.5 million Reddit posts across 35 tags to find which topics actually get engagement, which popular topics are underperforming, and what kind of language separates high-scoring posts from the rest.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-11557C)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13-4C72B0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/analytics-ak/reddit-engagement-analysis/blob/main/reddit_engagement_analysis.ipynb)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/analytics-ak/reddit-engagement-analysis/main?labpath=reddit_engagement_analysis.ipynb)

</div>

---

## Problem Statement

Community platforms have millions of posts but only a handful get any real attention. Knowing which topics are popular isn't enough — some popular topics get tons of posts but barely any reaction, while smaller topics punch way above their weight.

This project answers three questions:

- **Which topics consistently get high engagement — not just on average, but reliably?**
- **Why do some popular topics attract lots of posts but very little reaction?**
- **What kind of language shows up in high-scoring posts that doesn't appear in low-scoring ones?**

---

## What This Project Does

- Cleaned and deduplicated a **4.5 million row** Reddit dataset
- Used a validated **200K sample** for efficient analysis without losing accuracy
- Showed why averages are misleading for this data and used median + IQR instead
- Filtered out small tags to avoid drawing conclusions from noise
- Built a **4-quadrant framework** that classifies every tag by volume and engagement
- Compared the actual words used in high vs low engagement posts
- Deep-dived into "Work" — a tag that's heavily posted but poorly engaged — to understand why

---

## The Dataset

- **Source:** [Kaggle — Reddit Labeled Post Data](https://www.kaggle.com/datasets/vaibhavsxn/reddit-comments-labeled-data)
- **Rows:** ~4.6 million
- **Columns:** 4 (score, body, Topic, Tag)
- **Tags:** 35 categories (Teenage, Work, Gender, Games, Social, etc.)
- **Topics:** 40 numeric IDs

Each row contains a Reddit post's score (upvotes), text body, topic ID, and a readable tag label.

---

## Why This Matters

- Helps content or community teams focus on topics that consistently perform, not just ones that go viral once
- Spots high-volume topics where posting effort is being wasted because nobody reacts
- Shows that engagement depends on how something is written, not just what topic it falls under

---

## Sampling Approach

The full dataset has 4.3 million clean rows. Running every chart on that is unnecessary. A random sample of 200,000 rows was taken and validated against the full data.

Mean and median scores for the top 5 tags match almost exactly between the sample and the full dataset. Tag proportions closely match the full dataset. The sample holds — all analysis from this point uses it.

---

## Key Findings

### 1. Most Posts Get Almost No Attention

The score distribution is extremely skewed. Median score is 2, mean is 6.2 — pulled up by a few viral posts. 90% of all posts score 8 or below. This is why the analysis uses median instead of mean wherever possible — the average is misleading.

![Score Distribution](images/score_distribution.png)

---

### 2. Tag Rankings Change When You Use the Right Metric

When you rank tags by mean score, Teenage comes out on top at 10.58. But the median for almost every tag is 2. The real difference between tags shows up in the mean and IQR — some tags produce more high-scoring posts than others, even though the typical post in every tag scores about the same.

Tags with fewer than 500 posts were filtered out to keep the rankings reliable.

| Tag | Posts | Mean Score | Median | IQR |
|-----|-------|-----------|--------|-----|
| Teenage | 20,541 | 10.58 | 2.0 | 3.0 |
| Gender | 10,341 | 8.68 | 2.0 | 4.0 |
| International | 7,653 | 8.32 | 2.0 | 4.0 |
| Nature | 4,842 | 8.06 | 2.0 | 3.0 |
| Photography | 2,215 | 8.03 | 2.0 | 2.5 |

---

### 3. Some Tags Are Consistent, Others Are Spiky

The boxplot below shows the score spread for the top 10 tags by volume. Gender and International have wide boxes — their engagement is all over the place. Work and TV are tight and low — consistently weak.

A wide box doesn't mean the tag is bad. It means some posts in that tag do really well while most don't. A narrow box that sits low means the tag just doesn't generate much engagement at all.

![Tag Stability](images/tag_stability_boxplot.png)

---

### 4. The 4-Quadrant View — This Is the Main Chart

Every tag with 500+ posts plotted by volume (how many posts) vs engagement (mean score). The quadrant lines are set at the median of each axis.

![Quadrant Chart](images/popularity_vs_engagement_quadrant.png)

Four groups come out of this:

- **Top-right — High Volume + High Engagement:** Teenage, Gender, College. These are the strongest topics. They get posted a lot, and people react to them.
- **Bottom-right — High Volume + Low Engagement:** Work, Games, TV, Social. Tons of posts, but weak response. This is where effort is being wasted.
- **Top-left — Niche + Loved:** Photography, Nature, Treatment. Small audiences but strong reactions. Growth opportunities.
- **Bottom-left — Low Activity:** Hardware, Conversation, Laptops. Not much posting, not much reaction. Lowest priority.

---

### 5. Deep Dive — Why "Work" Underperforms

Work sits in the bottom-right quadrant — one of the most posted tags, but one of the lowest scoring. The quadrant chart flagged it, so we dug in.

Comparing the top 25 words in Work posts vs Teenage posts (the highest engagement tag) tells the story:

![Work vs Teenage Words](images/work_vs_teenage_words.png)

Work posts use more practical and neutral language, while Teenage posts include more personal and day-to-day expressions.

This does not fully explain the engagement gap, but it suggests that posts that feel more personal or relatable may perform better than purely informational ones.

---

### 6. High vs Low Engagement — Same Words, Different Results

This one goes beyond topic-level analysis. ALL posts were split into two groups — top 10% by score and bottom 50% — and the most common words were compared.

![High vs Low Words](images/high_vs_low_engagement_words.png)

The result is interesting: the most common words are almost the same in both groups. "Like," "people," "think," "time," "know" — they show up everywhere.

This tells us something important. Engagement isn't about using specific keywords. It's about how ideas are framed — context, tone, and personal expression matter more than word choice.

---

## What Didn't Separate High From Low

| Factor | Result |
|--------|--------|
| Specific keywords | Same common words appear in both high and low scoring posts |
| Topic ID alone | Topics are just numeric codes — no insight without the Tag labels |

This reinforces that engagement is not driven by simple keyword presence.
---

## Recommendations

Four things a community or content platform should do based on this data:

**1. Put more weight behind high-engagement topics**
Tags like Teenage, Gender, and International consistently drive strong reactions. Give them more visibility, better placement, and priority in feeds.

**2. Rethink high-volume, low-engagement areas**
Work, Games, and TV get lots of posts but weak scores. The language in these posts is flat and factual. Encouraging storytelling or opinion-based formats in these areas could help.

**3. Grow the niche-but-loved topics**
Photography, Nature, and Treatment have small audiences but strong engagement. Promoting them to a wider audience could bring in users who actually interact, not just scroll.

**4. Focus on writing style, not just topic**
Engagement is not explained by keywords alone. The analysis suggests that how content is written — including tone and framing — may play an important role alongside topic selection.

---

## Limitations

- **Score is not sentiment.** Reddit upvotes measure popularity and agreement, not whether the post is positive or negative. A highly upvoted post could be angry, sad, or funny.
- **Dataset is pre-labelled.** The Tag and Topic columns were assigned before this analysis, not discovered from the text.
- **Score doesn't capture full engagement.** Comments, shares, saves, and awards are all forms of engagement that this data doesn't include.
- **Sample vs population.** Analysis uses a 200K sample from 4.3M rows. Validation shows it holds, but edge cases in very small tags may not be fully captured.
- **No time dimension.** No timestamps in the data, so we can't track trends or seasonal patterns.

---

## Conclusion

Most Reddit posts get almost no attention — the median score is 2, and 90% of posts score 8 or below. The few posts that do well tend to come from the same handful of topics.

The biggest problem area is tags like Work and Games — people post a lot, but nobody really reacts. When you look at the language, it makes sense. These posts are plain and factual. The tags that do well (like Teenage and Gender) have Posts that feel more personal or experience-driven, tend to show higher engagement, while purely informational posts often receive weaker responses.

For any platform trying to improve engagement, the answer isn't just picking the right topic. It's about how people write. Posts that feel personal get more reaction than posts that just share information.

---

## Tools & Libraries

| Tool | Used For |
|------|----------|
| Python | Data cleaning, feature engineering, analysis |
| Pandas | Grouping, filtering, aggregation |
| NumPy | Numerical operations |
| Matplotlib | All charts and visualizations |
| Seaborn | Statistical plots and styled visuals |
| Scikit-learn | CountVectorizer for word frequency analysis |
| Jupyter Notebook | Full end-to-end analysis |

---

## Project Structure

```
reddit-engagement-analysis/
│
├── reddit_engagement_analysis.ipynb      # Full analysis notebook
├── README.md                              # This file
│
└── images/                                # All charts from the notebook
    ├── score_distribution.png
    ├── tag_stability_boxplot.png
    ├── popularity_vs_engagement_quadrant.png
    ├── work_vs_teenage_words.png
    └── high_vs_low_engagement_words.png
```

---

## How to Run This Project

1. Clone this repo
   ```bash
   git clone https://github.com/analytics-ak/reddit-engagement-analysis.git
   ```
2. Install the required libraries
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn
   ```
3. Open the notebook
   ```bash
   jupyter notebook reddit_engagement_analysis.ipynb
   ```
4. Run all cells — charts will generate automatically

---

## Profile & Dataset

* 🔗 **LinkedIn:** [View My Profile](https://www.linkedin.com/in/analytics-ashish/)
* 📂 **Dataset:** [Reddit Labeled Post Data on Kaggle](https://www.kaggle.com/datasets/vaibhavsxn/reddit-comments-labeled-data)
* 💻 **GitHub Repository:** [Reddit Engagement Analysis](https://github.com/analytics-ak/reddit-engagement-analysis/)
* 📘 **Notebook:** [reddit_engagement_analysis.ipynb](https://github.com/analytics-ak/reddit-engagement-analysis/blob/main/reddit_engagement_analysis.ipynb)

<br>

## Author

**Ashish Kumar Dongre**
Data Analyst

- Python | Pandas | Data Analysis
- Focus: **Business-driven data insights**
