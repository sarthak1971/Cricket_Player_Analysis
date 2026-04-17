# 🏏 Cricket Player Analytics — Power BI Dashboard

> **Project Sportan** — An interactive Power BI report for scouting and evaluating cricket players across specialized batting and bowling roles, enabling data-driven squad selection.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Report Pages](#report-pages)
- [Data Model](#data-model)
- [Key Measures (DAX)](#key-measures-dax)
- [Visuals Used](#visuals-used)
- [Filters & Interactivity](#filters--interactivity)
- [File Info](#file-info)
- [How to Use](#how-to-use)

---

## Project Overview

**Project Sportan** is a multi-page Power BI dashboard designed to analyse cricket player performance data for squad selection purposes. The report categorises players by their playing role — openers, middle-order batters, finishers, all-rounders, and specialist bowlers — and provides in-depth batting and bowling statistics at both the aggregate and per-match level.

The dashboard is intended for cricket analysts, team management, and selectors who need a clear, visual way to compare players across performance metrics and tournament stages.

---

## Report Pages

| # | Page Name | Purpose |
|---|-----------|---------|
| 1 | **Project - Sportan** | Overview/home page — aggregate batting stats, scatter plots, and trend charts for all players |
| 2 | **New Anchors / Middle Order** | Analysis of anchor batters and middle-order players — batting average, strike rate, boundary % |
| 3 | **New Finisher / Lower Order Anchor** | Evaluation of finishing batters — includes bowling strike rate trend for dual-role players |
| 4 | **New All Rounders / Lower Middle Order** | All-rounder assessment — combined batting and bowling metrics (economy, bowling strike rate) |
| 5 | **New Specialist Fast Bowlers / Tail End** | Specialist bowler analysis — bowling average, economy, dot ball %, bowling strike rate |
| 6 | **New Final 12** | Final squad shortlist view — player cards with image, role, team, and all key stats |
| 7 | **Batters — Player Details by Match** | Batter drill-down — per-match pivot tables for batting average and related metrics |
| 8 | **All Rounder / Low** | All-rounder per-match drill-down — batting and bowling pivot breakdowns |
| 9 | **Bowler — Player Details by Match** | Bowler drill-down — per-match bowling performance across pivot tables |

---

## Data Model

The report uses a **star schema** with the following tables:

### Dimension Tables

| Table | Key Columns | Description |
|-------|-------------|-------------|
| `dim_players` | `name`, `team`, `battingStyle`, `bowlingStyle`, `playingRole`, `image`, `Custom Batting Order` | Player master data including role, team, handedness, and profile image |
| `dim_match_summary` | `matchDate`, `Stage` | Match-level context including date hierarchy (Year/Quarter/Month/Day) and tournament stage |

### Fact Tables

| Table | Key Columns | Description |
|-------|-------------|-------------|
| `fact_batting_summary` | `match` (linked to `dim_match_summary`) | Ball-by-ball or innings-level batting records |
| `fact_bowling_summary` | `maiden` | Bowling spell records including maiden overs |

### Relationships

The model follows a standard star schema with `dim_players` and `dim_match_summary` acting as lookup tables connected to the fact tables. No auto-created relationships were configured (per the metadata).

---

## Key Measures (DAX)

All calculated measures are housed in the `key_measures` table. The following metrics power the report:

### Batting Metrics

| Measure | Description |
|---------|-------------|
| `Total Runs` | Total runs scored by the player |
| `Total Innings Batted` | Number of innings played |
| `Batting Average` | Runs per dismissal |
| `Strike Rate` | Runs scored per 100 balls faced |
| `Avg balls faced` | Average number of balls faced per innings |
| `Boundary%` | Percentage of runs scored via boundaries (4s & 6s) |
| `Batting Position` | Average position in the batting order |

### Bowling Metrics

| Measure | Description |
|---------|-------------|
| `Wickets` | Total wickets taken |
| `Total Innings Bowled` | Number of innings in which the player bowled |
| `Bowling Average` | Runs conceded per wicket taken |
| `Bowling Strike Rate` | Balls bowled per wicket taken |
| `Economy` | Runs conceded per over bowled |
| `Dot ball %` | Percentage of deliveries bowled that were dot balls |

---

## Visuals Used

| Visual Type | Usage |
|-------------|-------|
| **Table** (`tableEx`) | Player comparison tables — name, team, batting/bowling style, and multiple metrics |
| **Scatter Chart** | Batting Average vs Strike Rate (bubble size = Total Runs) — used for player clustering |
| **Area Chart** | Time-series trends for key metrics over match dates |
| **Pivot Table** | Per-match drill-downs on individual player performance |
| **Card** | KPI tiles showing aggregate values for selected player/filter context |
| **Slicer** | Filter by `Stage` (tournament stage) on all main pages; filter by player `name` on the Final 12 page |
| **Custom Image Visual** | Player profile photo display on drill-down pages |
| **Action Buttons** | Page navigation buttons for moving between report sections |
| **Shapes & Images** | Decorative elements and branding (logos) |

---

## Filters & Interactivity

- **Stage Slicer** — Available on pages 1–5; filters all visuals on the page to a specific tournament stage (e.g., Group Stage, Semi-Final, Final).
- **Player Name Slicer** — Available on the Final 12 page; select a specific player to view their complete stat card.
- **Cross-filtering** — Clicking a player in the scatter chart or table filters all other visuals on the same page to that player's data.
- **Drill-down Pages** — Pages 7–9 serve as detail views; use the navigation buttons on the role-based pages to jump to the per-match breakdown for a selected player.

---

## File Info

| Property | Value |
|----------|-------|
| File Name | `final_11.pbix` |
| Power BI Version | 1.28 (2026.01) |
| Created From | Power BI Cloud |
| File Size | ~271 KB |
| Dataset ID | `7b509ca0-46ea-426a-a869-b569958065b1` |
| Report ID | `cbf6afb1-4665-482c-8213-096911eb3925` |
| Theme | CY23SU04 (built-in Power BI theme) |
| Custom Visual | Simple Image Visual (`simpleImage`) — used for player profile photos |

---

## How to Use

1. **Open the file** in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (version 2026.01 or later recommended).
2. **Connect your data source** — the report references a cloud-hosted dataset. Ensure you have access to the linked dataset or replace it with your own data following the same schema.
3. **Navigate pages** using the action buttons on each page (top navigation bar within the report), or via the Pages panel in Power BI Desktop.
4. **Use the Stage slicer** to narrow analysis to a specific part of the tournament.
5. **Click any player row** in a table or a bubble in the scatter chart to cross-filter all visuals on the page to that player.
6. **View per-match details** by navigating to pages 7–9 for batting, all-rounder, or bowling breakdowns.
7. **Final 12 page** — use the player name slicer to review the selected squad's individual stat cards.

---

## Notes

- Player images are stored as static resources within the `.pbix` file and are rendered using the custom **Simple Image** visual.
- The `dim_players.image` field must contain valid image URLs or base64 data for profile photos to render correctly.
- The `Batting Position` measure uses an aggregated ordering based on `Custom Batting Order` from `dim_players`.

---

*Built with Microsoft Power BI | Cricket Analytics | Project Sportan*
