# Excel Performance Dashboard — Plumbing, HVAC & Electrical

A fully interactive Excel dashboard built to track **month-to-month performance year-over-year** for a trade-services company. Built entirely with native Excel features — no add-ins, no coding environment, works on Excel for Windows and Mac.

> Note: The workbook uses sample data for demonstration purposes. The focus of this portfolio piece is the **functionality, interactivity, and data-handling logic** of the dashboard.

***

## Project Summary

**Goal:** Give an internal, non-technical team a self-maintaining performance dashboard — they add monthly raw data, and every chart and KPI updates automatically.

**What the client sees in the workbook (4 sheets):**

| Sheet | Purpose |
| --- | --- |
| **RawData** | The only sheet the team touches — add new monthly data here |
| **Calc** | All calculations, pivot tables, and control cells (hidden from normal use) |
| **Dashboard** | The visual report: KPI cards, slicer, charts, and buttons |
| **Pivot** | Underlying pivot table feeding the dashboard |

***

## Dashboard Layout (6 modules)

1. **Marketing Cost** — monthly bars + YoY % line (dual-axis combo chart)
2. **Call Volume** — monthly bars + YoY % line (dual-axis combo chart)
3. **Revenue Share** — pie chart of department revenue mix (Plumbing / HVAC / Electrical)
4. **Plumbing Revenue** — monthly bars + YoY % line
5. **HVAC Revenue** — monthly bars + YoY % line
6. **Electrical Revenue** — monthly bars + YoY % line

Every chart shows **two things at once**: the actual monthly value (bars) and the year-over-year growth rate (line).

***

## Key Features & How They Work

### 1. Self-Maintaining Data (Super Table)

- The **RawData** sheet is an Excel **structured table**.
- When the team types a new month's data in the row below, the table **auto-expands** its range.
- All formulas and charts pick up the new row automatically.

**Columns:**

```
Year | Month | Total_Marketing_Cost | Total_Call_Volume | Revenue_Plumbing | Revenue_HVAC | Revenue_Electrical
```

### 2. Dirty-Data Prevention (Data Validation)

Each input column has **data validation** to keep the data clean:

- **Year** → whole number only (e.g., 2000–2099)
- **Month** → integer between 1 and 12
- **Marketing cost & revenue columns** → non-negative numbers, formatted as currency

Each validated cell also shows an **input prompt** (what to enter) and an **error alert** (blocks invalid entry), so the team can't accidentally type a bad month or negative revenue.

### 3. Year Slicer (Interactive Filtering)

- A **slicer** on the left lets the user pick a year (e.g., 2026).
- Selecting a year instantly filters **all pivot tables** feeding the dashboard.
- Every chart and KPI switches to show that year vs. the prior year.

### 4. One-Click / Automatic Data Refresh

- A **Refresh Data** button (form control + macro) refreshes all pivot tables after new data is added.
- Fallback for clients who disable macros: the pivot table is set to **refresh when the file opens**, so closing and reopening the file also updates everything.
- **No-add-in alternative:** the standard `Data > Refresh All` menu works without any macro.

### 5. KPI Cards (Text Boxes Linked to Cells)

- Top of the dashboard shows KPI cards: **Total Revenue, Total Marketing Cost, Total Call Volume, YoY Growth %**.
- Each card is a **text box linked to a cell** — when the slicer changes or data refreshes, the card numbers update automatically.

### 6. Smart Formatting (Auto Positive/Negative Color)

- Custom number format: `+0.0%;-0.0%;0` → positive shows `+8.8%`, negative shows `-8.0%`.
- **Conditional formatting** turns the YoY % **green** when positive and **red** when negative — growth vs. decline is visible at a glance.

### 7. Department Switch Buttons (Option Buttons)

- Three **option buttons** (Plumbing / HVAC / Electrical) sit beside the department chart.
- Clicking a button writes `1 / 2 / 3` into a control cell.
- An `IF` formula reads that cell and loads the matching department's 12-month revenue data into the chart — so one chart swaps between three departments without rebuilding anything.

***

## Formulas Used

| Function | Role in this dashboard |
| --- | --- |
| `SUMIFS` | Sum a metric by year and/or month (e.g., total revenue for a selected year). |
| `SUMPRODUCT` | Multi-condition matching for YoY comparisons (same month, prior year). |
| `IF` | Department switching — read the button value (1/2/3) and return the right department's data. |


***

## Native Excel Techniques Used

- Structured tables (auto-expanding data ranges, structured references)
- Data validation with input prompts & error alerts
- Named ranges / defined names (readable formulas instead of raw cell addresses)
- Pivot tables + slicer (interactive year filtering)
- Combo charts (bar + line on dual axes)
- Pie chart with data labels
- Custom number formats
- Conditional formatting (automatic red/green)
- Form controls (option buttons)
- Text boxes linked to cells (live KPI cards)
- Worksheet protection (control which cells the team can edit)

***

## How the User Works With It

1. Add new monthly data in the **RawData** sheet (validated cells only).
2. Click **Refresh Data** (or `Data > Refresh All`, or close & reopen the file).
3. Use the **year slicer** to compare years.
4. Use the **option buttons** to switch department views.
5. Read the KPI cards and charts — all live and auto-updating.

***
