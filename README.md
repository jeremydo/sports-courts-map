# Sports Courts Map — Potential Pickleball Sites

An interactive map that finds sports courts near any US location using OpenStreetMap data, and shows the noise/impact radius for each court. Useful for pickleball advocacy, parks planning, or anyone researching court availability in their area.

## Features

- Fetches all sports courts (tennis, basketball, pickleball, multi-sport) within a configurable radius using the Overpass API
- Displays a noise impact radius circle around each court (adjustable 200–1000 ft)
- Clicking a court shows its address (reverse-geocoded via Nominatim), area in sq ft, sport type, and a link to Google Maps satellite view
- Filter by minimum court size
- Satellite imagery overlay (Esri World Imagery), clipped to the selected court's impact circle and blended with the OSM base map
- Excludes non-pickleball-compatible sports (baseball, soccer, equestrian, boules)
- No build step, no API keys required — single HTML file

## Quickstart

1. Download `index.html`
2. Open a terminal in the same folder and run:
   ```
   python3 -m http.server 8765
   ```
3. Open `http://localhost:8765` in your browser

> A local server is required (not `file://`) because the Overpass and Nominatim APIs block direct file:// requests due to CORS.

## Customizing for your location

Edit the `CONFIG` block near the top of `index.html`:

```javascript
const CONFIG = {
  lat:          39.7392,       // Center latitude  (decimal degrees)
  lng:         -104.9903,      // Center longitude (decimal degrees, negative = West)
  locationName: 'Denver',      // City / area name used in titles and status messages
  defaultSearchMiles: 5,       // Starting search radius shown on page load (1–15)
};
```

To find coordinates for your location, right-click any point in Google Maps and copy the lat/lng shown at the top of the context menu.

## Deploying publicly

Because this is a single static HTML file with no backend, it can be hosted for free on several platforms with no server administration required.

### Option A: GitHub Pages (easiest, free)

1. Fork this repository on GitHub
2. Edit `index.html` to set your `CONFIG` values (you can do this directly in the GitHub web editor)
3. Go to your fork's **Settings → Pages**
4. Under **Source**, select **Deploy from a branch**, choose `main`, folder `/root`, and click Save
5. Your map will be live at `https://<your-github-username>.github.io/sports-courts-map/` within a minute or two

### Option B: Netlify (free, drag-and-drop)

1. Edit `index.html` with your `CONFIG` values
2. Go to [netlify.com](https://www.netlify.com) and create a free account
3. From the dashboard, drag and drop your `index.html` file onto the page
4. Netlify gives you an instant public URL — you can set a custom domain in settings

### Option C: Any static web host

The file has no server-side dependencies. Upload `index.html` to any web host (shared hosting, S3, Cloudflare Pages, Vercel, etc.) and it will work. The only requirement is that it is served over HTTP/HTTPS — not opened directly as a `file://` URL.

## Data sources

- Court geometry: [OpenStreetMap](https://www.openstreetmap.org) via [Overpass API](https://overpass-api.de)
- Address lookup: [Nominatim](https://nominatim.openstreetmap.org)
- Satellite imagery: [Esri World Imagery](https://www.arcgis.com/home/item.html?id=10df2279f9684e4a9f6a7f08febac2a9)
- Map tiles: [OpenStreetMap](https://www.openstreetmap.org)

If courts are missing in your area, you can add them directly on [openstreetmap.org](https://www.openstreetmap.org/welcome) — the map will reflect edits within a day or two.

## Adding courts to OpenStreetMap

If you know of courts that aren't showing up, the data gap is in OpenStreetMap itself. You can fix this:

1. Create a free account at [openstreetmap.org](https://www.openstreetmap.org/user/new)
2. Navigate to the location and click **Edit**
3. Add the court as an area with tag `leisure=pitch` and `sport=tennis` (or `basketball`, `pickleball`, etc.)

## License

MIT
