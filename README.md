# Gantt Chart Tool

**Live App:** [https://kolfers.github.io/public_excel_to_gantt_standalone/](https://kolfers.github.io/public_excel_to_gantt_standalone/)
**GitHub Repository:** [https://github.com/kolfers/public_excel_to_gantt_standalone](https://github.com/kolfers/public_excel_to_gantt_standalone)

A standalone HTML/JS tool that reads an Excel planning file and renders an interactive Gantt chart in the browser. No server or installation is required. All parsing and rendering runs locally in the browser, so your data stays on your machine.

## Quick Start

1. Open `gantt_standalone.html` in any modern web browser (Edge, Chrome, Firefox, Safari).
2. Drag and drop your `.xlsx` or `.xlsm` file onto the drop zone, or click **"Browse..."** to select it.
3. The Gantt chart will render immediately.

*No data yet? Click **"Load example"** on the landing page to load built-in mock data, or click **"Start Empty Chart"** to start from scratch.*

## Setting Up Your Excel File

Your workbook uses two sheets. Columns left blank will use sensible defaults.

### "Current Planning" Sheet (or "Sheet1")
Each row defines a single task:

| Column | Description |
|---|---|
| `ID` | A unique code for the task (e.g. `T001`). *Default: falls back to Title* |
| `Phase` | The high-level phase (e.g. `Design`). *Default: `Phase 1`* |
| `Category` | A group within the phase (e.g. `UX`). *Default: `Category 1`* |
| `Title` | **[Required]** The task name. Add `(milestone)` anywhere to mark it as a milestone. |
| `Status` | `Done`, `On Track`, `Behind`, `Waiting`, or `On Hold`. |
| `Start Date` | **[Required]** Format: `12-Mar-2026` |
| `End Date` | **[Required]** Format: `30-Apr-2026` |
| `Progress` | A number 0–100 (percent complete). |
| `Priority` | `High`, `Medium`, or `Low`. |
| `Dependency` | The `ID` of another task that must complete before this one starts. |
| `Description` | Any extra notes, visible in the hover tooltip. |

### "Log" Sheet (or "Sheet2")
A historical archive of your plan. Each time you click **💾 Save Excel** in the app, a snapshot of the current tasks is appended to this sheet. The browser will prompt you to download the updated `.xlsx` file.

## Features

### Chart & Navigation
- Tasks are grouped by Phase and Category. Milestone and completion stats are aggregated in the left panel.
- Click and drag the chart to scroll horizontally.
- Switch between Week, Month, and Year scale views. Week view aligns to Mondays.

### Task Management
- Click any task bar to open the Edit Task modal. Hovering a bar shows ✎ Edit and 💬 Comments buttons. The same options are available by hovering task rows in the left panel.
- Add tasks via the **Add Task** button in the top bar, the inline `+` button on Phase/Category rows, or by pressing `n` while hovering a Phase or Category row.
- In the Edit Task modal, **Dependent Task** creates a follow-on task pre-linked by dependency; **Duplicate Task** copies the task along with its comments.
- Comments support author names, timestamps, and inline edit/delete.
- **Keyboard shortcuts** (while hovering a bar or left-panel row): `e` Edit · `c` Comments · `d` Dependent · `n` Duplicate. On Phase/Category hover: `n` adds a task, `e` or `r` renames. `s` saves the Excel from anywhere.

### Filtering
- **Active** hides On Hold tasks. **Overdue** shows only overdue items. Both collapse empty categories automatically.
- The **Filter** button opens a panel for fine-grained filtering by Status, Priority, Comments, Dependency, and Overdue state. Filters within a property are OR'd; filters across properties are AND'd. Active filters are shown as a summary bar beneath the timeline.
- **Compact** mode compresses the left panel to save horizontal space.

### Snapshots & Export
- Once the Log sheet contains snapshots, the **Compare** dropdown overlays an older snapshot as ghost tracks on the chart. Changed items are highlighted and the timeline header turns red. A stats panel summarises milestones, completions, holds, and overruns relative to the chosen baseline.
- **Export Chart** packages the entire UI and current data into a single self-contained `.html` file that can be opened on any computer without the original Excel file.

---
*Released under the MIT License.*
