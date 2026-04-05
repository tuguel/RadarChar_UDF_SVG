# RadarChar_UDF_SVG
Radar Chart UDF + SVG + DAX
# Dynamic Radar Charts for Power BI

**Fully dynamic Radar Charts in Power BI using only DAX + SVG + UDF**

A flexible and ready-to-use solution that automatically generates Radar Charts with any number of nodes (3 to 8), concentric rings, axis guides, and smart auto-rotated labels.

![Data Pills Logo](DataPills.svg)

## Features

- Dynamic nodes from **3 to 8** based on your data
- Concentric rings, axis guides and auto-rotated labels
- Intelligent label rotation (perpendicular "T" style on 5 and 7 nodes)
- Fully customizable (just change colors)
- Works in Table visuals, multi-row Cards and Image visuals
- Cross-platform compatible (including Apple M1/M2)

## Repository Files

| File                    | Description |
|-------------------------|-----------|
| `Radar.PBIX`            | Ready-to-use Power BI file (recommended) |
| `Table&Measure.TMDL`    | TMDL script to create `ProfileScores` table and measures |
| `UDF4Radar.txt`         | All User-Defined Functions (5 functions) |
| `SampleTable.txt`       | Sample data for `ProfileScores` table |
| `Measures.txt`          | Color measures (`AreaHexColour`, `EdgeHexColour`), `NodeOrder`, `NodeScore` and final `SVGRadar` measure |

## Quick Start

1. Download the **`Radar.PBIX`** file
2. Open it in Power BI Desktop
3. Replace the data in the `ProfileScores` table with your own data
4. Customize colors in the `SVGRadar` measure if desired
5. Done! Your dynamic Radar Charts are ready

## Preview

![Dynamic Radar Charts](RadarChart.PNG)  
*(3, 4, 5, 6, 7 and 8 nodes)*

## How to add to your existing PBIX

- Use the **TMDL** file (`Table&Measure.TMDL`) to import the table and measures.
- Or manually copy the functions from `UDF4Radar.txt` and the measure from `Measures.txt`.

## Author
**Miguel Madriz** – Data Pills Series
