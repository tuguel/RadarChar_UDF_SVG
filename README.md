# Dynamic Radar Charts for Power BI

**Fully dynamic Radar Charts in Power BI using only DAX + SVG + UDF — no external visuals, no security risks, 100% native.**

A flexible solution that automatically generates Radar Charts with any number of nodes (3 to 8),
concentric rings, axis guides, and smart auto-rotated labels — driven entirely by your data.

![Data Pills Logo](DataPills-Logo.svg)

---

## Preview

![Dynamic Radar Charts](RadarChart.png)
*Flexible from 3 to 8 nodes — fully driven by your data*

---

## Features

- Dynamic nodes from **3 to 8** based on your data
- Concentric rings, axis guides, and auto-rotated labels
- Intelligent label rotation (perpendicular "T" style on 5 and 7 nodes)
- Fully customizable fill and edge colors
- Works in **Table**, **multi-row Card**, and **Image** visuals
- No external visuals required — 100% native Power BI

---

## Prerequisites

- **Power BI Desktop** version **2.120 or later**
- **DAX User-Defined Functions** enabled *(Preview Feature — must be turned on manually)*:
  `File → Options and settings → Options → Preview features → DAX User-Defined Functions`

> ⚠️ Without enabling DAX UDFs, the TMDL will fail to apply. This is a one-time setup per Desktop installation.

---

## Data Structure

The solution expects a table named **`ProfileScores`** with the following columns:

| Column     | Type    | Required | Description                                        |
|------------|---------|----------|----------------------------------------------------|
| `Property` | Text    | ✅        | Name shown as the chart title (e.g., "ArQ Hotel")  |
| `Category` | Text    | ✅        | Axis label (e.g., "Cleanliness", "Location")       |
| `Review`   | Decimal | ✅        | Normalized value between **0.0 and 1.0**           |
| `Sorting`  | Integer | Optional | Controls axis sequence; falls back to alphabetical |

> 💡 Each unique `Property` value generates its own Radar Chart when used in a Table or multi-row Card visual.

---

## Repository Files

| File                 | Description                                          |
|----------------------|------------------------------------------------------|
| `Radar.pbix`         | Ready-to-use Power BI file **(recommended)**         |
| `Table&Measure.TMDL` | TMDL script with sample table + all measures         |
| `Radar_UDFs.TMDL`    | All User-Defined Functions (TMDL format)             |
| `SampleTable.txt`    | Optional: DAX code to recreate the sample table      |
| `Measures.txt`       | Optional: DAX code for measures only                 |

---

## Quick Start (Recommended)

1. Download the **`Radar.pbix`** file
2. Open it in **Power BI Desktop**
3. Make sure **DAX UDFs** are enabled (see [Prerequisites](#prerequisites))
4. Replace the data in the **`ProfileScores`** table with your own
   — match the columns `Property`, `Category`, `Review`, and optionally `Sorting`
   (see [Data Structure](#data-structure))
5. Customize colors via the `AreaHexColour` and `EdgeHexColour` measures if desired
   (see [Default Colors](#default-colors))
6. Done — your dynamic Radar Charts are ready ✅

---

## Adding to an Existing PBIX

1. Open your existing PBIX file in Power BI Desktop
2. Switch to **TMDL View** (TMDL icon on the left sidebar)
3. Paste the content of **`Radar_UDFs.TMDL`** → click **Apply changes**
4. Paste the content of **`Table&Measure.TMDL`** → click **Apply changes**
5. Go to **Report View** and build your visualization:
   - Add a **Button Slicer** → use the `[Property]` field
   - Add an **Image** visual (or Card) → place `SVGRadar` in the Image Field
   - Set **Image Fit** to **Stretch**
6. If your table or column names differ from `ProfileScores`, update these references
   inside the **`SVGRadar`** measure:
   ```dax
   ALLSELECTED(ProfileScores)  -- replace with your table name
   ProfileScores[Category]     -- replace with your axis/category field
   ```
   Also update **`NodeScore`** and **`NodeOrder`** if your column names differ from
   `ProfileScores[Review]` and `ProfileScores[Sorting]` respectively.

> 💡 `SVGradarFromTable` expects a table with exactly these internal column names:
> `Attribute` (Text), `Score` (Decimal, 0.0–1.0), `Order` (Integer, optional).
> The `SVGRadar` measure handles this mapping automatically from `ProfileScores`.
> If you call the UDF directly with your own table, make sure your schema matches these names.

---

## Default Colors

Colors are controlled by two dedicated measures in the `🧮Measures` table.
To change them, update the return value of each measure directly:

| Measure         | Default   | Controls                        |
|-----------------|-----------|---------------------------------|
| `AreaHexColour` | `#00D4C6` | Fill color of the radar polygon |
| `EdgeHexColour` | `#101080` | Border/edge color               |

```dax
MEASURE '🧮Measures'[AreaHexColour] = "#00D4C6"
MEASURE '🧮Measures'[EdgeHexColour] = "#101080"
```

Any valid hex color is supported. Changes apply instantly across all charts in the visual.

---

## Limitations & Known Behavior

| Scenario                            | Behavior                                                                    |
|-------------------------------------|-----------------------------------------------------------------------------|
| More than 8 attributes per property | Only the first 8 are rendered (sorted by `Sorting`, then alphabetically)    |
| Fewer than 3 attributes             | Chart will not render — minimum is 3 nodes                                  |
| Missing `Review` values             | Rows with blank scores are excluded automatically                           |
| Even vs odd node count              | Even N: guide lines connect opposite vertices. Odd N: lines radiate from center. Both are by design |
| Power BI Service                    | Fully supported — UDFs are evaluated server-side with no additional setup   |

---

## License

This project is released under the [MIT License](LICENSE).
Free to use, adapt, and share — attribution appreciated.

---

## Author

**Miguel Madriz** · [LinkedIn](https://linkedin.com/in/miguelmadriz/) · [GitHub](https://github.com/tuguel/)

*Part of the **Data Pills** series — bite-sized Power BI solutions that make your data dance.*

---

⭐ If this saved you time, consider starring the repo — it helps others find it.
