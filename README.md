# CS503 — Data Visualization — HW4

Coursework for **Data Visualization (CS503)**, Department of Computer Science, Bishop's University.

## Map, network and data visualization of US COVID-19

**Hypothesis:** spatial distance between US states correlates with the number of COVID-19 cases
reported. This project tests that hypothesis with a state-similarity network, community detection,
and a geographic heatmap.

The solution is in [`HW4.ipynb`](HW4.ipynb).

## What the notebook covers

1. Compute **TNC** (total confirmed cases) and **TND** (total deaths) per state from the daily
   county-level data.
2. Save those totals to [`state_covid_totals.csv`](state_covid_totals.csv).
3. Build an **affinity matrix** `A` from each state's `[TNC, TND]` vector using a Gaussian kernel
   with free parameter σ.
4. Threshold it into an **adjacency matrix** `B` (`A ≥ 0.5`).
5. Build the graph with **NetworkX**.
6. Draw it with nodes labelled by state initials.
7. Detect **communities** (Louvain) and visualize the clusters.
8. Repeat community detection for several values of σ.
9. Export the graph for **Gephi** (`covid_state_graph.gexf`, `gephi_nodes.csv`).
10. A **geographic heatmap** (`covid_state_heatmap.html`, via folium) plus a discussion of whether
    geographically close states show similar case counts.

## Finding

The communities group states by similar case/death magnitude, not by geography: neighbouring states
often fall in different communities while distant states share one, and the largest states
(California, Texas, Florida, New York) stay isolated because no other state is numerically close.
The evidence does not support the hypothesis; population size explains the case counts far better
than spatial distance.

## Note on Task 9 (Gephi)

Gephi is a desktop application and is used outside the notebook. The notebook exports the graph as
`covid_state_graph.gexf` so it can be loaded directly into Gephi for layout and modularity-based
community detection.

## Running it

```bash
pip install numpy pandas matplotlib networkx scikit-learn folium
jupyter notebook HW4.ipynb
```

## Files

| File | Description |
|------|-------------|
| `HW4.ipynb` | Full solution (Tasks 1–10) |
| `HW4.pdf` | Assignment description |
| `us_counties_covid19_daily.csv` | Source dataset (daily county-level COVID-19 counts) |
| `state_covid_totals.csv` | Computed per-state TNC and TND (Task 2 output) |
| `covid_state_graph.gexf`, `gephi_nodes.csv` | Graph exports for Gephi (Task 9) |
| `covid_state_heatmap.html` | Geographic heatmap (Task 10 output) |
