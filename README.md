# Bird Collision Risk Map

A single-page web app to place pins on a campus map, view collision risk per building, and edit the inputs that drive each risk level. Everything runs in the browser—no build tooling required.

## Files
- `index.html` – main app (HTML/CSS/JS).
- `bird_collision_risk.csv` / `bird_collision_risk.xlsx` – data source (CSV is loaded by the app).
- `map.jpg` – base campus map image.

## How to run
1. From this folder, start a simple static server so the browser can load the CSV (fetch is blocked on `file://`):
   - Python 3: `python -m http.server 8000`
   - Node: `npx http-server -p 8000`
2. Open `http://localhost:8000` in your browser.
3. The map appears with tools to place and edit pins.

## Using the app
- **Load data:** CSV loads automatically into the building list.
- **Place a pin:** Pick a building from the dropdown → click **Place pin on map** → click the correct spot on the map. Color = live risk (Low green, Median yellow, High red).
- **Select:** Click a pin or a building in the list to open its details.
- **Edit values:** Adjust Glass / Vegetation / Light / Location / Prevention (0–10). Score and risk update instantly, and the pin color follows.
- **Resize pins per-building:** Use the Pin size slider (200–400px) while a building is selected; only that marker changes size.
- **Rename buildings:** Change the building name in the detail panel; the list, dropdown, and pin tooltip update immediately.
- **Move a pin:** Click **Place pin** again for the same building, then click a new spot.
- **Remove:** Click **Remove pin** with the building selected.
- **Map controls:** Drag to pan; mouse wheel (or pinch) to zoom.
- **Add a building:** Fill out the “Add Building” card (name + scores) and click **Create & place pin**. The new item appears in the list and can be placed like others.
- **Persistence:** Pin positions, edits, new buildings, and pin size are saved to your browser (localStorage). Reloading the page keeps your work.
- **Export/Import:** Use the Backup & Sync card to download your state as JSON and import it on another machine to restore pins and edits.
- **Custom pin icons:** Pins use `green.png`, `yellow.png`, and `red.png` based on risk, and the size slider affects these icons.

## Scoring logic
```
Score = Glass*0.35 + Vegetation*0.25 + Light*0.20 + Location*0.15 + Prevention*0.05
Risk  = Low if Score < 4
        Median if 4 <= Score <= 7
        High if Score > 7
```

## Customization tips
- Update `bird_collision_risk.csv` to change buildings or defaults. Ensure the header row matches the existing column names.
- Swap `map.jpg` with a new map (keep the filename or update the `src` in `index.html`).
- Colors live in `:root` CSS variables in `index.html`.
- Pin positions are stored in-page; reload resets placement. Add a small persistence layer (e.g., `localStorage`) if you want positions remembered between visits.

## Notes
- Everything is written in English per the requirements.
- The design leans on a bird-friendly green palette; adjust as needed to fit your brand.
