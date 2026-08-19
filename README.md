# Istanbul Airbnb Market Analysis (2026)

![Istanbul Cover](visuals/istanbul-cover.jpg)

## Project Overview
This project analyzes Istanbul Airbnb listings to identify what drives listing success using real market data from Inside Airbnb.

The core business question is:
**Why are many listings inactive, and which factors are associated with higher occupancy and revenue?**

## Introduction
Istanbul has thousands of Airbnb listings, but listing availability does not guarantee market performance. This project builds a data-driven market review to understand which listings are active, which are inactive, and what characteristics separate both groups.

## Problem Statement
During early exploration, a large share of listings showed zero estimated occupancy over the previous 365 days. This indicates a performance gap in the market and raises a core business question:
- Why do some listings attract bookings while many others remain inactive?

## Goal
Build an analytical framework that identifies success signals in Istanbul Airbnb listings by measuring:
1. Occupancy activity
2. Revenue potential
3. Price positioning by neighborhood and listing profile

## Factors Used
The analysis focuses on factors with direct business relevance:
- **Location:** `neighbourhood_cleansed`
- **Listing format:** `room_type`, `property_type`
- **Capacity/features:** `accommodates`, `bedrooms`, `beds`, `bathrooms`
- **Host quality:** `host_is_superhost`
- **Demand/engagement:** `number_of_reviews`, `review_scores_rating`
- **Performance targets:** `estimated_occupancy_l365d`, `estimated_revenue_l365d`, `price`

## How the Goal Was Detected from Data
The goal was not assumed before analysis. It was discovered through structured data review:
1. Audit of missing values and dtypes
2. Price outlier detection and correction
3. Distribution checks for occupancy and revenue
4. Active vs inactive segmentation using `estimated_occupancy_l365d`

This process revealed that inactive listings form a major market share, so the project was framed around explaining that gap.

---

## Data Source
- **Source:** Inside Airbnb (Istanbul, Marmara, Turkey)
- **Snapshot:** 30 June 2026
- **Main file used for analysis:** `listings.csv.gz`
- **Supporting files:** `calendar.csv.gz`, `reviews.csv.gz`, `neighbourhoods.csv`, `neighbourhoods.geojson`

## Data Headers (Column Groups)
To keep analysis readable, headers were grouped by role:

### Listing identity
- `id`

### Location headers
- `neighbourhood_cleansed`

### Listing type headers
- `room_type`
- `property_type`

### Price and performance headers
- `price`
- `estimated_occupancy_l365d`
- `estimated_revenue_l365d`

### Capacity headers
- `accommodates`
- `bedrooms`
- `beds`
- `bathrooms`

### Host and reputation headers
- `host_is_superhost`
- `number_of_reviews`
- `review_scores_rating`

## Header Relationships
- `id` is the unique listing key.
- `price` + `estimated_occupancy_l365d` jointly influence `estimated_revenue_l365d`.
- `room_type`, `property_type`, and capacity headers explain listing positioning.
- `host_is_superhost` and review metrics capture trust and service quality.
- `neighbourhood_cleansed` captures geographic demand effects.

---

## Repository Structure
```text
Istanbul-Airbnb-Analysis/
├── data/
│   └── raw/
│       ├── listings.csv.gz
│       ├── calendar.csv.gz
│       ├── reviews.csv.gz
│       ├── reviews.csv
│       ├── neighbourhoods.csv
│       └── neighbourhoods.geojson
├── visuals/
│   ├── istanbul-cover.jpg
│   ├── occupancy_by_neighborhood.png
│   ├── revenue_by_neighborhood.png
│   ├── room_type_comparison.png
│   ├── superhost_comparison.png
│   └── price_distribution.png
├── Istanbul-Airbnb-Analysis.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Analysis Workflow
1. Data loading and audit
2. Missing value and type checks
3. Price cleaning and outlier treatment
4. Active vs inactive market segmentation
5. Neighborhood performance comparison
6. Room type and superhost impact analysis
7. Visualization and final business insights

---

## Data Review (What the data revealed)
- Initial listings: **26,631**
- Cleaned analytical sample: **23,467**
- Key quality issues found:
  - Missing values in `beds`, `bathrooms`, `review_scores_rating`
  - Extreme price outliers that distort averages
- Key segmentation:
  - **Active listings:** occupancy > 0
  - **Inactive listings:** occupancy = 0

---

## Key Findings
1. **Market concentration:** Active demand is heavily concentrated in a few areas, especially Beyoglu.
2. **Room type effect:** Active listings are mostly entire homes/apartments.
3. **Host quality effect:** Superhost share is much higher in active listings than inactive listings.
4. **Price-performance split:** Active listings have a much higher median price than inactive listings.

---

## Visualizations
### Median Occupancy by Neighborhood
![Occupancy by Neighborhood](visuals/occupancy_by_neighborhood.png)

### Median Revenue by Neighborhood
![Revenue by Neighborhood](visuals/revenue_by_neighborhood.png)

### Room Type: Active vs Inactive
![Room Type Comparison](visuals/room_type_comparison.png)

### Superhost: Active vs Inactive
![Superhost Comparison](visuals/superhost_comparison.png)

### Price Distribution: Active vs Inactive
![Price Distribution](visuals/price_distribution.png)

---

## Business Recommendations
- Prioritize neighborhoods with proven occupancy performance.
- Favor listing formats aligned with active demand (entire home/apt).
- Improve host trust signals (Superhost pathway, response quality).
- Use neighborhood-aware pricing instead of one generic pricing strategy.

---

## Run the Project
```bash
pip install -r requirements.txt
jupyter notebook
```

Open:
- `Istanbul-Airbnb-Analysis.ipynb`

---

## GitHub Pages (HTML Project Page)
To publish a live project page:
1. Export the notebook to HTML.
2. Save it as `index.html` in the repository root.
3. Enable GitHub Pages from the `main` branch (root) in repository settings.

Live URL format:
`https://siavashrko.github.io/Istanbul-Airbnb-Analysis/`
