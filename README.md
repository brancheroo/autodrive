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

C camera (interior / exterior / overhead / drone circle / drone follow / helicopter) · drag pan · wheel zoom · Space pause · W weather · X chaos ·
P oil protest · R AI Radio (songs written live about where you are) · S tracking satellite on/off (3 km prediction-based self-driving, any car) · I trip &amp; data panel on/off · T Techno FM (generated live, 25–200 BPM from speed &amp; situation) · D window dog · N reroute now · K chase mode (1–10 police) · E express (chase driving, no police) · click the in-car screens (interior view) · time slider 1–1000×.
