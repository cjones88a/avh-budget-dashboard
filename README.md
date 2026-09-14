# AVH Budget Burndown

Static dashboard published to GitHub Pages. `index.html` reads `time_entries.csv`
in this same folder at load time and recomputes every number in the browser —
no build step, no server.

## Updating it (weekly)

1. Export the current time entries from Basecamp:
   https://mapletonhillmedia.basecamphq.com/projects/15410215-contentful-build/time_entries
2. Replace `time_entries.csv` in this folder with one row per entry, columns:
   `date,person,hours,description`
   - `date`: `YYYY-MM-DD` (preferred) or `MM/DD/YYYY`
   - `description`: should start with the AVH## scope code, e.g. `AVH21 - Standup`.
     Rows without a code are folded into AVH21 and called out on the page.
     `AHV##` is auto-corrected to `AVH##` (a known typo in the time tool).
3. Commit and push:
   ```
   git add time_entries.csv
   git commit -m "Update time entries"
   git push
   ```
4. Refresh the GitHub Pages URL — the new totals appear immediately, no other
   file needs to change.

## Changing the budget itself

The per-line-item estimates (hours/$ per AVH## code) are NOT in the CSV — they
only change when the Scope & Time Tracker itself changes (a new SOW, a change
order, etc.). To update them, edit the `budgetItems` array near the top of the
`<script>` block in `index.html`.
