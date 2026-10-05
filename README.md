# Gantt Chart Builder

**Live App:** [https://kolfers.github.io/public_excel_to_gantt_standalone/](https://kolfers.github.io/public_excel_to_gantt_standalone/)
**GitHub Repository:** [https://github.com/kolfers/public_excel_to_gantt_standalone](https://github.com/kolfers/public_excel_to_gantt_standalone)

Turn your Excel plan into an interactive Gantt chart. One self-contained HTML file: no server, no installation, no network requests. Everything runs in your browser and your file is never uploaded.

Desktop browsers only (Chrome or Edge recommended; see [Saving](#saving)).

## Changelog

### v3.0.0 — 5 Oct 2026
- **A complete rewrite.** Version 3 opens your existing workbooks and adds six views: Timeline, Dependencies, Roadmap, Table, Board (kanban by status) and Matrix (urgency by importance). See "Coming from version 2?" below for what changed.
- Saving writes into your original workbook and keeps its formatting and Excel Tables. Plan settings are shared through a hidden `Gantt Settings` sheet, and the `Log` sheet is now a compact history.
- If a save fails the app retries, offers Save as... and keeps a recovery copy in your browser. If the file changed on disk, changes are merged and you are only asked about real conflicts.
- Compare against a snapshot with ghost bars and a Changes panel, now with a snapshot picker in the navigation row.
- Select several tasks and change them together with the bulk bar; every bulk action is one undo step.
- Better filtering, a docked Settings panel and Info guide, a more compact left panel, and Matrix cards with due tags.
- Timeline and Roadmap header labels now thin out at regular calendar intervals so they never overlap, however far you zoom out or narrow the window.

## Quick start

1. Open `index.html` (or the live app) in a modern desktop browser.
2. Click **Open Excel file**, or drop an `.xlsx` / `.xlsm` file onto the drop box. Your two most recent files are listed under **Recent** (Chrome / Edge).
3. The chart renders immediately.

No plan yet? Click **Try example chart**, **Start an empty chart**, or **Download template**. **Download the app for offline use** saves this page as a single file you can keep.

## Your Excel file

The workbook can have three sheets:

| Sheet (accepted names) | Purpose |
|---|---|
| `Current Planning` (or `Sheet1`, `Sheet 1`, otherwise the first sheet) | One row per task |
| `Log` (or `Sheet2`, `Sheet 2`) | Snapshot history, written by the app |
| `Gantt Settings` (hidden) | Plan settings shared by everyone who opens the file, written by the app (see [Saving](#saving)). Do not edit it by hand. |

Only **Title**, **Start Date** and **End Date** are required. Header names are matched case-insensitively. Columns you add yourself are kept and written back untouched.

| Column | Description |
|---|---|
| `ID` | Filled in automatically (`T-001`, `T-002`, ...). Leave blank for new rows and do not change existing IDs. Duplicate IDs are renamed on load. |
| `Phase` | Top-level group. Default `Phase 1`. |
| `Category` | Group within a phase. Default `Category 1`. |
| `Title` | **Required.** Add `(milestone)` to mark a milestone. |
| `Status` | `Done`, `On Track`, `Behind`, `Waiting`, `On Hold`. |
| `Start Date`, `End Date` | **Required.** `DD-Mon-YYYY` (for example `12-Mar-2026`), `YYYY-MM-DD` or a real Excel date. Avoid text like `12/03/2026`, which is ambiguous. |
| `Progress` | 0-100. |
| `Priority` | `High`, `Medium` or `Low`. |
| `Dependency` | IDs of the tasks this one depends on, separated by commas. A task title also works and is converted to the ID. |
| `Owner` | Person responsible. Can be filtered and used for grouping. |
| `Tags` | Comma-separated labels. |
| `Description` | Free text. |
| `Comments` | Managed by the app, as `[DD-Mon-YYYY HH:MM:Name] text` entries. |

Rows without a title or with missing or unreadable dates are skipped (and kept in the file); an **Import report** tells you what was skipped or fixed.

## Using the chart

- **Views:** six tabs, switched with `l` / `Shift+L`.
  - *Timeline*: tasks as bars on a calendar.
  - *Dependencies*: tasks laid out left to right by what they depend on.
  - *Roadmap*: one row per phase or category, for the big picture.
  - *Table*: one row per task with sortable, reorderable columns.
  - *Board*: a kanban board by status; drag a card to change its status.
  - *Matrix*: urgency by importance, in four quadrants; drag a card to change its priority or due date.
- **Zoom:** Week / Month / Quarter / Year, `+` / `-` or Ctrl + scroll for finer steps, **Fit project**, **Today** (`t`). `v` cycles the levels.
- **Edit:** double-click a bar or row (or press `e`) to open the task modal. Drag a bar to move it, drag its edges to resize (snaps to days). `d` adds a task that depends on the hovered one, `n` duplicates, `s` adds a parent task.
- **Select several tasks:** Ctrl/Cmd+click, Shift+click for a range, Alt+click for a task and everything downstream. A bulk bar offers Status, Priority, Move to, Shift dates, Tags and Delete.
- **Undo / redo:** Ctrl+Z, Ctrl+Shift+Z or Ctrl+Y. Every bulk action is one step.
- **Filters and search:** All / Active / Overdue, a filter panel (`f`) with Status, Priority, Owner, Tags and more, group by owner, and task search (`/`).
- **Check dependencies:** finds overlaps, cycles and missing references, and offers fixes with a preview.
- **Compare** (Timeline, Dependencies and Table): tick **Show changes since** and pick a snapshot to see ghost bars and a Changes panel (added, delayed, completed, ...). Snapshots can be named and one can be marked as the baseline.
- **Export:** the **...** menu offers a 16:9 **slide** (PNG, SVG or clipboard, rolled up to phases, categories or tasks) and a read-only **interactive HTML** copy you can share.
- **Settings** (the gear): legend, compact rows, auto-save, hover panel, layout choices for the Table, Board, Matrix and Roadmap, and reset buttons. **Info** (`i`) is a built-in guide to the app. Both panels stay docked to the side so the chart remains usable.
- **Appearance:** several colour palettes (Catppuccin, Dracula, Monokai and more), light and dark mode (`m`, `p`), and a compact left panel for narrow windows. Press `?` for the full list of shortcuts.

## Saving

- **Save Excel** (Ctrl+S) writes your changes into the original workbook, keeping its formatting and Excel Tables, and appends a snapshot to the `Log` sheet. In Chrome and Edge a file opened with **Open Excel file** or **Recent** is saved in place; a dropped file or another browser downloads a copy instead.
- **Plan settings** (hover panel, Table columns, Board, Matrix and Roadmap layout, ...) are stored in the workbook's hidden `Gantt Settings` sheet, so everyone who opens the file sees the same layout. Personal settings (theme, palette, zoom, filters, compact rows, ...) stay in your browser.
- **Auto-save** (optional, Chrome / Edge) saves the planning sheet about a second and a half after each edit.
- If a save fails the app retries three times, then shows **Not saved** with Retry, Save as... and Download copy. A recovery copy is kept in your browser, and the app offers to restore it the next time you open that file.
- If the file changed on disk (for example you edited it in Excel), the app merges the changes and asks only about fields that conflict.
- Opening the same file in a second tab shows a warning and pauses auto-save there.
- `.xlsm` files are saved in place with their macros kept. Only if the workbook cannot be patched safely does the app offer a new `.xlsx` copy (without macros).

## Coming from version 2?

Version 3 is a rewrite and opens your v2 workbooks, with these differences:

- The `Log` sheet is now a compact delta log. Old logs are converted on the first save and are no longer readable as plain rows in Excel.
- Rows without an `ID` get one (`T-001`, ...), duplicate IDs are renumbered, and task titles in the `Dependency` column are converted to IDs. The app shows a notice when it does this.
- Weekend shading and the easter eggs are gone, and the app is desktop only.

## Privacy

Your data stays on your machine. The app makes no network requests; fonts and the Excel library are inlined in the page. Recent files, view settings and recovery copies are stored only in your browser.

---
*Released under the MIT License.*
