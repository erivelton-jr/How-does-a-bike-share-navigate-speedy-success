<table>
  <tr>
    <td><img src="https://miro.medium.com/v2/resize:fit:1181/1*5aFr82kqA3lsHx-KgwIP3w.jpeg" width="150"/></td>
    <td><h1>How does a bike-share navigate speedy success?</h1></td>
  </tr>
</table>


![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-150458?style=flat&logo=pandas&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-Public-E97627?style=flat&logo=tableau&logoColor=white)
![Google Data Analytics](https://img.shields.io/badge/Google-Data%20Analytics%20Certificate-4285F4?style=flat&logo=google&logoColor=white)

*This project is part of the **Google Data Analytics** course, where I perform typical tasks of a junior data analyst following the data analysis process: **Ask → Prepare → Process → Analyze → Share → Act**.*

---

## Table of Contents

- [Scenario](#scenario)
- [Ask](#ask)
- [Prepare](#prepare)
- [Process](#process)
- [Analyze & Share](#analyze--share)
- [Act](#act)

---

## Scenario

You are a junior data analyst working on the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company's future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.

---

## Ask

According to the finance analysts at Cyclistic, annual members generate significantly more profit than casual riders. As a result, the company's primary business objective is to increase the number of annual memberships by converting existing casual riders into members.

To achieve this goal, the marketing analytics team must first understand the behavioral differences between annual members and casual riders. Identifying these differences will provide data-driven insights to support the development of targeted marketing strategies.

Three key questions will guide the future marketing program:

1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders purchase Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

For this analysis, the focus will be on answering the first question: **How do annual members and casual riders use Cyclistic bikes differently?**

---

## Prepare

### Data source

The data covers the full year of **2025** (January through December), organized as monthly `.csv` files provided by *Motivate International Inc.* under this [license](https://www.divvybikes.com/data-license-agreement).

> **Note:** The raw data files are not included in this repository due to file size constraints. You can download the original `.zip` files directly from the [Divvy trip data portal](https://divvy-tripdata.s3.amazonaws.com/index.html). After downloading, extract them into `data/raw/` following the naming pattern `2025MM-divvy-tripdata.csv`.

### Folder structure

```
data/
├── zipped/    # Downloaded .zip files
└── raw/       # Extracted .csv files (one per month)
```

### Dataset schema

| Column | Description |
|---|---|
| `ride_id` | Unique identifier for each trip |
| `rideable_type` | Bike type: `classic_bike` or `electric_bike` |
| `started_at` | Trip start timestamp |
| `ended_at` | Trip end timestamp |
| `start_station_name` | Name of the departure station |
| `start_station_id` | ID of the departure station |
| `end_station_name` | Name of the arrival station |
| `end_station_id` | ID of the arrival station |
| `start_lat` / `start_lng` | Departure coordinates |
| `end_lat` / `end_lng` | Arrival coordinates |
| `member_casual` | Rider type: `member` or `casual` |

---

## Process

Analysis was performed in **Python** with **Jupyter Notebook**, chosen for its support of iterative exploration and inline documentation.

### Requirements

```
Python 3.10+
pandas
requests
```

Install dependencies:

```bash
pip install pandas requests
```

### Steps

1. **Concatenate** — loaded all 12 monthly files into a single DataFrame (~5.5M rows).
2. **Transform datetime** — parsed `started_at` and `ended_at` columns to `datetime64`.
3. **Feature engineering** — derived `trip_duration_seconds`, `day_of_week`, `date`, `day`, `month`, and `year` from the datetime columns.
4. **Remove nulls** — dropped rows with any `NaN` value. Station name/ID columns had significant missing data (~1.18M rows for start, ~1.24M for end), primarily from electric bikes without docked stations. Rows with missing `end_lat`/`end_lng` (5,535 rows) were also removed. This reduced the dataset from 5.55M to approximately 3.69M clean rows.
5. **Remove invalid trips** — filtered out records where `trip_duration_seconds ≤ 0`.

> **Final dataset:** ~3.69M rows covering January–December 2025.

---

## Analyze & Share

Aggregations and visual analysis were performed in **Tableau**. The interactive dashboard is embedded below and also accessible directly on [Tableau Public](https://public.tableau.com/views/Howdoesabike-sharenavigatespeedysuccess_17739326193670/Painel1?:language=pt-BR&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link).
 
<a href="https://public.tableau.com/views/Howdoesabike-sharenavigatespeedysuccess_17739326193670/Painel1?:language=pt-BR&:display_count=n&:origin=viz_share_link">
  <img src="https://public.tableau.com/static/images/Ho/Howdoesabike-sharenavigatespeedysuccess_17739326193670/Painel1/1.png" alt="Dashboard Tableau" width="100%">

</a>

### Key findings

**1. Trips by Day of Week**
Casual riders concentrate their usage on weekends, while members ride more consistently on weekdays — indicating a leisure vs. commuting split.

**2. Average Trip Duration**
Casual riders average nearly twice the trip duration of members (~1,339s vs. ~740s), reinforcing the recreational use pattern.

**3. Trips by Rideable Type**
Both groups prefer classic bikes. Members show a wider gap between classic and electric usage; casual riders show a smaller difference.

**4. Trips by Month**
Usage peaks in summer and early fall (June–October) for both groups, with a sharp decline in winter months — a strong seasonal pattern.

**5. Start vs. End Trip Heat Map**
Start trips are concentrated in a central hotspot zone (likely tourist and transit hubs), while end trips are dispersed across a wider area of the city.

---

## Act

### Key Insights

| Dimension | Casual Riders | Annual Members |
|---|---|---|
| Peak days | Weekends | Weekdays |
| Trip duration | Longer (~22 min avg) | Shorter (~12 min avg) |
| Peak season | Summer / Fall | Summer / Fall |
| Station usage | Central hotspots | Distributed citywide |

### Why Casual Riders Would Buy Annual Memberships

**Pain points**
- Paying a higher per-ride rate on long, frequent trips.
- High usage during summer accumulates cost quickly.
- Often renting multiple times in a single day or weekend.

**Motivators for purchase**
- Unlimited riding at a flat annual cost.
- No surprise charges — predictable expense.
- Access to exclusive features and priority availability.
- Personalized cost comparison nudges ("you'd save $X with a membership").

### Strategic Action Plan

#### A — Target High-Value Segments
- Casual riders on weekends and during summer.
- Tourists and leisure users near hotspot start stations.

#### B — Trial Memberships
- Offer 1-week or 1-month low-cost trial passes.
- Include an auto-upgrade option at trial end.

#### C — Usage-Based Upgrade Suggestions
- Trigger in-app notifications when a casual rider's spend approaches membership value.
- Example: *"You've spent $X this week — members would pay only $Y."*

### Digital Media Strategy

#### A — Geolocation Ads
- Activate campaigns near top start-station hotspots.
- Messaging: *"Starting a ride? Save more with unlimited trips."*

#### B — Push Notifications / In-App Messaging
- Show personalized savings after 2+ rides in a day or week.

#### C — Remarketing Campaigns
- Google, YouTube, and Instagram ads targeting users who rode in the last 30 days.
- Focus: benefits, savings, and convenience.

### Offers & Incentives
- Seasonal discounts timed to summer peak demand.
- "Summer Unlimited Ride Pass" promotional campaigns.
- Partnerships with hotels, hostels, parks, and tourist operators near hotspot zones.

### Final Recommendation

Cyclistic can maximize annual membership conversions by:
- Targeting casual riders based on observed behavioral patterns (weekends, long trips, summer peaks).
- Offering trial memberships and personalized savings nudges at the right moment.
- Leveraging geolocated and remarketing digital campaigns near high-traffic stations.
- Strengthening operational presence in identified hotspot areas.
