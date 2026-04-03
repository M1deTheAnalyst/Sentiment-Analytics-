# Sentiment Dashboard Analytics

> A 2-page Power BI dashboard suite that tracks social media sentiment trends, platform engagement, and geographic distribution across categories and time periods.

<img width="1544" height="1735" alt="Sentiment Analytics Dashboard" src="https://github.com/user-attachments/assets/75e1d75f-564b-4b35-ac25-2b9e48568057" />

---

## 📋 Table of Contents

- [Overview](#overview)
- [Dashboard Pages](#dashboard-pages)
  - [Sentiment Health & Trends](#1-sentiment-health--trends)
  - [Platform & Geographic Intelligence](#2-platform--geographic-intelligence)
- [Key Metrics & KPIs](#key-metrics--kpis)
- [Relationship Model](#Relationship-model)
- [Dataset Schema](#dataset-schema)
- [File Structure](#file-structure)
- [Getting Started](#getting-started)
- [Prerequisites](#prerequisites)
- [Usage & Filters](#usage--filters)
- [Insights Summary](#insights-summary)

---

## Overview

The **Sentiment Dashboard Analytics** solution is a Power BI dashboard built to monitor social media sentiment across platforms, geographies, and time periods. It enables marketing teams, community managers, and social listening analysts to track how audiences feel, where engagement peaks, and how sentiment shifts month over month.

### 🎯 Business Objectives

- Track the volume and distribution of Positive, Negative, and Neutral sentiment over time
- Identify which platforms and countries generate the highest engagement
- Monitor month-over-month sentiment shifts to detect emerging trends or brand crises
- Understand what time of day and day of week drives the most audience activity
- Benchmark platform performance by engagement and sentiment composition

---

## Dashboard Pages

### 1. Sentiment Health & Trends

> *Tracks how sentiment categories evolve over time and how engagement compares across sentiment types and platforms.*

<img width="1542" height="867" alt="Sentiment Health   Trends Dashboard" src="https://github.com/user-attachments/assets/871a8128-c33b-4c5c-8522-44aca4221c4b" />

#### KPI / Slicer Filters

| Filter | Options |
|--------|---------|
| **Year / Month** | Date range selector |
| **Country** | All countries in dataset |
| **Platform** | All platforms in dataset |

#### Visuals

**Sentiment Category by Day — Line Chart**
- Tracks daily volume of Positive, Negative, and Neutral posts across the selected date range
- Useful for spotting spikes in negative sentiment or viral positive moments

**Total Sentiments by Sentiment Category — Donut Chart**
- Proportional breakdown of Positive, Negative, and Neutral post volumes across the full dataset
- Provides a quick health snapshot of overall audience tone

**Average Engagement by Sentiment Category — Clustered Bar Chart** *(Drill-down to Platform)*
- Compares average engagement scores per sentiment category
- Drill-down reveals which platforms amplify each sentiment type most

**Sentiment Category by Month — Clustered Column Chart** *(Drill-down to Platform)*
- Monthly trend of Positive post volume with platform drill-down capability
- Supports spotting seasonal patterns and campaign impact periods

**Sentiment vs. Engagement — Clustered Column Chart**
- Maps raw engagement counts against sentiment categories for a quick correlation view

**Year-over-Year Comparison KPI Charts, with MoM Comparision as Tooltip (×4)**
- **Positive Posts vs. Previous Year** — tracks whether positivity is growing
- **Neutral Posts vs. Previous Year** — monitors baseline/passive audience activity
- **Negative Posts vs. Previous Year** — early warning for sentiment degradation
- **Average Engagement vs. Previous Year** — compares current year engagement against the prior year

---

### 2. Platform & Geographic Intelligence

> *Analyses how engagement and sentiment distribute across platforms and countries, and identifies peak activity hours.*

<img width="1544" height="867" alt="Platform   Geographic Intelligence Dashboard" src="https://github.com/user-attachments/assets/3395f0d5-cc4a-4626-a68a-09a591a86ec6" />

#### KPI Cards

| Card | Purpose |
|------|---------|
| **Top Platform** | The platform with the highest overall presence |
| **Highest Engagement Platform** | Platform generating the most average engagement |
| **Most Positive Platform** | Platform with the highest share of positive posts |
| **Most Negative Platform** | Platform with the highest share of negative posts |

#### Visuals

**Engagement by Platform — Clustered Bar Chart** *(Drill-down to Sentiment Category)*
- Ranks platforms by total engagement volume
- Drill-down reveals sentiment composition per platform

**Average Engagement by Hour — Line Chart**
- Tracks when audiences are most active throughout the day
- Enables optimal posting time strategy

**Engagement by Day — Clustered Column Chart** *(Drill-down to Sentiment Category)*
- Shows which days of the week generate the most engagement
- Drill-down surfaces whether peak days skew positive or negative

**Sentiment by Platform — Clustered Bar Chart** *(Drill-down to Country)*
- Breaks down Positive, Negative, and Neutral post counts per platform
- Drill-down allows geographic attribution of platform sentiment

**Sentiment by Country — Clustered Bar Chart** *(Drill-down to Platform)*
- Ranks countries by sentiment composition
- Drill-down reveals which platforms dominate each country's conversation

---

## Key Metrics & KPIs

| KPI | Definition |
|-----|-----------|
| **Positive Posts** | Count of posts classified as positive sentiment |
| **Negative Posts** | Count of posts classified as negative sentiment |
| **Neutral Posts** | Count of posts classified as neutral sentiment |
| **Average Engagement** | Mean engagement score (likes, shares, comments) across posts |
| **Engagement** | Total engagement volume for a given dimension |
| **Top Platform** | Platform with the highest activity volume |
| **Highest Engagement Platform** | Platform with the highest average engagement per post |
| **Most Positive Platform** | Platform with the greatest proportion of positive sentiment |
| **Most Negative Platform** | Platform with the greatest proportion of negative sentiment |
| **YoY Comparison** | Current year value vs. prior year (used for Positive, Negative, Neutral, and Average Engagement) |

---

## Relationship Model

| From (FK)                      | To (PK)                        | Join Column        |
|--------------------------------|--------------------------------|--------------------|
| Fact_Sentiment.CountryID       | Dim_Location.CountryID         | CountryID          |
| Fact_Sentiment.Date            | DateTable.Date                 | Date               |
| Fact_Sentiment.PlatformID      | Dim_Platform.PlatformID        | PlatformID         |
| Fact_Sentiment.SentimentID     | Dim_Sentiment_Type.SentimentID | SentimentID        |
| Fact_Sentiment.UserID          | Dim_user.UserID                | UserID             |
  
---

## Dataset Schema

| Column | Type | Description |
|--------|------|-------------|
| `Day` | Date/String | Day-level date dimension for trend analysis |
| `Month` | String/Integer | Month dimension for MoM comparisons |
| `Year` | Integer | Year dimension for period filtering |
| `HourLabel` | String | Hour of day label (e.g., "08:00", "14:00") |
| `Platform` | String | Social media platform (Twitter, Instagram, Facebook) |
| `Country` | String | Geographic origin of the post/activity |
| `SentimentCategory` | String | Positive / Negative / Neutral |
| `Positive Posts` | Integer | Count of positive-sentiment posts |
| `Negative Posts` | Integer | Count of negative-sentiment posts |
| `Neutral Posts` | Integer | Count of neutral-sentiment posts |
| `Engagement` | Numeric | Raw engagement metric per post or group |
| `Average Engagement` | Numeric | Aggregated average engagement |
| `positive from previous year` | Numeric | Prior year positive post count for YoY tracking |
| `negative from previous year` | Numeric | Prior year negative post count for YoY tracking |
| `neutral from previous year` | Numeric | Prior year neutral post count for YoY tracking |
| `avg. engagement from previous year` | Numeric | Prior year average engagement for YoY tracking |
| `Top Platform` | String/Measure | DAX measure identifying leading platform |
| `Highest Engagement Platform` | String/Measure | DAX measure identifying top engagement platform 
| `Most Positive Platform` | String/Measure | DAX measure identifying most positive platform |
| `Most Negative Platform` | String/Measure | DAX measure identifying most negative platform |

---

## File Structure

```
sentiment-dashboard/
│
├── 📊 Sentiment_Dashboard.pbix          # Main Power BI file
│
├── 📁 screenshots/
│   ├── sentiment-health-trends.jpg
│   └── platform-geographic-intelligence.jpg
|
├── 📂 Sentiment_Dataset.xlsx      # Source data
│
└── 📄 README.md                         # This file
```

---

## Getting Started

### Prerequisites

| Tool | Version | Purpose |
|------|---------|---------|
| [Power BI Desktop](https://powerbi.microsoft.com/desktop/) | Latest | Open & edit `.pbix` |
| Microsoft Excel | 2016+ | View/edit source dataset (if applicable) |

### Installation & Setup

1. **Clone or download the repository**
   ```bash
   git clone https://github.com/your-username/sentiment-dashboard.git
   cd sentiment-dashboard
   ```

2. **Open the dashboard**
   - Launch **Power BI Desktop**
   - Go to `File → Open` and select `Sentiment_Dashboard.pbix`

3. **Verify data source connection**
   - Navigate to `Home → Transform Data → Data Source Settings`
   - Update the path to your source dataset if prompted
   - Click `Refresh` to load the latest data

4. **Refresh data**
   ```
   Home → Refresh
   ```

---

## Usage & Filters

The dashboard includes slicers on both pages supporting the following filters:

- 📅 **Year / Month** : Filter by specific month or year
- 🌍 **Country** : Focus on a specific geographic market
- 📱 **Platform** : Isolate performance by social media platform

### Navigation

Use the **Page Navigator** (available on both pages) to switch between:
- `Sentiment Health & Trends` — Sentiment overview & YoY tracking
- `Platform & Geographic Intelligence` — Platform rankings, hour/day analysis & country breakdown

### Drill-Down Interactions

Several visuals support drill-down for deeper analysis:

| Visual | Primary | Drill-Down |
|--------|---------|------------|
| Avg. Engagement by Sentiment Category | Sentiment Category | Platform |
| Sentiment Category by Month | Month | Platform |
| Engagement by Platform | Platform | Sentiment Category |
| Engagement by Day | Day | Sentiment Category |
| Sentiment by Platform | Platform | Country |
| Sentiment by Country | Country | Platform |

---

## Insights Summary

1. **Audience is overwhelmingly positive** : **11.9%** of all posts are Neutral, **50.89%** are Positive, and only **37.21%** are Negative. Less than 1 in 3 posts carry negative sentiment — a strong brand health signal.

2. **Positive posts drive significantly more engagement** : Positive content averages **68.6** engagement points (Likes + Retweets) versus just **50.0** for Negative posts — a **37%** engagement premium for positive sentiment. Negativity gets noticed less, not more.

3. **Instagram is the highest-engagement platform** Instagram leads with an average of **67.7** engagement per post and the highest total engagement at **17,464**, outperforming both Twitter **(62.4 avg)** and Facebook **(62.8 avg)**. It's also the most positive platform, with **37.2%** of its posts classified as positive.
   
5. **Twitter carries the most negative sentiment** : Despite ranking second in total engagement, twitter has the highest negative post rate at **36.50%**, compared to Facebook's **29.41%**. Instagram is close behind Twitter at **34.19%**, making both worth monitoring for sentiment dips.
   
6. **11 PM is your peak engagement window** : Posts published at 11 PM (Hour 23) generate the highest average engagement at **85.0**, closely followed by 5 AM **(83.0)** and 10 PM **(75.9)**. Your audience is most active outside of standard business hours.
   
7. **United States dominates volume but Canada punches above its weight** United States contributes the most posts **(188)** with a **46.3%** positive rate. Canada, with **135** posts, holds a **40.7%** positive rate almost matching the United States while India and Australia trail with lower positive proportions.

---

## Author

**M1deTheAnalyst**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/m1detheanalyst)

---

*Built with ❤️ using Power BI | Data-driven decisions for modern social media teams*
