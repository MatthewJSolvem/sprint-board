# Sprint Board

A single-file, read-only web app for Scrum on Azure DevOps. It has three tabs:

- **Stand-up**: the current sprint by developer, with blocked, stale and ageing flags.
- **Planning**: the Friday planning view. Build a proposed sprint from the ranked backlog, check it against capacity, and copy the list of changes to make in Azure DevOps.
- **Reporting**: scope growth, completed work and velocity, bugs against tasks, QA waiting against testing, send-backs by root cause, and a stale backlog list.

The app never writes to Azure DevOps. It only reads.

## Use it

1. Open `index.html` in a browser (or host it with GitHub Pages).
2. Press **Settings** and fill in your organisation, project and area path.
3. Paste a Personal Access Token with the **Work Items: Read** scope only, then **Save and load**.
4. To look around without a token, open `index.html#demo`, `#demo-plan` or `#demo-report`.

## Where data is kept

- All data goes directly from your browser to `dev.azure.com`. There is no server.
- The token is kept in the browser's session storage and is dropped when the tab closes, unless you tick "remember".
- Settings and planning drafts are kept in the browser's local storage.

Never commit a token to this repository.

## Settings you will probably need to confirm

| Setting | Default |
| --- | --- |
| Story points field | the Azure DevOps default field |
| Blocked tag | `Blocked` |
| Backlog iteration | `Solvem - SDLC\Unallocated Pool` |
| Backlog tag | `Backlog` |
| QA waiting states | `Ready for QA` |
| QA testing states | `In QA, QA, Testing` |
| Root cause field | `Custom.RootCause` |

Until QA is split into a waiting and a testing state, all QA time on the Reporting tab shows as testing.

## Hosting on GitHub Pages

Settings, then Pages, then deploy from the `main` branch root. If the browser blocks calls to Azure DevOps from the hosted page, open the file locally instead.
