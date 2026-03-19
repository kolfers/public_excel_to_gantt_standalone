# Gantt Chart Tool

**Live App:** [https://kolfers.github.io/public_excel_to_gantt_standalone/](https://kolfers.github.io/public_excel_to_gantt_standalone/)  
**GitHub Repository:** [https://github.com/kolfers/public_excel_to_gantt_standalone](https://github.com/kolfers/public_excel_to_gantt_standalone)

A self-contained HTML/JS tool that reads your Excel planning file and generates an interactive, beautiful Gantt chart directly in your browser. No server, no Python, and no installations are required. Your data never leaves your computer because all parsing and rendering happens locally in your browser.

## Quick Start

1. Open `index.html` in any modern web browser (Edge, Chrome, Firefox, Safari).
2. Drag and drop your `.xlsx` or `.xlsm` file onto the drop zone, or click **"Browse..."** to select it.
3. The interactive Gantt chart will appear immediately!

*Don't have a dataset? Click **"Load example"** on the landing page to instantly try out the tool with built-in mock data, or click **"Start Empty Chart"** to begin from scratch.*

## Setting Up Your Excel File

Your workbook uses two sheets. If columns are left blank, intelligent defaults are provided.

### "Current Planning" Sheet (or "Sheet1")
Contains your main tasks. Each row defines a single task:

| Column | Description |
|---|---|
| `ID` | A unique code for the task (e.g. `T001`). *Default: falls back to Title* |
| `Phase` | The high-level phase (e.g. `Design`). *Default: `Phase 1`* |
| `Category` | A group within the phase (e.g. `UX`). *Default: `Category 1`* |
| `Title` | **[Required]** The task name. Add `(milestone)` anywhere to turn it into a gold milestone marker. |
| `Status` | `Done`, `On Track`, `Behind`, or `Waiting`. |
| `Start Date` | **[Required]** Format: `12-Mar-2026` |
| `End Date` | **[Required]** Format: `30-Apr-2026` |
| `Progress` | A number 0–100 (percent complete). |
| `Priority` | `High`, `Medium`, or `Low`. |
| `Dependency` | The `ID` of another task that must complete before this one starts. |
| `Description` | Any extra notes, visible in the hover tooltip and Edit modal. |
| `Comments` | Internal comment log (managed by the app — do not edit manually). |

### "Log" Sheet (or "Sheet2")
A historical archive of your plan. Every time you click the **💾 Save Excel** button, a snapshot of your current tasks is appended to this log so you can compare changes over time.

## Features & Using the App

### Visualizations & Interactivity
- **Smart Formatting:** Tasks are grouped by Phase and Category. Milestones and completion stats are automatically aggregated in the left panel.
- **Fluid Panning:** Click and drag the chart to scroll horizontally with smooth inertia momentum. Load extra timeline bounds infinitely by clicking the glowing edge pills.
- **Multiple Time Horizons:** Switch between Week, Month, and Year scale toggles. The Week view locks to Mondays for structured short-term planning.
- **Bar Hover Overlay:** Hovering a task bar reveals floating **💬** and **✎** action buttons. Keyboard shortcuts also work: press `c` to open Comments, `e` to open the Edit modal while hovering a bar.
- **Dark Mode:** Toggle between light and dark themes using the ☽/☀ button in the toolbar. Your preference is remembered across sessions.

### Powerful Task Management Engine
- **Interact Directly:** Click on any task bar to open the **Edit Task** modal. Edit all task properties without touching Excel.
- **Add Native Tasks:** Use the `+` buttons that appear when hovering a phase or category row, or use the global **Add +** button in the toolbar.
- **Chaining & Duplication:** In the Edit Task modal, use **"Dependent Task"** to create a new task that starts where this one ends, or **"Duplicate Task"** to clone it instantly.
- **Phase & Category Rename:** Hover a phase or category row and click the ✏ pencil icon (or press `e`) to rename it. If the new name collides with an existing group, you'll be offered a choice to **merge** all tasks into it or add an auto-incremented suffix instead.
- **Data Filtering:** Click **Active** or **Overdue** on the left panel to hide finished work and collapse empty categories. Toggle **Compact** mode to compress the left panel and maximise chart space.
- **Left Panel Sorting:** Tasks are sorted by Priority (High → Medium → Low), then most-overdue first, then earliest start date. Categories are sorted alphabetically.

### Comments System
- **Per-Task Comments:** Each task has a comments log. Open the **Comments modal** from the bar hover overlay (💬), the Edit modal's comment count link, or the modal view-switcher.
- **Add, Edit & Delete:** Type a comment with your name, then add it. Each comment shows its author (with a consistent color), date, and text. Edit or delete any comment with the icons that appear on hover.
- **Side-by-Side View:** Use the **⬜⬜ Both** button in any modal's view-switcher to open Edit and Comments panels side by side.

### History, Feedback & Archiving
- **Comparison Engine:** Once snapshots are tracked in the Log sheet, use the **Compare** dropdown. Older snapshots are overlaid as ghost rows, the timeline border glows red, and changed fields are highlighted.
- **Stats Dashboard:** A slide-out panel tallies milestones achieved, items finished, and overruns since your chosen baseline snapshot.
- **Unsaved Changes Indicator:** Any in-app edit triggers a visible warning on the toolbar (yellow background in light mode, amber glow in dark mode). It clears automatically on save.
- **Save Excel:** The **💾 Save Excel** button downloads an updated `.xlsx` file with the current snapshot appended to the Log sheet. The download is named `{source}_gantt_{d}-{month}-{yyyy}.xlsx`.
- **Export Chart:** The **📥 Export Chart** button packages the entire app state into a single self-contained read-only `.html` file — perfect for sharing with stakeholders who don't use tracking sheets.
- **Local Privacy:** All processing is browser-native. Your data never touches a third-party server.

---

## Dev Notes

The `index.html` file is built from modular source files using a Python build pipeline and is not intended to be edited directly.

---

*Released under the MIT License.*
