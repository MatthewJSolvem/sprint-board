# Sprint Board

Single-file HTML app for scrum sessions. Four screens: Sprint overview, Developer board, TMT tracker, Skills and assignments.
Open `index.html` from GitHub Pages (or any static host). There is no build step.

## Token
Create an Azure DevOps personal access token with **Work Items: Read and Write**, paste it into Settings.
The token stays in the browser (session storage, or local storage if you tick "Remember"). **Never commit a token to this repository.**

## What it writes to Azure DevOps
- Dragging a card changes `System.State`. Dragging to Done also sets Remaining Work to 0.
- Picking a size writes Original Estimate (S 2, M 5, L 14, XL 24 hours). If the item is not in a Proposed state, only Original Estimate is written; otherwise Remaining Work is written too.
- Assign on the Skills screen writes `System.AssignedTo`.

## Test rejected rework
Bugs and tasks have a boolean field called **Test Rejected**. When it is true, QA or the client returned the item because of a developer fault. The board finds the field by its display name "Test Rejected" (override it in Settings under Fields; a warning shows if it is not found).
- Kanban: the card has a red border, a "Test rejected" tag and a **Rework 1 h / 3 h / 5 h** picker. Rejected cards sort to the top of each lane.
- Burndown: the blue line is planned work without rejected items. A red line shows the rework hours you picked for open rejected items.
- Rework is separate effort. It is not counted in hours committed, completed work, scope change or sprint health.
- The 1 / 3 / 5 h picks are kept in the browser only (local storage). **Nothing is written to Azure DevOps for them.** Other people and other browsers do not see them.

## Notes and dependencies on cards
Each Kanban card has an icon: grey = has a note, amber = waiting on another developer, red = overdue (waiting longer than the stuck days, promised date passed, or the linked item is blocked), green = dependency cleared. The developer being waited on sees an "others are waiting" icon on the linked card.
Everything is stored in Azure DevOps so it is visible there too:
- **Comments** on the work item: notes, and dependency events that start with `[Board]` (waiting on, promised date changed, promise missed with reason, completed).
- **Tags**: `Waiting-<developer>` while waiting, `Dep-Cleared` once cleared.
- **Predecessor link** (`System.LinkTypes.Dependency-Reverse`) when a specific card is chosen.
One active dependency per card. The token needs Work Items: Read and Write (comments and links included).

## Notes
- States, work item types and field names are read from Azure DevOps. Client, Severity, Priority and Due Date fields are found by name; override them in Settings if needed.
- Master Tracker children are found through parent links (recursive). Finished Master Trackers (Completed category) are hidden.
- Photos and the skills matrix live in the browser. Use Photos and data to export or import them as text.
- Add `#demo` to the address to try it with invented data.
