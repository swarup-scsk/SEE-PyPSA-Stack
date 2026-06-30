# GB Stack Model — Network Explorer (Pass 1)

A first-pass front end for the SEE PyPSA stack model: renders the GB network on a map
with click-to-drill-down, plus the price/demand forecast chart. Built against Owen's
sample network object (gb_ecmwf_00z_base_milp).

## What's here
- `index.html` — the whole app (deck.gl + MapLibre + ECharts, no build step)
- `data.json` — the data layer, extracted from the sample network object (.nc)

## What it shows
- GB map: generators as dots (size = capacity, colour = fuel type)
- Interconnectors as arcs to real neighbour locations (width = capacity)
- Click a generator -> its attributes + modelled output over the window
- Click an interconnector -> its flows
- Bottom chart: GB day-ahead price + demand across the forecast window

Note: generator positions are schematic (the model is zonal — plant coordinates are
not in the file). Interconnector endpoints use the real bus coordinates.

## How to view it

### Option A — deploy to Vercel (recommended, gives a shareable URL)
1. Create a new repository in your SCSK GitHub (e.g. `gb-network-explorer`).
2. Upload these two files (`index.html`, `data.json`) to it
   (GitHub web: "Add file" -> "Upload files", or GitHub Desktop drag-and-drop).
3. Go to vercel.com -> "Add New… -> Project" -> "Import" your repo.
4. Framework preset: "Other" (it's a static site). Click Deploy.
5. Vercel gives you a URL — open it. Done.
   Every time the files change in GitHub, Vercel redeploys automatically.

### Option B — run locally (needs a tiny web server, not just double-click)
Because the app loads data.json, it must be served over http, not file://.
In this folder run:  `python -m http.server 8000`
then open http://localhost:8000

## Next iterations
- Wire to Owen's live FastAPI run endpoint (needs API access via Paul)
- Scenario controls (edit inputs -> re-run -> compare vs base)
- Real plant coordinates if/when available; richer drill-down
- Graduate into a full Next.js app for the data-heavy phase
