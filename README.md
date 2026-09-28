# AVH Budget Burndown

Static dashboard published to GitHub Pages. `index.html` looks for a CSV export
in this same folder at load time and recomputes every number in the browser,
no build step, no server.

## Updating it (weekly)

1. Export the current time entries from Basecamp:
   https://mapletonhillmedia.basecamphq.com/projects/15410215-contentful-build/time_entries
2. Save that export into this folder as either `time-report.csv` or
   `time_entries.csv` (the page tries both names in that order, so whichever
   one Basecamp gives you that week just works). Whatever extra columns
   Basecamp adds (`todo`, `list`, `company`, `project`, ...) are ignored;
   the page only reads:
   `date, person, hours, description`
   - `date`: `YYYY-MM-DD` (preferred) or `MM/DD/YYYY`
   - `description`: should start with the AVH## scope code, e.g. `AVH21 - Standup`,
     with or without a hyphen (`AVH-21` also works).
     Rows without a code are folded into AVH21 and called out on the page.
     `AHV##` is auto corrected to `AVH##` (a known typo in the time tool).
   - Delimiter (comma or tab) and a leading UTF-8 BOM are both handled
     automatically, no reformatting needed, just save what Basecamp exports.
3. Commit and push (replace the filename below with whichever one you saved):
   ```
   git add time-report.csv
   git commit -m "Update time entries"
   git push
   ```
4. Refresh the GitHub Pages URL, the new totals appear immediately, no other
   file needs to change.

## Changing the budget itself

The per-line-item estimates (hours/$ per AVH## code) are NOT in the CSV, they
only change when the Scope & Time Tracker itself changes (a new SOW, a change
order, etc.). To update them, edit the `budgetItems` array near the top of the
`<script>` block in `index.html`.
