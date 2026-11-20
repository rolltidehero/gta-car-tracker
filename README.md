# GTA Car Tracker

GTA VI car values by buyer (Moses, Pay 'n' Spray and Randy) and tracker level, plus a location card for every car on Randy's Wish List. Live page: https://rolltidehero.github.io/gta-car-tracker/

Sister apps: the [Glitch Tracker](https://rolltidehero.github.io/gta-glitch-tracker/) for physics reports and the [Money Tracker](https://rolltidehero.github.io/gta-money-tracker/) for money reports and earning routes.

Car values come from published scan cards and guides, mainly IGN's vehicle table. They are not measurements, nothing was checked in the game for this tracker, and the page shows where guides disagree.

## What is in here

| File | What it is |
| --- | --- |
| `tracker-data.json` | The only file you edit by hand. Cars, buyers, notes, Wish List location cards and sources. |
| `data.js` | Generated from `tracker-data.json`. Do not edit. |
| `index.html`, `app.js`, `style.css`, `base.css` | The page itself. No build step, no dependencies. |
| `exports/` | Generated CSV copy of the car value list. |
| `update-tracker.js` | The single update script, shared by all three repos. It reads `meta.repo` in `tracker-data.json` to identify its app. |
| `.github/workflows/refresh.yml` | Runs the script every four hours on GitHub's servers. |

## How to update

1. Edit `tracker-data.json`.
2. Run `node update-tracker.js` (Node.js 18 or newer). Use `--help` for every option, `--refresh-cars` to pull the newest IGN values, `--dry-run` to test without writing.

The script shows each of its 13 steps (steps that belong to the Glitch Tracker are skipped here), validates the data, rebuilds `data.js` and the CSV, runs self-tests, commits and pushes.

## Automatic refresh

The workflow runs `node update-tracker.js --auto` every four hours at minute 43 UTC. It refreshes car values from IGN, stamps the date, rebuilds, commits and pushes only when something changed, then asks GitHub Pages to rebuild. Disputed values and Wish List location updates still need editorial review.

## Wish List location cards

Every car with `"wishList": true` carries a `"wish"` object with `status` (an evidence tier: Guides agree, Reported sighting, Traffic search or No fixed spot), `list`, `spots`, `need`, `how`, `tracker`, `caveat` and `sources`. Nothing was checked in the game, so a spot is never described as confirmed.

## RSS alerts

Select **Get RSS alerts!** or paste the [feed URL](https://rolltidehero.github.io/gta-car-tracker/feed.xml) into a feed reader. The update script generates `feed.xml` and keeps the 25 most recent items. Car values, Wish List cards, and other tracker content changes generate alerts; date-only checks do not.

## Footer version

The footer shows the latest commit hash, commit count and commit time, read live from the GitHub API.
