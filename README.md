# Gantt Chart Builder

**Live App:** [https://kolfers.github.io/public_excel_to_gantt_standalone/](https://kolfers.github.io/public_excel_to_gantt_standalone/)
**GitHub Repository:** [https://github.com/kolfers/public_excel_to_gantt_standalone](https://github.com/kolfers/public_excel_to_gantt_standalone)

Turn your Excel plan into an interactive Gantt chart. One self-contained HTML file: no server, no installation, no network requests. Everything runs in your browser and your file is never uploaded.

Desktop browsers only (Chrome or Edge recommended; see [Saving](#saving)).

## Quick start

1. Open `index.html` (or the live app) in a modern desktop browser.
2. Click **Open Excel file**, or drop an `.xlsx` / `.xlsm` file onto the drop box. Your two most recent files are listed under **Recent** (Chrome / Edge). Use **Try styles** above the drop box to pick dark or light mode and a colour palette.
3. The chart renders immediately.

No plan yet? Click **Try example chart**, **Start an empty chart** (the app asks you for your first task), or **Download template**. **Download the app for offline use** saves this page as a single file you can keep.

The example chart opens with a short guided tour of the main features. **Stop tour** ends it, **Don't show again** switches it off (turn it back on in Settings), and the **?** button at the right end of the nav row replays the tour for the view you are in.

## Your Excel file

The workbook can have three sheets:

| Sheet (accepted names) | Purpose |
|---|---|
| `Current Planning` (or `Sheet1`, `Sheet 1`, otherwise the first sheet) | One row per task |
| `Log` (or `Sheet2`, `Sheet 2`) | Snapshot history, written by the app |
| `Gantt Settings` (hidden) | Plan settings shared by everyone who opens the file, written by the app (see [Saving](#saving)). Do not edit it by hand. |

Only **Title** is required. Header names are matched case-insensitively. Columns you add yourself are kept and written back untouched.

| Column | Description |
|---|---|
| `ID` | Filled in automatically (`T-001`, `T-002`, ...). Leave blank for new rows and do not change existing IDs. Duplicate IDs are renamed on load. |
| `Phase` | Top-level group. Default `Phase 1`. |
| `Category` | Group within a phase. Default `Category 1`. |
| `Title` | **Required.** Add `(milestone)` to mark a milestone. |
| `Status` | `Done`, `On Track`, `Behind`, `Waiting`, `On Hold`. |
| `Start Date`, `End Date` | Optional: a task with no dates starts today and ends 6 days later; with one date, the other is set 6 days away. `DD-Mon-YYYY` (for example `12-Mar-2026`), `YYYY-MM-DD` or a real Excel date. Avoid text like `12/03/2026`, which is ambiguous. |
| `Progress` | 0-100. |
| `Priority` | `High`, `Medium` or `Low`. |
| `Dependency` | IDs of the tasks this one depends on, separated by commas. A task title also works and is converted to the ID. |
| `Owner` | Person responsible. Can be filtered and used for grouping. |
| `Tags` | Comma-separated labels. |
| `Description` | Free text. |
| `Subtasks` | Optional checklist: one line per subtask, `- [ ] text` (open) or `- [x] text` (done). |
| `Comments` | Managed by the app, as `[DD-Mon-YYYY HH:MM:Name] text` entries. |

Rows without a title are skipped (and kept in the file). Missing or unreadable dates get the defaults above; an **Import report** summarises what was skipped or filled in, with per-row details on request.

## Using the chart

- **Views:** six tabs, switched with `l` / `Shift+L`.
  - *Timeline*: tasks as bars on a calendar.
  - *Dependencies*: tasks laid out left to right by what they depend on.
  - *Roadmap*: one row per phase or category, for the big picture.
  - *Table*: one row per task with sortable, reorderable columns.
  - *Board*: a kanban board by status or priority; drag a card to change it; hide and reorder the columns with Panels ▾ or by dragging a column title, restore the default layout with **Reset view**, and create your own statuses with + New status (or Custom… in a task's Status list); the coloured edge of each card shows its phase or category (Settings).
  - *Matrix*: urgency by importance, in four quadrants; the coloured edge of each card shows its phase or category (Settings); drag a card to change its priority or due date; Done tasks are shown (hide them with the Active or Status filter); dropping a Done task on Do or Delegate explains why it can't go there and offers to hide Done tasks; **Reset view** restores the default rules.
- **Reorganise in the left panel:** drag a task onto another category to move it there, a category onto another phase, or a phase above or below another to reorder the phases (one undo step each). If the task has linked tasks (parents or children), you are asked whether to move them too; choose a default in Settings → Dependencies.
- **Collapsed phases and categories:** in the Timeline and Dependencies charts a collapsed category shows **show category: Category**, and with Phase rows in the chart off a collapsed phase shows **show phase: Phase**; click it to expand.
- **Order:** in Timeline and Dependencies the **Order** button (next to the New Task button) sets how tasks are ordered within each category. Tick the criteria to use (priority, days late, dates, urgency, progress, status and more), flip each between ascending and descending and drag them into priority order; use one order for both views or one each. It is saved in this browser, not in the Excel file, and Reset to default restores today's order (priority, days late, start date).
- **Zoom:** Week / Month / Quarter / Year, `+` / `-` or Ctrl + scroll for finer steps (in Dependencies they make the bars wider or narrower), **Fit project**, **Today** (`t`). `v` cycles the levels.
- **Reset view:** appears in the nav row of every view once you change the view's layout or turn on a filter; one click restores the view's defaults and clears all filters (your data and browser settings stay).
- **Edit:** double-click a bar or row (or press `e`) to open the task modal. Drag a bar to move it, drag its edges to resize (snaps to days). `d` adds a task that depends on the hovered one, `n` duplicates, `s` adds a parent task. Tags are pills: type to add one (new tags too), click a pill to remove it. Subtasks: in the task window, Description has a Subtasks checklist under it (add with +, tick, edit in place, drag to reorder; Enter adds one below, Backspace on an empty one deletes it, Alt+↑/↓ moves it; the Convert button turns the subtasks into a chain of linked tasks before or after the task, or into separate parents or children of it; each subtask also has its own Convert button). Board and Matrix cards, the Table and the hover cards show how many subtasks are done. Ticking subtasks sets the task's progress to the share done (all done = Done); turn the checklist off in Settings → Subtasks. Closing the task window with unsaved edits offers Save, Discard or Cancel and can list what changed. Save & Close turns green while there are unsaved changes. Mark a task done with the ✓ in its hover menu or the Done switch in the task window.
- **Link tasks:** hover a bar and drag the ◁ at the start of its hover menu onto the task it should wait for (its parent), or the ▷ at the end onto a task that should wait for it. Click a dependency line to remove it.
- **Select several tasks:** Ctrl/Cmd+click, Shift+click for a range, Alt+click for a task and everything downstream. A bulk bar offers Status, Priority, Move to, Shift dates, Tags and Delete.
- **Undo / redo:** Ctrl+Z, Ctrl+Shift+Z or Ctrl+Y. Every bulk action is one step.
- **Filters and search:** All / Active / Overdue, a filter panel (`f`) with Status, Priority, Owner, Tags and more, group by owner, and task search (`/`).
- **Check dependencies:** finds overlaps, cycles and missing references, and offers fixes with a preview.
- **Compare** (Timeline, Dependencies and Table): tick **Show changes since** and pick a snapshot to see ghost bars and a Changes panel (added, delayed, completed, ...). Hovering a task shows what changed since the snapshot (old → new). Snapshots can be named and one can be marked as the baseline.
- **Export:** the **...** menu offers 16:9 **slides** (PNG, SVG or clipboard): the timeline (rolled up to phases, categories or tasks), the changes since a snapshot, the milestones and a one-page status; and a read-only **interactive HTML** copy you can share. Slides are made for presentations: pick any of the app's colour palettes, light or dark, add a subtitle, and get a sharp 3840 × 2160 PNG (or Standard 1920 × 1080).
- **Settings** (the gear): grouped into foldable sections (click a section's title to fold or unfold it; only File is open at first): File (save as, **New chart** opens the start screen in a new tab, export, reload, import report, auto-save) and Display (theme and palette buttons, legend, the Hotkeys strip, compact rows, phase and category rows in the chart, colour items by phase or category, status indicators left or right of the title), then hover info (Compact, Full, Side pane or Off; the left panel's task rows show the same hover card), the Subtasks switch, Dependencies (check dependencies, moving linked tasks, uniform bar width) and Help (keyboard shortcuts and the guided tour). Every setting is tagged (browser) or (excel) to show where it is saved, and there are two reset buttons: Reset browser settings and Reset Excel settings. **Info** (`i`) is a built-in guide to the app. Both panels stay docked to the side so the chart remains usable.
- **Appearance:** several colour palettes (Catppuccin, Dracula, Monokai and more), light and dark mode (`m`, `p`), and a compact left panel for narrow windows. The Hotkeys strip at the bottom shows the keys for what is under the mouse. Press `?` for the full list of shortcuts.

## Saving

- **Save Excel** (Ctrl+S) writes your changes into the original workbook, keeping its formatting and Excel Tables, and appends a snapshot to the `Log` sheet. In Chrome and Edge a file opened with **Open Excel file** or **Recent** is saved in place; a dropped file or another browser downloads a copy instead.
- **Excel settings** (hover panel, Table columns, Board, Matrix and Roadmap layout, custom statuses, ...) are stored in the workbook's hidden `Gantt Settings` sheet, so everyone who opens the file sees the same layout. Personal settings (theme, palette, zoom, filters, compact rows, colour by, status indicators, ...) stay in your browser.
- **Auto-save** (optional, Chrome / Edge) saves the planning sheet about a second and a half after each edit.
- If a save fails the app retries three times, then shows **Not saved** and opens a dialog with tips and Retry, Save as... and Download copy. The most common cause is the file being open in Excel: close it there and click Retry. A recovery copy is kept in your browser, and the app offers to restore it the next time you open that file.
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

## Changelog

### v3.0.81 — 29 Oct 2026
- Matrix: dropping a Done task on Do or Delegate now explains why it can't go there, with a button to hide Done tasks.

### v3.0.80 — 28 Oct 2026
- Task window: Save & Close turns green when there are unsaved changes, and so does Save in the unsaved-changes prompt.

### v3.0.79 — 27 Oct 2026
- If saving to your Excel file fails (for example because it is open in Excel), a dialog now explains how to fix it and offers Retry, Save as… or Download copy.

### v3.0.78 — 26 Oct 2026
- Compare: the compact hover card now lists what changed since the snapshot (old → new for dates, status, progress and more).

### v3.0.77 — 26 Oct 2026
- Timeline and Dependencies: the Order button now sits right next to the New Task button.

### v3.0.76 — 25 Oct 2026
- Slide exports have a cleaner, presentation-ready look and can use any of the app's colour palettes, light or dark, as sharp 2x PNGs.
- Timeline and Dependencies: a new Order button sets how tasks are ordered within each category (priority, dates, urgency, progress and more, each ascending or descending, in the order you drag them), for both views or each separately; saved in this browser.
- Settings are regrouped: dependency tools and options share a Dependencies section, Keyboard shortcuts and the tour are under Help, Import report is under File, and choice buttons are only as wide as their labels.
- Board and Matrix: the Show done switch is gone; Done tasks are always shown (hide them with the Active or Status filter, or Panels ▾ on the Board).
- Checkboxes (subtasks, column and panel lists, pickers) follow the colour palette instead of showing white in dark mode.
- Left panel: late tags read "3d late" instead of "(3d late)".
- Search: on a narrow window the results are no longer covered by the date header in Timeline and Dependencies.

### v3.0.69 — 23 Oct 2026
- Left panel: hovering a task shows the same details card as its bar in the chart, kept inside the panel.
- Hover cards show how many of a task's subtasks are done.
- Subtasks: a task without subtasks shows an empty subtask row, so you can start typing right away.
- Subtasks: Convert can now make each subtask a separate parent or child of the task, and each subtask has its own Convert button.
- Task window: the unsaved-changes prompt now has a Save button and can show a short list of what changed.
- Settings panel: sections fold and unfold (only File is open at first), and their contents are indented for an easier read.

### v3.0.63 — 23 Oct 2026
- Moving a linked task to another phase or category asks whether to move its linked tasks too (just this one, those in the same group, or all); choose a default in Settings → Dependencies.
- Subtasks: give a task a checklist in its edit window (new optional Excel column "Subtasks"); ticking subtasks sets the task's progress. Turn it off in Settings → Subtasks.
- Subtasks: a Convert button turns a task's subtasks into a chain of linked tasks, before or after the task.
- Subtasks: Board and Matrix cards show a done/total subtask count, and the Table has a Subtasks column.
- Left panel: hovering a task shows one hover box again, not two overlapping ones.

### v3.0.58 — 22 Oct 2026
- Timeline and Dependencies: the "show phase:" / "show category:" buttons are now square, dashed-outline bars with a ▶ triangle, so they no longer look like items.

### v3.0.57 — 20 Oct 2026
- Timeline and Dependencies: the "show phase:" and "show category:" buttons now start at the middle of the chart, so they line up.
- Left panel: a late item's "(3d late)" tag now always sits right of its title, whichever side the status dot is on.

### v3.0.55 — 13 Oct 2026
- A clear "New Task" button now sits at the far left of the toolbar in every view (just "+" when space is short).
- Starting an empty chart now welcomes you and opens the New task form for your first task.
- Dependencies view: a bar too narrow for its title now shows the full title next to it, like the Timeline.
- Roadmap bars now use the same phase colours as the other views; a dot in each bar shows its status.
- Status indicators in one place: the status dot, late mark and milestone diamond now sit left of the title in every view (Settings → Display → Status indicators switches them to the right).

### v3.0.50 — 12 Oct 2026
- Colour by phase or category: Settings → Display → Colour items by colours bars, cards and left panel rows in every view by phase (now the default) or by category; choose Category to get the previous look back.
- Board and Matrix: the coloured left edge of each card now shows the task's phase instead of its category.

### v3.0.48 — 12 Oct 2026
- Hover texts: the "!" for a hidden dependency, Matrix pane titles, category counters and Check dependencies now show a bold heading with the details on separate lines or as a list.
- Filter chips are easier to read: Status and Priority chips now have a soft coloured background with normal text, over the chart and in the Filter panel.
- Matrix: dragging a card where only one change is possible (for example into Do, which only sets the priority to High) now applies it at once, with an undo hint, instead of asking first.
- Roadmap, Table and Board: an empty row at the top keeps active filter chips from covering the headers.
- Reset view now appears in every view whenever you change the view or turn on a filter, and one click restores the view's defaults and clears all filters (including Phases / Categories).
- Guided tour: the Left panel step now mentions drag and drop, and the chart steps explain linking with the ◁ / ▷ buttons in a bar's hover menu.
- Export: three new slides: changes since a snapshot (summary numbers, the moved bars and the biggest changes), milestones, and a one-page status summary.
- Roadmap: picking a task in the search box now opens its phase (or category) list with the task highlighted.

### v3.0.40 — 12 Oct 2026
- Task window: the Done and Comments switches now show a checkmark and a comment icon before their labels.
- Timeline: the full title shown after a narrow bar is now solid, so dependency lines and the Today line no longer show through its letters.
- The Info and Settings panels now end above the bottom row, so the legend, hotkeys and theme buttons stay visible while they are open.
- Start screen: the dark/light and palette buttons now sit in a "Try styles:" row just above the drop box.
- Settings: a new **New chart** button below Save as… opens the start screen in a new tab.
- Settings: regrouped into File, Tools and Display sections, with the theme and palette buttons, a (browser)/(excel) tag on every setting, and a new Reset Excel settings button.
- Opening a workbook now only needs a Title column: tasks without dates start today and end 6 days later, and the Import report summarises every default it filled in, with per-row details on request.
- Timeline and Dependencies: phase rows are now hidden by default (a thin line separates phases); Phase rows and Category rows in the chart are now saved in your browser instead of the Excel file, with shorter descriptions in Settings.

### v3.0.32 — 11 Oct 2026
- New guided tour: the example chart walks you through the main features, and the ? button at the right of the nav row replays the tour for the current view (switch it off in Settings).
- Timeline and Dependencies: a collapsed category now shows a clearer "show category: …" button, and with Phase rows in the chart off a collapsed phase shows "show phase: …".
- Timeline and Dependencies: hovering the "!" next to a bar now tells you which predecessor is hidden in a collapsed phase or category and that clicking it shows it.

### v3.0.29 — 10 Oct 2026
- Board: drag a column title left or right to reorder the columns.
- Board and Matrix: the highlighted (current) card now stands out with a coloured outline and a slight lift instead of a fill, so its text stays easy to read.
- Dependency lines: only the task you last hovered or clicked has its lines highlighted; earlier highlights clear right away.
- Timeline: clicking a task bar now just selects it; the chart no longer jumps sideways.

### v3.0.25 — 9 Oct 2026
- Bar hover buttons now open with the edit button above the mouse and follow it along long bars, so they no longer end up off-screen.
- Zooming between Month and Week with Ctrl + scroll or `+` / `-` now goes in smaller steps instead of one big jump.

### v3.0.23 — 9 Oct 2026
- Compact hover card: bold Priority, Owner, Tags and Description labels, the priority in its colour, and when the task last changed (from the Excel Log).
- Timeline: clicking a task in the left panel now scrolls the chart so the task's start is under the Today button, like search, without scrolling up or down.

### v3.0.21 — 9 Oct 2026
- Bar hover menu in Timeline and Dependencies: the link triangles moved into the menu (◁ parent first, ▷ child last), the Comments button is gone (press `c` or open the task), and the eye is no longer accent-coloured.
- Hover info in Timeline and Dependencies now has four modes in Settings: Compact (new default: priority, owner, tags, a bit of the description and the latest comment), Full, Side pane and Off.
- New Hotkeys strip at the bottom: shows the keyboard shortcuts for the task, row or chart space under the mouse (or the current task); fold it like the legend or switch it off in Settings.
- Timeline and Dependencies: the legend row at the bottom now spans the full window width, under the left panel, as in the other views.

### v3.0.17 — 9 Oct 2026
- Timeline and Dependencies: drag from the triangle at either end of a bar onto another bar to link them, and click a dependency line to remove the link.
- Mark a task done in one click: a ✓ in the bar hover menu and a Done switch next to View in the task window.
- Task window: tags are now removable pills, as in the Filter panel; type to add an existing or a new tag.

### v3.0.14 — 8 Oct 2026
- Timeline and Dependencies: a collapsed category now shows "show: Category" in the chart (click to expand), and Settings → Category rows in the chart draws category title rows like the phase rows.
- Board and Matrix: a Reset view button appears in the nav row when you have changed the view's layout, and puts it back to the defaults in one click.
- Clicking the Info button again now closes the Info panel.

### v3.0.11 — 7 Oct 2026
- **Custom statuses.** Pick Custom… in a task's Status list, or + New status in the Board's Panels menu, to create your own status. Each gets its own colour and is saved in the Excel file.
- **Board by status or priority.** The Board can now show a column per priority instead of per status, and Panels ▾ lets you hide and reorder the columns; Swimlanes is now a dropdown.

### v3.0.9 — 6 Oct 2026
- **Jump to a task from the eye menu.** Choosing a view from the eye ("Show in view…") now scrolls so the task's start sits under the Today button (or the Uniform button in Dependencies), and the eye is also at the end of the hover buttons on bars in the Timeline and Dependencies views.
- **Zoom the Dependencies view.** Ctrl/Cmd + scroll, a trackpad pinch or `+` / `-` now make the bars wider or narrower (Narrow, Medium, Wide) instead of zooming the whole page.
- **Late items show a red "!".** In the Timeline and Dependencies views, late tasks no longer get an outline; a red exclamation mark appears next to the status dot instead.
- **Left panel Full / Compact is a browser setting.** Your choice now applies to every file you open in this browser and is no longer remembered per file.
- **Filter pills.** Tags, Phase and Category in the Filter panel show your picks as pills you click to remove, and the All button no longer looks selected while a filter is on.
- **Phase and Category pickers in the task window.** They now suggest existing values as you type, show a grey completion that Tab accepts, keep a new value when you press Enter, and have a ▾ arrow that lists everything.
- **Roomier task window.** The title now has its own full-width row, and the Milestone switch sits next to Status and Priority.
- **Custom statuses and import report.** A status such as "In Progress" no longer triggers the import report and can now be picked in the task window, the bulk Status menu and the Filter panel. Unresolved dependencies in the import report have an Edit link that opens the task.
- **Search jumps to the task.** Picking a task in the search box now scrolls the view to it, vertically centred, with its start under the Today button.

### v3.0.0 — 5 Oct 2026
- **A complete rewrite.** Version 3 opens your existing workbooks and adds six views: Timeline, Dependencies, Roadmap, Table, Board (kanban by status or priority) and Matrix (urgency by importance). See "Coming from version 2?" below for what changed.
- Saving writes into your original workbook and keeps its formatting and Excel Tables. Plan settings are shared through a hidden `Gantt Settings` sheet, and the `Log` sheet is now a compact history.
- If a save fails the app retries, offers Save as... and keeps a recovery copy in your browser. If the file changed on disk, changes are merged and you are only asked about real conflicts.
- Compare against a snapshot with ghost bars and a Changes panel, now with a snapshot picker in the navigation row.
- Select several tasks and change them together with the bulk bar; every bulk action is one undo step.
- Better filtering, a docked Settings panel and Info guide, a more compact left panel, and Matrix cards with due tags.
- Timeline and Roadmap header labels now thin out at regular calendar intervals so they never overlap, however far you zoom out or narrow the window.

---
*Released under the MIT License.*
