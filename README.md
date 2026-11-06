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

## Notes
- States, work item types and field names are read from Azure DevOps. Client, Severity, Priority and Due Date fields are found by name; override them in Settings if needed.
- Master Tracker children are found through parent links (recursive). Finished Master Trackers (Completed category) are hidden.
- Photos and the skills matrix live in the browser. Use Photos and data to export or import them as text.
- Add `#demo` to the address to try it with invented data.
