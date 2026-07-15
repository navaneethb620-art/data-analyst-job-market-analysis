## Data Analyst Job Market Intelligence: India vs Global

# Project Overview

As a fresher transitioning into a Data Analyst role, I wanted to answer a simple question before investing more time upskilling: does what I've learned (SQL, Python, Excel, Power BI) actually match what employers are hiring for — right now, in India, and globally? Instead of relying on generic advice, I pulled live job posting data from India (via the Adzuna API) and a larger historical dataset of global postings (via Kaggle), cleaned both from scratch, and analyzed them using SQL, Python, and Power BI to find out.

# Business Questions

1. Skill demand comparison — India vs Global
2. City-wise skill demand
3. Skills-per-posting distribution + most common skill pairs
4. Does mentioning specific skills correlate with higher salary?
5. Does skill demand differ by seniority level?
6. Company-level hiring patterns


# Tools Used

1.Python (pandas) 
2.SQL (SQLite) 
3.Power BI 

# Data Sources

-Adzuna API — live India job postings for "Data Analyst" (250 rows, pulled July 2026)
- Kaggle (asaniczka/data-analyst-job-postings) — Global job postings, filtered from 12,894 broad "Analyst" listings down to 2,736 rows specifically matching "Data Analyst" in the title (single-day snapshot, Dec 2023)

# NOTE:
The original raw Kaggle file (~58MB) is not included in this repo due to size; only the cleaned/filtered version is provided. The full raw file can be downloaded from the Kaggle link above.



# Data Cleaning Highlights

 A few highlights:


Caught a truncation bias, not just a missing-data issue: Adzuna's free-tier API returns descriptions capped at ~500 characters. This meant 156/250 postings initially showed "0 skills detected" — investigation confirmed these descriptions were cut off mid-sentence, not genuinely skill-less. This was documented as a limitation rather than reported as a real finding.

- Standardized messy location data using two different techniques depending on scale: Adzuna's 34 unique location strings were manually mapped to known cities (small enough to eyeball); Kaggle's 838 unique locations were instead parsed structurally by comma-count, since manual listing wasn't feasible at that scale.
- Removed unpaid/volunteer postings (e.g., "Volunteer: Wildfire Prevention Data Analyst") that would have skewed the analysis, identified via a "Volunteer:" prefix pattern in job titles.
- Investigated salary anomalies instead of blindly imputing: one row showed a nonsensical ₹15-25 salary range (nulled out as a data error), while 13 separate rows showed salary_min=0 paired with realistic salary_max values — correctly interpreted as "employer didn't disclose a floor," not a real ₹0 salary, and nulled accordingly.
- Filtered out a broad "Analyst" search dataset down to genuine Data Analyst roles — the raw Kaggle data included unrelated titles like Financial Analyst, Malware Analyst, and even Behavior Analyst (BCBA, a therapy role), which were excluded to keep the comparison fair.


# Key Findings

- SQL is the most universally demanded skill in both markets — 25.2% of India postings and 67.5% of Global postings mention it, the highest of any tracked skill in both regions.
- Global postings show substantially higher skill-mention rates across the board than India — though part of this gap likely reflects Adzuna's description truncation rather than a true regional demand difference (see Limitations).
- Most postings ask for a small number of skills at once — after excluding the truncation-affected "0 skills" bucket, the single most common requirement in both markets is just 1 explicitly-mentioned skill, with demand dropping off sharply past 2-3 skills.
- SQL + Python is the most common skill pairing in India (29 postings), while SQL + Tableau and SQL + Python are essentially tied as the top pairing globally (930 and 929 postings respectively).
- Skill demand is broadly similar between Associate and Mid-senior roles globally —once corrected for the ~4x difference in posting volume between the two groups, most skills show only a small gap (e.g., SQL: 68.2% Mid-senior vs 65.2% Associate). The clearest genuine difference is Excel, which Associate-level postings mention more (41.5% vs 33.9%) — suggesting foundational tools remain relevant even at senior levels, and Excel specifically skews toward entry-level roles.
- Bangalore dominates India's Data Analyst hiring, accounting for roughly 30% of all postings in the dataset.


# Limitations

- Adzuna sample size is small (250 rows), and further splitting by skill/salary shrinks group sizes considerably — salary-vs-skill comparisons in particular (~77 rows with disclosed salary) should be read as directional, not statistically robust.
- Adzuna descriptions are truncated (~500 characters), which likely undercounts true skill-mention rates — all Adzuna skill percentages should be treated as a lower bound, not an exact figure.
- Kaggle data is a single-day snapshot (December 2023), not a rolling historical dataset — it reflects one point in time, not a trend over time.
- The two datasets differ in region, source, and collection method (live API vs. pre-scraped LinkedIn data), so direct India-vs-Global comparisons should be read as broadly indicative rather than perfectly like-for-like.

# What's Next

This analysis validates my current learning path — SQL and Python show consistent demand across both markets and across seniority levels, so I'm prioritizing deeper SQL and Python practice next, alongside Power BI dashboarding (already a relative strength based on this project). Excel remains relevant for entry-level roles specifically, reinforcing that it's still worth keeping sharp even while building toward more advanced tools



