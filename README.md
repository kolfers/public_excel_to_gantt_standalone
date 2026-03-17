# Gantt Chart Tool

A self-contained HTML/JS tool that reads your Excel planning file and generates an interactive, Gantt chart directly in your browser. No server, no Python, and no installations are required. Your data never leaves your computer because all parsing and rendering happens locally in your browser.

**Live App:** [https://kolfers.github.io/public_excel_to_gantt_standalone/](https://kolfers.github.io/public_excel_to_gantt_standalone/) 

## Quick Start

1. Open `gantt_standalone.html` in any modern web browser (Edge, Chrome, Firefox, Safari).
2. Drag and drop your `.xlsx` or `.xlsm` file onto the drop zone, or click **"Browse..."** to select it.
3. The interactive Gantt chart will appear immediately!

_Don't have a dataset? Click **"Load example"** on the landing page to instantly try out the tool with built-in mock data, or click **"Start Empty Chart"** to begin from scratch._

## Setting Up Your Excel File

Your workbook uses two sheets. If columns are left blank, intelligent defaults are provided.

### "Current Planning" Sheet (or "Sheet1")

Contains your main tasks. Each row defines a single task:
| Column | Description |
|---|---|
| `ID` | A unique code for the task (e.g. `T001`). _Default: falls back to Title_ |
| `Phase` | The high-level phase (e.g. `Design`). _Default: `Phase 1`_ |
| `Category` | A group within the phase (e.g. `UX`). _Default: `Category 1`_ |
| `Title` | **[Required]** The task name. Add `(milestone)` anywhere to turn it into a gold milestone marker. |
| `Status` | `Done`, `On Track`, `Behind`, or `Waiting`. |
| `Start Date` | **[Required]** Format: `12-Mar-2026` |
| `End Date` | **[Required]** Format: `30-Apr-2026` |
| `Progress` | A number 0–100 (percent complete). |
| `Priority` | `High`, `Medium`, or `Low`. |
| `Dependency` | The `ID` of another task that must complete before this one starts. |
| `Description` | Any extra notes, visible in the hover tooltip. |

### "Log" Sheet (or "Sheet2")

A historical archive of your plan. Every time you click the **💾 Save Excel** button in the app, a snapshot of your current tasks is appended to this log so you can compare changes over time. Your browser will prompt you to download the updated `.xlsx` file.

## Features & Using the App

### Visualizations & Interactivity

- **Smart Formatting:** Tasks are grouped by Phase and Category. Milestones and completion stats are automatically aggregated in the left panel.
- **Fluid Panning:** Click and drag the chart to scroll horizontally. Inertia makes scrolling smooth. Load extra timeline bounds infinitely by clicking edge pills.
- **Multiple Time Horizons:** Switch quickly between Week, Month, and Year scale toggles. The Week view locks to Mondays for structured short-term planning.

### Task Management Features

- **Interact Directly:** Click on any data bar directly in the graph to open the Edit Task property modal. Edit details precisely without opening Excel.
- **Add Native Tasks:** Use the `+` buttons natively inside the left menu, or use the global `Add +` button.
- **Chaining & Duplication:** In the Edit Task modal, you can use the `"Dependent Task"` or `"Duplicate Task"` actions to rapidly create sequential work structures.
- **Data Filtering:** Click "Active" or "Overdue" on the left panel to cut through the noise, hiding finished projects and automatically collapsing empty categories. Toggle "Compact" mode to compress the left menu and use space efficiently.

### History, Feedback & Archiving

- **Comparison Engine:** Once snapshots are tracked in the Log sheet, use the **Compare** dropdown. The tool overlays older snapshots as ghost tracks (light grey items), and the timeline glows red. Changed items are visually demarcated.
- **Stats Dashboard:** A slide-out panel automatically tallies milestones achieved, items finished, and overruns that occurred since your chosen baseline snapshot.
- **Exporting for Co-Workers:** Need to share your visual timeline with a manager who doesn't use tracking sheets? Click the **📥 Export Chart** button. The app packages the entire UI and your current loaded data into a single, pre-filled, read-only `.html` file that opens identically on any computer.
- **Local Privacy:** Since the tool relies completely on browser-native Javascript processing, your corporate data and unannounced roadmaps never touch a third-party server.

## Dev Notes

- The html file is built using a python pipeline. So by itself the html file is probably not very readable, sorry.

---

_Released under the MIT License._
