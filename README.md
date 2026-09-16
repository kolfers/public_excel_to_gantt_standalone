# Gantt Chart Tool

***Last updated: 16 Sep 2026: v2.32***

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
| `Dependency` | The `ID` of another task that must complete before this one starts. A task can depend on more than one other task — list multiple IDs separated by commas. |
| `Tags` | Comma-separated labels for filtering, e.g. `urgent, needs-review` (letters, numbers, dashes, and spaces allowed within a tag; commas separate tags). |
| `Description` | Any extra notes, visible in the hover tooltip. |

### "Log" Sheet (or "Sheet2")
A historical archive of your plan. Each time you click **💾 Save Excel** in the app, a snapshot of the current tasks is appended to this sheet. On supported browsers (Chrome/Edge), if you opened the file via **"Browse..."**, changes are saved directly back to the original file. Otherwise the updated `.xlsx` is downloaded.

## Features

### Chart & Navigation
- Tasks are grouped by Phase and Category. Milestone and completion stats are aggregated in the left panel.
- Click and drag the chart to scroll horizontally.
- Switch between Week, Month, and Year scale views. Week view aligns to Mondays.
- **Linked view** (toggle button in the toolbar, or press `l`) lays tasks out left-to-right by dependency chain instead of by date, so you can follow a chain of dependent tasks at a glance. Dependency arrows connect each task to what it's waiting on, and snapshot comparisons still show ghost bars for changed items. Add Task, Edit, and all the usual row shortcuts work the same as in Timeline view.
- **Task search**: the search field next to the `+` new-task button finds tasks by title as you type (3+ characters), with an autocomplete dropdown you can navigate by mouse or arrow keys. Selecting a result jumps straight to that task, automatically clearing filters or expanding a collapsed Phase/Category if needed to reveal it.

### Task Management
- Click any task bar to open the Edit Task modal. Hovering a bar shows ✎ Edit and 💬 Comments buttons. The same options are available by hovering task rows in the left panel.
- Add tasks via the **Add Task** button in the top bar, the inline `+` button on Phase/Category rows, or by pressing `n` while hovering a Phase or Category row.
- In the Edit Task modal, **New Dependent** creates a follow-on task pre-linked by dependency; **New Duplicate** copies the task along with its comments. Either one first saves any unsaved edits on the task you're currently viewing, so nothing is lost when you switch.
- A task can now depend on **multiple other tasks** — pick as many as needed from the dependency dropdown in the Edit Task modal, shown as removable chips colored by each dependency's status. The chart draws one arrow per dependency, and arrows converging on the same task merge into a single shared line instead of crossing.
- **Tags**: A full-width field below Progress in the Edit Task modal. Type comma-separated tags and/or pick from a dropdown of tags already used elsewhere — picking one from the dropdown adds it to the list instead of replacing what's typed.
- Comments support author names, timestamps, and inline edit/delete.
- Hovering a Phase or Category row in the left panel reveals a ✏ (rename/delete) icon; renaming a Category also offers a **Move** button to reassign it (and all its tasks) to a different Phase. You can also drag and drop rows directly in the left panel: drag a Phase onto another Phase to reorder, a Category onto a row in a different Phase to move it, or a task onto a Category/task row to reassign it.
- **Keyboard shortcuts** (while hovering a bar or left-panel row): `e` Edit · `c` Comments · `d` Dependent · `n` Duplicate · `s` creates a new predecessor task in the same Phase/Category, automatically linked as a dependency of the hovered task once saved (the reverse of `d`). On Phase/Category hover: `n` adds a task, `e` or `r` renames. Use the **Save Excel** button to save — `s` is no longer a save shortcut.

### Filtering
- **Active** hides On Hold tasks. **Overdue** shows only overdue items. Both collapse empty categories automatically.
- The **Filter** button opens a panel for fine-grained filtering by Status, Priority, Comments, Dependency, Overdue state, Milestone, and Tags (listed last, since the tag list can grow large). Filters within a property are OR'd (so selecting two tags shows items with either one); filters across properties are AND'd. The **Clear all** button sits right after the "Filters" title and turns red once a filter is active. When any filter is active, the Filter button itself shows a small "×" — click it to clear every filter in one go. Active filters are shown as a summary bar beneath the timeline, with tags getting their own rotating colors. Press `f` to open the panel with its corner right at your cursor instead of anchored to the button; it stays open briefly if the cursor strays outside it.
- **Compact** mode compresses the left panel to save horizontal space.

### Saving & Snapshots
- **Save Excel** writes the current tasks back to the *Current Planning* sheet and appends a timestamped snapshot to the *Log* sheet. On supported browsers (Chrome/Edge) when the file was opened via "Browse", it overwrites the original file directly; otherwise it downloads an updated `.xlsx`. Each saved snapshot becomes a selectable entry in the **Compare** dropdown.
- **Auto-Save** (Chrome/Edge only, `.xlsx` files opened via "Browse") silently rewrites only the *Current Planning* sheet after each confirmed edit, keeping your work safe if the browser closes unexpectedly. It does **not** create a Log entry or add a Compare snapshot — it is a safety net, not a versioned checkpoint.
- **On-open snapshot (automatic):** Every time you open a file, the app compares *Current Planning* against the most recent Log entry. If they differ — because Auto-Save ran since the last manual save, or the file was edited externally — a snapshot is silently appended to the Log, timestamped with the file's last-modified date. Your history stays complete with no extra steps.
- Use the **Compare** dropdown to overlay any past snapshot as ghost tracks on the chart. Changed items are highlighted and the timeline header glows red. The **Stats** flyout summarises milestones, completions, holds, and overruns relative to the chosen baseline.
- **Export Chart** packages the current view into a single self-contained `.html` file that can be opened on any computer without the original Excel file.

## Changelog

### v2.32 — 16 Sep 2026
- Fixed: applying a filter (Active/Overdue or a custom filter) to a fully collapsed board could hide every Phase entirely instead of showing the collapsed Phase headers that still had matching tasks inside.
- Fixed: applying a filter to a collapsed Phase no longer spills its Categories back open — collapsed groups now stay collapsed exactly as you left them, whether or not a filter is active.

### v2.31 — 16 Sep 2026
- New **task search**: a search field next to the `+` new-task button lets you find a task by title as you type (3+ characters). Matching tasks are listed in a dropdown with the matched letters highlighted; use the mouse or the arrow keys and Enter to jump straight to a task, even if it's currently hidden behind a filter or a collapsed Phase/Category.
- The `+` new-task button now sits just below the timeline header instead of overlapping the first phase row, and its "+" glyph is centered more consistently across all color themes.
- Fixed: when a Phase was collapsed while a filter or comparison was active, matching Categories under that Phase could disappear instead of staying visible.

### v2.30 — 16 Sep 2026
- Dragging a Phase in the left panel can now be dropped on any Category or Task row belonging to a different Phase (not just another Phase header) — it's inserted right after whichever Phase that row belongs to.
- New **Preferences** setting for Linked (dependency) view: choose whether task bars are all Narrow, all Medium (the new default), all Wide, or sized "By Duration" (the previous always-on behavior).

### v2.29 — 16 Sep 2026
- **Fixed the Start/End Date picker icon being invisible (black-on-black) in dark mode.**
- The Edit Task modal's **Category** dropdown now only lists Categories already used within the currently-selected Phase, instead of every Category across the whole plan.
- Renaming or deleting a Phase/Category, and choosing how to resolve a naming collision, now uses the app's own centered dialogs instead of the browser's plain popup boxes.
- New **Move** button in the Rename/Delete Category modal: moves a Category (and all its tasks) to a different Phase, with the same "merge into an existing Category or keep it separate" handling as a rename collision.
- **Left-panel drag and drop**: Phases, Categories, and individual tasks can now be reordered/re-parented by dragging their row in the left panel — drag a Phase onto another Phase to reorder them, a Category onto any row in a different Phase to move it there, or a task onto a Category/task row to move it. Dragging over a collapsed Phase or Category for about a second auto-expands it, and dragging near the top/bottom edge auto-scrolls.

### v2.28 — 9 Sep 2026
- **Fixed Export Chart producing a broken, unopenable file.** Exported charts now open correctly every time, with all tasks, bars, and toolbar behavior intact.
- **A task can now depend on more than one other task.** Pick as many dependencies as needed from the dropdown in the Edit Task modal — each is shown as a removable chip colored by that dependency's status. The chart draws one arrow per dependency, and arrows converging on the same task now merge into a single shared line instead of crossing.
- The Edit Task modal is reorganized into separate Properties, Description, and Comments panels, and the hover panel got a matching layout with a new Settings toggle to show/hide each section. **New Dependent** and **New Duplicate** now save any unsaved edits on the task you're viewing before switching, instead of silently discarding them.
- New keyboard shortcut: hovering a task and pressing `s` creates a new predecessor task in the same Phase/Category, pre-filled and automatically linked as a dependency of the hovered task once saved (the reverse of the `d` shortcut). Note that `s` no longer saves to Excel — use the **Save Excel** button instead.
- Reworked the top toolbar: the Timeline/Linked view toggle is now a slider switch instead of swapping button text, spacing between toolbar buttons is now even, and the toolbar no longer shifts position when the unsaved-changes indicator appears or the view is switched.
- Timeline header dates (day names/numbers, week numbers) are easier to read in several dark color palettes.

### v2.24 — 8 Sep 2026
- Active-filter pills: Comments, Dependency, Overdue, and Milestone no longer show a redundant "COMMENTS:"/"DEPENDENCY:"/etc. prefix (Status, Priority, and Tag still do, since their values need it for context).
- Active-filter pill text is now noticeably darker for better readability against its tinted background.
- Tag chips in the Filter panel itself now show the same distinct rotating colors as their matching active-filter pills, instead of the plain default styling.

### v2.23 — 8 Sep 2026
- Fixed snapshot comparison + filtering: in the normal ("show all") comparison view, filters (Status, Priority, Tags, etc.) now apply to the faded snapshot bars too, not just the current ones. In "show changes" view, filters now combine correctly with the changed-items view (changed **and** matching the active filters), instead of being ignored.
- Turning on "show changes" against a snapshot with no actual differences now shows a "No changes since snapshot" message instead of a blank chart.
- Fixed a display glitch where a task deleted since the snapshot, if it belonged to a phase or category that still has other tasks, could show up as a disconnected, duplicated section at the very bottom of the chart instead of grouped with the rest of its phase.

### v2.22 — 8 Sep 2026
- Pressing `f` now opens the Filter panel right at your cursor (top-left corner anchored to the pointer, kept fully on-screen) instead of centred over the chart.
- The Filter button now shows a small "×" whenever a filter is active — click the button itself to instantly clear every filter.
- In the Filter panel, **Clear all** moved to sit immediately after the "Filters" title (previously pushed to the far right), and now turns red while any filter is active.
- The active-filter pills below the timeline are easier to read: larger text (matching the Phase row size), a solid (non-transparent) tinted background so chart gridlines no longer show through, upper-case labels (e.g. "STATUS: Done"), and Tags now get their own distinct rotating colors instead of one flat amber.

### v2.21 — 7 Sep 2026
- New **Tags** property: add any number of free-form, comma-separated tags to a task (letters, numbers, dashes, and spaces — commas separate tags) via a full-width field below Progress in the Edit Task modal, either by typing or by picking from a dropdown of tags already in use (which adds to the list rather than replacing it). Tags round-trip through Excel like any other column.
- The Filter panel gained a **Tags** row at the bottom (since the tag list can grow large) — selecting multiple tags is OR, combined with every other filter as AND, same as the existing filters.
- The Filter panel now has a short grace period before it closes when the cursor leaves it, so briefly overshooting doesn't lose your place. Press `f` anywhere in the main view to open it centred over the chart instead of anchored to the Filter button.
- **Flow view is renamed "Linked view"** everywhere in the UI, and its hotkey moves from `f` to `l` (freeing up `f` for the Filter panel above).

### v2.20 — 7 Sep 2026
- In the Add/Edit Task window, choosing the **Done** status now automatically sets Progress to 100%, and Progress reaching 100% now automatically sets Status to **Done**. Status only moves back to **On Track** automatically if you lower Progress after it was at 100% — any other Progress change leaves your chosen Status alone.
- Fixed the Edit modal accidentally closing when you selected text by click-and-drag and released the mouse just outside the modal box — it now only closes when you actually click on the dark backdrop.

### v2.17 — 3 Sep 2026
- New **Flow view**: toggle the chart (button in the toolbar, or press `f`) between the usual date-based Timeline and a new dependency-chain layout, where tasks are arranged left-to-right by what they depend on rather than by date. Handy for following a chain of related tasks without scrolling around the calendar.
- Flow view has its own toolbar controls (Active/Overdue filters, First/Last navigation) and keeps dependency arrows, snapshot-comparison ghost bars, hover tooltips, and click-to-edit all working the same as Timeline view.
- Added a floating **+** button over the chart for quickly adding a new task from either view.

### v2.16 — 21 Aug 2026
- The Add/Edit Task window now has a **Milestone** checkbox next to Title — checking/unchecking it adds or removes the `(milestone)` tag on the title for you, instead of typing it by hand.
- The **Load More Past / Load More Future** buttons are bigger, pinned near the top of the chart area (in line with the first phase row) instead of the vertical middle of the whole chart, and briefly pulse to draw attention.
- Ctrl/Cmd + mousewheel (and trackpad pinch) now zooms the page as expected while the cursor is over the chart area, instead of being silently swallowed.

### v2.15 — 21 Aug 2026
- Starting a new empty chart now begins with one example task already filled in (instead of an empty chart and a blank "Add Task" popup), so there's a row to edit right away.
- In the Add/Edit Task window, changing the Start Date now automatically shifts the End Date to keep the task's original duration. Changing the End Date to a date earlier than the Start Date now automatically moves the Start Date up to match.

---
*Released under the MIT License.*
