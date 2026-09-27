# Autodrive

Browser-based self-driving ride simulator (three.js). Streams live OpenStreetMap, satellite imagery,
terrain, routing, chargers and weather.

## Run

Serve this folder (needed for the offline region packs):

    python3 -m http.server 8766 -d autodrive

then open http://localhost:8766. Opening `index.html` directly (file://) also works, but offline packs
are then ignored and everything streams from the internet.

## Offline region packs (`regions/`)

| Pack | Contents |
|---|---|
| `regions/sanfrancisco/` | 175k LiDAR-measured building footprints + median/peak roof heights (DataSF "Building Footprints", ODC-PDDL). Replaces OSM building outlines inside San Francisco. |
| `regions/losangeles/` | 885k LiDAR-measured building outlines + roof heights (LA County LARIAC 2020) from Santa Monica/Venice to Downtown/East LA, LAX to Hollywood. |
| `regions/roseville/` | Full OSM data for every map tile (same query the game uses), Esri imagery z14/z17 citywide + z19 for Downtown/Vernon St, the Galleria and I-80 interchanges, Terrarium terrain z15, geotagged Wikimedia Commons photos. |

The game reads `regions/index.json` at startup; inside a pack's bounding box it loads local files first
and falls back to the internet for anything missing.

Rebuild / refresh:

    python3 regions/fetch_region.py roseville
    python3 regions/fetch_sf_buildings.py
    python3 regions/fetch_la_buildings.py

## Data & credits

Map data © OpenStreetMap contributors (ODbL) · OpenFreeMap (backup vector tiles) · Routing: OSRM ·
Geocoding: Photon · Elevation: AWS Terrain Tiles / Open-Meteo · Imagery © Esri, Maxar, Earthstar Geographics ·
Chargers: US DOE AFDC (developer.nlr.gov) · Textures: Poly Haven (CC0) · Photos: Wikimedia Commons (per-photo licence shown in game) ·
SF buildings: DataSF · Signs & street names: OpenStreetMap · Live vocals: meSpeak (eSpeak, GPL) · LA buildings: LA County LARIAC · Radio: KEXP, KQED, WNYC, BBC World Service, Jazz Radio.

## Controls

C camera · Space pause · **Esc pause menu** · **? all shortcuts** · E driving style (Normal / Comfort / Express) · H take over (arrow keys drive) · K police chase · X chaos · W weather · P protest · N reroute · S tracking satellite · I trip panel · D window dog · T Techno FM · R AI Radio · V emergency vehicle · F photo mode · M rear-view mirror · B cinema mode · ` performance profiler.
Gamepads and touch screens are supported. Drag to look around, wheel/pinch to zoom.

## Start screen

Game mode (free ride, robotaxi business, career, daily challenge, Cannonball Run, rush hour, fuel-economy, scavenger hunt, hurricane evacuation, rally, driver's test) with local leaderboards and share codes · 22 cars, each graded on driving skill · driving style · graphics quality · weather (incl. fog, dust storm, wildfire smoke) · your rider's outfit, face and hair · passengers (companions, kids, mood, cat, parrot) · garage (paint, wraps, decals, upgrades, repairs) · time-trial ghost · live AI rival · delivery run · shareable trip links · resume a saved trip.

## In the ride

🎬 in-car activities · 📔 road-trip journal · 🧪 scenario editor · ◧ split-screen · 📥 save the route for offline use · 🐞 debug log · ⚙️ switch any feature off · ♿ accessibility & 5 languages (pause menu).

## Code layout

`autodrive/index.html` is the core; features live in `autodrive/mods/*.js` and `python3 autodrive/build.py` inlines them so the published page stays one file. Add `?selftest` to the URL to start a ride in every car and check each keeps running.
