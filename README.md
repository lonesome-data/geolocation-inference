# Geolocation Inference from Call Detail Records Using K-Means Clustering

Completed as part of the **Naval Postgraduate School** Data Science Professional Certificate (OS4601 Advanced Data Analysis).

## Problem

Given 3 years of Call Detail Records (CDRs) for 10 mobile phone users, infer their likely **residence** and **workplace** locations using only cell tower coordinates and call timestamps.

## Approach

No labeled location data exists — this is an **unsupervised** problem. The solution combines domain heuristics with K-Means clustering:

1. **Temporal segmentation** — calls are partitioned by day-of-week and time-of-day to isolate behavioral regimes
2. **Residence inference** — weekend calls between 0000–0600 ("twilight hours") cluster near home
3. **Workplace inference** — weekday calls between 0730–1700 cluster near work
4. **K-Means (K=2)** — separates the dominant spatial cluster (workplace) from transit/commute towers
5. **Validation** — mean call time per cluster confirms the transit cluster shows earlier timestamps (morning commute)

## Key Findings

- Temporal filtering is essential — raw CDR coordinates are spatially noisy without behavioral context
- K=2 reliably separates workplace from transit across all 10 users
- The transit cluster consistently shows earlier mean call times (~0750), confirming the commute window hypothesis
- Cell tower resolution is the fundamental limiting factor — user location is approximated by the nearest tower

## Dataset

~50,000 CDR records across 10 users over 3 years. Each record includes:
- Caller ID, call date/time, duration
- Day of week
- Cell tower latitude/longitude

## Quickstart

```bash
git clone https://github.com/lonesome-data/OS4601_Advanced_Data_Analysis.git
cd OS4601_Advanced_Data_Analysis
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook cdr_geolocation_analysis.ipynb
```

## Project Structure

```
├── cdr_geolocation_analysis.ipynb   # Analysis notebook (modernized)
├── data/
│   └── CDR.csv                      # Call Detail Records
├── requirements.txt                 # Python dependencies
└── Forester_OS4106_Final_Project.ipynb  # Original 2018 notebook (archived)
```

## License

MIT
