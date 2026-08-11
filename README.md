# Perseid Radiant Tracker

A small field tool for the 2026 Perseid meteor shower: enter your location and get the best viewing window, the direction to look, and a live compass to point you there.

**Live tool:** `https://eceozen.github.io/perseid-tracker`

## What it does

- Enter a city/town (with autocomplete) or use your device's GPS
- Pick the observing night (defaults to the 2026 peak, Aug 12–13)
- See:
  - the peak viewing time, converted to your local time zone
  - the compass direction and altitude to look toward
  - a 0–100 observing score combining radiant altitude, cloud cover, moon illumination, and light pollution
  - a polar sky-dial showing the radiant's path through the night, with the peak moment marked
- Open the live compass and get real-time "turn left / turn right" guidance until you're pointed at the peak
- Available in **Turkish, English, French, and German**
- Share a link that reproduces your exact location, date, and language via URL parameters

## How it works

Everything runs client-side, in the browser — no backend, no build step.

- **Radiant position**: computed with a Local Sidereal Time / Alt-Az transform written in vanilla JS, cross-checked against [Astropy](https://www.astropy.org/)'s `AltAz` frame in the companion notebooks (see below) to confirm the math agrees
- **Cloud cover**: pulled live from the [Open-Meteo](https://open-meteo.com) API (no key required)
- **Location search**: [OpenStreetMap Nominatim](https://nominatim.openstreetmap.org) for geocoding city/town names, plus the browser's native Geolocation API for GPS
- **Compass**: `DeviceOrientationEvent` (with the iOS permission prompt handled) for live heading

## Notebooks

The `notebooks/` folder has the Python/Astropy work behind the tool — useful if you want to see the astronomy explained step by step, or verify the JS math independently:

- **`perseid_astropy_prototype_en.ipynb`** — an from-scratch introduction to Astropy (units, `Time`, `EarthLocation`, `SkyCoord`, `AltAz`), building up to the same radiant-altitude and best-viewing-window calculation the live tool uses, plus `astroplan`'s `plot_sky`/`plot_altitude` visualizations
- **`perseid_anatomy_en.ipynb`** — the bigger picture: why the shower happens in August (orbital diagram of Earth crossing Comet Swift-Tuttle's debris trail), why it peaks on the 12th–13th specifically (activity/ZHR curve, including real observational data from the [Global Meteor Network](https://globalmeteornetwork.org/flux/)), and a short animation of why a radiant looks like a single point

GitHub renders `.ipynb` files (including the embedded plots) directly in the browser — no need to run anything to view them.

## Deploying your own copy

1. Push this repo to GitHub
2. Repo Settings → Pages → set source to the `main` branch, root folder
3. Wait a minute for the first deploy, then visit `https://<username>.github.io/<repo-name>/`

## Credits & data sources

- Radiant coordinates and shower timing: [IMO Meteor Shower Calendar](https://www.imo.net/resources/calendar/)
- Cloud forecasts: [Open-Meteo](https://open-meteo.com), CC BY 4.0
- Geocoding: [OpenStreetMap Nominatim](https://nominatim.openstreetmap.org), © OpenStreetMap contributors, ODbL
- Real activity data in the notebooks: [Global Meteor Network](https://globalmeteornetwork.org/flux/), CC BY 4.0 — see the notebook for full citation

## License

Code in this repo is free to reuse and adapt. Third-party data (Open-Meteo, OpenStreetMap, GMN) carries its own license — see the links above.
