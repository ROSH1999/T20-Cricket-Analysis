# 05 · Cricket T20 Analytics — Reading a Ball-by-Ball Dataset

The most fun of the five. Ball-by-ball data teaches you to aggregate at several
levels at once (match → innings → over → ball) and to be careful about **denominators**:
strike rate is per 100 balls, economy is per 6 balls, and mixing them up is the
number one rookie mistake in cricket analytics.

## Folder contents
```
05-cricket-t20-analytics/
├── t20_batting_analysis.ipynb   <- start here
└── data/
    ├── t20_matches.csv          <- 2 rows per match (one per innings)
    └── t20_deliveries.csv       <- ball-by-ball for 3 matches (the deep-dive file)
```

## Data model
| File | Grain | Key columns |
| --- | --- | --- |
| `t20_matches.csv` | one row per innings | `match_id`, `innings`, `runs`, `wickets`, `run_rate`, `winner`, `victory_margin` |
| `t20_deliveries.csv` | one row per ball | `match_id`, `innings`, `over`, `ball`, `batter`, `bowler`, `total_runs`, `is_wicket` |

> The deliveries file is deliberately limited to 3 matches so it stays small enough
> to read in seconds. Extend `scripts`/the notebook loop to pull more if you enjoy it.

## What you practise
| Skill | Why it matters |
| --- | --- |
| Multi-level `groupby` + `.agg()` with named aggregations | over-level and phase-level metrics |
| `pd.merge` to combine batting and bowling views | full player profiles |
| `pivot_table` heatmaps | over × match scoring patterns |
| Per-100 / per-over normalisation | comparable player stats |
| Sorting and ranking with ties | leaderboards that survive scrutiny |

## Questions this project answers
1. How does scoring speed change across powerplay, middle and death overs?
2. Who are the top run scorers, and how do strike rate and average trade off?
3. Which bowlers are actually economical once you normalise for overs bowled?
4. Do teams batting first win more often in this sample?
5. What does a "death overs specialist" look like in the numbers?

## Starter challenges
- Compute each batter's runs by phase and identify the specialists.
- Build a 2D scatter (strike rate vs average) with a labelled top-8 only.
- Add a `matchup` analysis: batter vs bowler runs and dismissals.
- Compute a ` Worm` chart per match (cumulative runs by over, wickets marked).
