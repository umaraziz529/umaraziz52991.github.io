# Local Weather (educational)

Static site: HTML + CSS + vanilla JS. Weather from [Open-Meteo](https://open-meteo.com/) (no key), place names from BigDataCloud's free client endpoint. No backend, no secrets.

When a visitor allows location using the Detect button, the page POSTs `{ latitude, longitude, accuracy }` as JSON to the same site's `/api/location` endpoint. Configure that endpoint in your backend and change `LOCATION_ENDPOINT` in `app.js` if needed. The endpoint must accept POST requests; a static host such as GitHub Pages cannot receive this request by itself. Delivery failures are shown in the page.

## Structure
```
weather-site/
├── index.html
├── css/style.css
├── js/app.js
└── README.md
```

## Run locally
Geolocation needs `localhost` or HTTPS (opening index.html as file:// may be blocked).
```
cd weather-site
python3 -m http.server 8000
```
Open http://localhost:8000 and click "Detect my location".

## Test permissions
- Allow: coordinates, place name and forecast appear.
- Block: a message appears and the button stops re-asking; use manual search. To retry, reset the site permission (lock icon in address bar) and reload.
- Manual: try `Lahore` and `33.6, 73.0`.

## Deploy on GitHub Pages
1. On github.com click New repository, name it e.g. `weather-site`, set Public, Create.
2. Click "uploading an existing file", drag in `index.html`, `css/`, `js/`, `README.md` (keep the folders), then Commit changes.
3. Go to Settings > Pages. Under Build and deployment choose Source: Deploy from a branch, Branch: `main`, folder `/ (root)`, Save.
4. After about a minute the site is at `https://YOUR-USERNAME.github.io/weather-site/` (HTTPS by default). All paths are relative, so the project URL works.

## Test on a phone
Open the HTTPS URL on the phone, tap Detect, allow location. Make sure device location services are on. For better accuracy, test outdoors.

## Limitations
- Accuracy depends on device, browser and signals; indoors it may be coarse.
- Shows today only (remaining hours). Free APIs have fair-use limits.
- Reverse geocoding may return a broad area name or fail; weather still loads.
