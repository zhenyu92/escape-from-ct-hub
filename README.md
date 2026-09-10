# 👻 ESCAPE FROM CT HUB

**A Paranormal Commute Advisory.** A straight-faced ghost-hunting instrument that tells you
whether to run for the bus. Every reading on it is real, live Singapore government data.

Fixed to **CT Hub, 2 Kallang Avenue**. Static single file. No server, no build step, no API key.

---

## The verdict

The instrument answers one question — *run for the bus, or don't* — by crossing live bus
arrivals against live rainfall:

| | |
|---|---|
| 🏃 **FLEE** | Water is coming and the bus is close enough to catch. Run. |
| 🕯️ **HOLD YOUR GROUND** | No water at the station, none foretold. Nothing to run for. |
| ☠️ **YOU ARE ALREADY DEAD** | Rain will reach the stop before the bus does. Go back inside. |

## The instruments

Ghost-hunting tropes map onto NEA's sensor network more neatly than they have any right to.

| Reading | What it actually is |
|---|---|
| ❄️ Thermal anomaly | Air-temperature station nearest CT Hub vs. the island-wide mean — a cold spot |
| ☂️ Ectoplasmic precipitation | 5-minute rainfall gauges; how far away the nearest wet one is |
| ≋ Spectral mist density | PM2.5 for the nearest region |
| ☉ Solar suppression | UV index, inverted — nothing walks in daylight |
| ⌁ The Vanishing | Available taxis within 3km, watched over time |
| ◐ Two-hour portent | NEA nowcast for the nearest named area (Kallang, 0.2km) |
| ⊟ The arrivals | Live bus times for the two stops that serve CT Hub |
| ▣ Surveillance | Nearest live roadside camera, degraded |
| ◈ Aggregate EMF | The above, weighted, scaled by nightfall and proximity to Samhain |

## The séance

**The Vanishing needs memory, and a static site has none.** With no server there is no
history, so the count of available taxis only becomes meaningful once the page has watched
it for a while. The instrument therefore refuses to conclude for the first **4 minutes and
3 readings**, and says so. Leave the tab open and it sharpens. The wait is the ritual.

## Seasonality

Halloween-only by design. The aggregate reading is scaled by proximity to 31 October
(15% baseline, ramping through October, 100% on the day) and by a nocturnal coefficient
after 19:00 SGT.

To witness it early: **`?samhain=1&night=1`**, or the ritual override buttons in the footer.

---

## Data sources

All feeds are public, keyless, and send `Access-Control-Allow-Origin: *`, so the page calls
them directly from the browser.

- `api-open.data.gov.sg/v2/real-time/api/` — air-temperature, rainfall
- `api.data.gov.sg/v1/environment/` — pm25, uv-index, 2-hour-weather-forecast
- `api.data.gov.sg/v1/transport/` — taxi-availability, traffic-images
- `arrivelah2.busrouter.sg` — LTA bus arrivals ([busrouter.sg](https://busrouter.sg))

### Notes on the feeds, learned the hard way

- **v2 carries far more stations than v1** — 18 thermometers and 88 rain gauges against
  1 and 4 observed on v1. The cold-spot reading is meaningless without v2, so temperature
  and rainfall prefer v2 and **fall back to v1** automatically.
- **v2 rate-limits.** Roughly 2 in 10 rapid calls return `429`. The page polls once a minute,
  which is comfortably under, and falls back to v1 when it is refused.
- **v2 has no `traffic-images`** — it returns `403`. Cameras stay on v1.
- **The camera feed thins out.** It normally carries ~90 cameras; it has been observed
  serving 8, with the nearest 7.2km from Kallang. The page uses whichever is nearest and
  says how many eyes are open, so it recovers on its own.
- **Thin data is reported, never faked.** With fewer than 3 thermometers reporting, the
  cold spot reads `INDETERMINATE` rather than inventing an anomaly.

## Stops

| Code | Name | Distance |
|---|---|---|
| `07379` | Aperia / Bef Kallang Rd | 131 m |
| `07369` | Aft Kallang Bahru | 147 m |

Serving 13, 61, 67, 107, 133, 141, 145, 175, 961.

---

## Running it

Open `index.html`. That is the whole thing.

To host: push to GitHub and enable **Pages** on the repository root. `index.html` sits at the
top level, so no workflow or build is required.

## Accessibility & layout

Single column below 620px, verified with no horizontal overflow at a 400px viewport.
All animation — flicker, tracking bar, sensor noise — is disabled under
`prefers-reduced-motion`.

---

*The instrument makes no claim as to the existence of the dead. It only reports the instruments.*
