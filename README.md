# WJC & Co. Orrery Chronometer

An astronomically accurate orrery for all nine planets (Mercury-Pluto), styled as
an antique brass/steel pocket watch. Runs entirely client-side in a single HTML
file -- no build step, no server.

**Live app:** [dhammadude.github.io/orrery-chronometer/orrery.html](https://dhammadude.github.io/orrery-chronometer/orrery.html)

## Features

- Real orbital mechanics -- VSOP87 (truncated to dominant terms) for Mercury
  through Neptune, Meeus's full ELP2000/82 lunar theory for the Moon, and
  Standish/JPL approximate Keplerian elements for Pluto -- with an adjustable
  simulation date and playback speed.
- Complications mounted on an integrated shield plate: Moon Phase (with a
  real, magnitude-scaled star plot of the current zodiac constellation and a
  Twin-Pip sun-position ring), Day-Date, and Metonic Cycle (19-year
  lunar/solar calendar sync).
- Zoomed views of the Jupiter and Saturn systems, with the Galilean moons and
  Saturn's four largest moons, real ring-plane geometry, and a ring
  plane-crossing gauge.
- An outer analog clock ring (hour/minute/second hands) tracking real local
  time, and a geocentric Sky View from any location.
- Solar and lunar eclipse prediction, with quick-jump buttons to the next new
  moon, full moon, solar eclipse, lunar eclipse, planetary retrograde window,
  Galilean moon conjunction, or Saturn ring-plane crossing.
- A discreet compass indicator using the device's own orientation sensor.
- Brass/steel theme toggle, compact (dial-only) view, and JSON export/import
  for snapshot or date-range data analysis.
- Installable as a PWA (offline-capable via a service worker) on desktop and
  mobile.

## Running locally

Just open `orrery.html` in a browser -- everything is self-contained. Serving
it over `http(s)` (rather than `file://`) is required for the service worker,
PWA install prompt, and device sensors (like the compass) to work, e.g.:

```
python3 -m http.server 8000
# then visit http://localhost:8000/orrery.html
```

## Repository layout

- `orrery.html` -- the entire app (all HTML/CSS/JS in one file).
- `manifest.json`, `sw.js`, `icons/` -- PWA support.

## Accuracy notes

Mercury-Neptune use a truncated VSOP87A series (real planet-on-planet
perturbation, not a simple two-body ellipse); the Moon uses Meeus's full
ELP2000/82 term tables. Pluto still uses the standard low-precision Keplerian
approximation (valid for roughly 1800-2050), the same tier the whole app used
before the VSOP87/ELP82 upgrade. Eclipse prediction uses mean lunar node
regression and angular season thresholds, so it flags *likely* eclipse
windows rather than computing exact saros-level circumstances.
