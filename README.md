# tutorsim.org

Project site for **TutorSim-Preview: When Help is Unhelpful — Evaluating AI Tutors for Productive Struggle**. Static site served by GitHub Pages (CNAME: tutorsim.org).

## Local preview

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

## Layout

- `index.html` — the whole page (Ai2-brand styling in `static/css/site.css`)
- `static/js/main.js` — renders the leaderboard table and the two interactive charts from `static/data/*.json`
- `static/data/` — chart data, all checked in (`leaderboard.json`, `latency.json`, `action_distribution.json`). If `action_distribution.json` is ever removed, its section hides itself
- `static/paper/tutorsim-preview.pdf`, `static/animation/index.html` — published copies of the paper and pipeline animation
- `assets/` — **gitignored** source material (paper draft, unreleased blog draft, animation original)

## Refreshing chart data

Results live in a local [allenai/tutorsim](https://github.com/allenai/tutorsim) checkout (the repo gitignores `results/` and `data/taxonomy/`). After running new models:

```sh
python3 scripts/refresh-data.py /path/to/tutorsim
```

This regenerates `static/data/{leaderboard,latency,action_distribution}.json`. The action-distribution figure reads the repo's `analysis/working-paper-20260630/action_taxonomy_distribution.csv` export (currently on the `action_taxonomy_data` branch); pass `--action-csv path/to/action_taxonomy_distribution.csv` to use a copy outside the checkout. Add new models to the `MODELS` list in the script (plus `ACTION_CSV_MODELS`, and `MODEL_STYLE` in `static/js/main.js`). Partial refreshes are fine — missing inputs just skip that JSON.

## TODOs when things go live

- Dataset pill in `index.html` — link when TutorSim-Transcripts-Preview is published
- Blog pill in `index.html` — link when the Ai2 blog post is live
- `static/data/latency.json` — latencies are currently read off the paper's Figure 7 (±0.2s); the refresh script replaces them with exact values from a checkout with results
