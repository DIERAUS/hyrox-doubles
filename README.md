# Doubles

Race-target calculator and the 8-week HYROX Doubles training block, built for Paris in December 2026.

Published at https://dieraus.github.io/hyrox-doubles/ and embedded in Notion.

## The sync seam

`index.html` contains a block marked `BEGIN SYNC DATA` / `END SYNC DATA`:

```js
const DATA = { syncedAt: null, stations: {}, runPace: null };
```

Nothing in it is typed by hand. A scheduled job replaces that object and pushes,
and GitHub Pages redeploys. Any station key present in `DATA.stations` overrides
the estimated split in the table; `syncedAt` drives the "Synced N/8 measured" label.

Station keys must match the names in the `STATIONS` array exactly, e.g. `"1000 m SkiErg"`.

## Why the data isn't fetched in the browser

Hevy and Strava send no CORS headers for browser origins, and their credentials
can't sit in a page this public. So the data is baked in by a job that holds the
keys server-side. Swapping to live fetches means standing up a JSON endpoint and
pointing the page at it — the page structure already allows for that.
