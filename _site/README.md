# Nivest India - Stock Research Reports

A Jekyll-based website for publishing comprehensive stock research reports and investment analysis for Indian markets.

## URL Structure

Research reports follow this clean URL pattern:
```
/stock-name/YYYYMMDD/
```

**Examples:**
- `/bajfinance/20250822/` - Bajaj Finance report from August 22, 2025
- `/reliance/20250825/` - Reliance Industries report from August 25, 2025
- `/tcs/20250830/` - TCS report from August 30, 2025

## Creating New Research Reports

### Option 1: Use the Generator Script (Recommended)

```bash
./scripts/generate-research-report.sh "TICKER" "YYYY-MM-DD" "Company Name"
```

**Example:**
```bash
./scripts/generate-research-report.sh "RELIANCE" "2025-08-25" "Reliance Industries"
```

This will create: `_posts/2025-08-25-reliance.md` with URL: `/reliance/20250825/`

### Option 2: Manual Creation

1. Create a new file in `_posts/` with format: `YYYY-MM-DD-ticker.md`
2. Add the front matter with custom permalink:

```yaml
---
layout: research
title: "Company Name Ltd (TICKER) - Comprehensive Stock Research Report"
date: YYYY-MM-DD 12:00:00 +0530
permalink: /ticker/YYYYMMDD/
categories: [Stock Research, Sector Name, Sub-sector]
tags: [TICKER, Company Name, Sector, Stock Analysis, Investment Research]
author: "Nivest India Research Team"
excerpt: "Brief description of the research report and key findings."
ticker: "TICKER"
sector: "Sector Name"
current_price: "₹XXX.XX"
market_cap: "₹X,XX,XXX Cr"
recommendation: "BUY/HOLD/SELL"
target_price: "₹XXX (12 months)"
risk_level: "Low/Medium/High"
---
```

## File Naming Convention

- **Filename**: `YYYY-MM-DD-ticker.md`
- **URL**: `/ticker/YYYYMMDD/`
- **Example**: `2025-08-22-bajfinance.md` → `/bajfinance/20250822/`

## Features

- **Professional Layout**: Custom research layout with stock information cards
- **Responsive Design**: Mobile-friendly interface
- **SEO Optimized**: Proper meta tags and descriptions
- **Easy Navigation**: Browse by sector, recommendation, or view all reports
- **RSS Feed**: Automatic feed generation for subscribers

## Development

```bash
# Install dependencies
bundle install

# Build the site
bundle exec jekyll build

# Serve locally
bundle exec jekyll serve --host 0.0.0.0 --port 4000
```

## Site Structure

```
/
├── / (homepage with latest research)
├── /research/ (all research reports)
├── /about/ (research methodology)
├── /stock-name/YYYYMMDD/ (individual research reports)
└── /feed.xml (RSS feed)
```

## Research Report Template

Use the template in `_research_templates/sample-research-report.md` as a starting point for new reports.

## License

This project is for educational and informational purposes only. Research reports should not be considered as investment advice.

