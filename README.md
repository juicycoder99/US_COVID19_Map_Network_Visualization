# US COVID-19 Map and Network Visualization

Geographic heatmap and state-similarity network analysis of US COVID-19 case data, testing whether spatial proximity predicts case counts.

## Map, network and data visualization of US COVID-19

**Hypothesis:** spatial distance between US states correlates with the number of COVID-19 cases
reported. This project tests that hypothesis with a state-similarity network, community detection,
and a geographic heatmap.

The implementation is in [`covid19_map_network_visualization.ipynb`](covid19_map_network_visualization.ipynb).

## What the notebook covers

1. Compute **TNC** (total confirmed cases) and **TND** (total deaths) per state from the daily
   county-level data.
2. Save those totals to [`state_covid_totals.csv`](state_covid_totals.csv).
3. Build an **affinity matrix** `A` from each state's `[TNC, TND]` vector using a Gaussian kernel
   with free parameter σ.
4. Threshold it into an **adjacency matrix** `B` (`A >= 0.5`).
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

## Note on Gephi

Gephi is a desktop application and is used outside the notebook. The notebook exports the graph as
`covid_state_graph.gexf` so it can be loaded directly into Gephi for layout and modularity-based
community detection.

## Running it

```bash
pip install numpy pandas matplotlib networkx scikit-learn folium
jupyter notebook covid19_map_network_visualization.ipynb
```

## Files

| File | Description |
|------|-------------|
| `covid19_map_network_visualization.ipynb` | Full implementation and analysis (Tasks 1–10) |
| `PROJECT_BRIEF.pdf` | Project brief (goals, objectives, outcomes) |
| `us_counties_covid19_daily.csv` | Source dataset (daily county-level COVID-19 counts) |
| `state_covid_totals.csv` | Computed per-state TNC and TND (Task 2 output) |
| `covid_state_graph.gexf`, `gephi_nodes.csv` | Graph exports for Gephi |
| `covid_state_heatmap.html` | Geographic heatmap (Task 10 output) |
