# Patrol Field Effort

Analyzes patrol activity within a study area and produces a dashboard summarizing field effort across three spatial metrics.

## What it does

1. **Fetches patrol data** from an EarthRanger connection for a specified time range (completed patrols only).
2. **Builds patrol trajectories** from the raw observations and reprojects them into a metric CRS (EPSG:3857).
3. **Creates an analysis grid** over the study area (default 1 km cells, clipped to the AOI boundary).
4. **Computes three field effort metrics** for each grid cell:
   - **Days since last patrol visit** — how recently rangers passed through each cell.
   - **Dwell time (hours)** — total time rangers spent inside each cell.
   - **Linear time density** — patrol route coverage expressed as a percentile across the grid.
5. **Bins and colors** each metric using natural-breaks classification (5 classes) with a Red–Yellow–Green palette; unvisited cells are grey.
6. **Calculates summary statistics**: total number of patrols, total distance (km), and spatial patrol coverage (%).
7. **Generates an operational days table** grouped by ranger ID and name.
8. **Assembles a dashboard** with:
   - Three stat cards (total patrols, distance, coverage)
   - Three interactive maps (days since visit, dwell time, linear time density)
   - One sortable/filterable operational summary table

## Outputs

| File | Description |
|---|---|
| `days_since_patrol_visit.gpkg` | Grid with days-since-visit stats |
| `time_spent_per_cell.gpkg` | Grid with dwell time (hours) per cell |
| `patrols_linear_time_density.gpkg` | Grid with linear time density percentiles |
| `er_spatial_file.gpkg` | Study area boundary |
| `patrol_observations.gpkg` | Raw patrol observation points |
| `patrol_trajectories.gpkg` | Patrol trajectory lines |
| `patrol_operational_days.csv` | Operational days per ranger |
| `days_since_patrol_visit_map.html` | Interactive days-since-visit map |
| `time_spent_per_grid_map.html` | Interactive dwell time map |
| `ltd_patrols_map.html` | Interactive linear time density map |

## Inputs

| Parameter | Description |
|---|---|
| EarthRanger connection | Source system for patrol data |
| Time range | Start and end dates for the analysis period |
| Area of interest | Spatial feature(s) defining the study area |
| Grid cell size | Cell size in metres (default 1000 m) |
| Groupers | Optional grouping variables for segmented analysis |
| Base maps | Background tile layers for the maps |
