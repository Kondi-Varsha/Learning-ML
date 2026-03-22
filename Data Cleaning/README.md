# Airbnb NYC Listings — Data Cleaning

## Introduction
Airbnb is a global platform connecting property owners (hosts) 
with travelers looking for short-term stays.

This dataset contains Airbnb listings from New York City with 
details like host information, location, room types, pricing, 
availability, and guest reviews — originally across 26 columns 
and 102,599 rows of messy real-world data.

---

## Approach
Before cleaning, the dataset was first **understood thoroughly**:
- What each column means
- Which columns are important vs redundant
- What data quality issues exist

Only then cleaning was performed — purposefully, not blindly.

---

## Dataset
- **Source**: Airbnb NYC Open Data
- **Original Shape**: 102,599 rows × 26 columns
- **Final Shape**: 102,058 rows × 20 columns

---

## Issues Found & Fixed

| Issue | Action Taken |
|---|---|
| 541 duplicate rows | Removed using `drop_duplicates()` |
| `$` sign in price & service fee | Stripped using `str.replace()` |
| Missing values in multiple columns | Filled using mode/mean — not dropped blindly |
| `availability 365` had values > 365 | Capped using `clip(upper=365)` |
| `minimum nights` had values > 365 | Capped using `clip(upper=365)` |
| Typos in neighbourhood group (`brookln`, `manhatan`) | Fixed using `str.replace()` |
| Inconsistent column names | Standardized to lowercase with spaces |
| Useless columns (`license`, `house_rules`, `country`, etc.) | Dropped |
| Float columns converted to int | Used `astype(int)` for cleaner data |
| Text columns standardized | Applied `.str.strip().str.title()` |

---

## Columns Dropped
- `host id` — not needed for analysis
- `country` & `country code` — all same value (United States)
- `license` — 99.99% missing
- `house_rules` — free text, not useful for analysis
- `last review` — too many nulls (15,000+)

---

## Tools Used
- Python
- Pandas
- NumPy

---

## Key Learnings
- Always understand the dataset before cleaning
- Never blindly drop nulls — check % missing first
- Use `clip()` instead of dropping outliers when data is valid
- Fixing typos and standardizing text is as important as handling nulls