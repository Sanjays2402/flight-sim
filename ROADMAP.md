# Flight Sim — ROADMAP

Single-file Three.js flight sim shipping to https://sanjays2402.github.io/flight-sim/.

## Style rules (do not violate)
- Single `index.html` only. No build step, no bundler, no framework.
- Three.js via CDN import map already in the file.
- Keep everything self-contained. No new files except `assets/*` (sounds, textures) if absolutely needed.
- One feature per ship. Small, visible, playable improvement.
- Plain English commit messages: `feat(flight): <thing>`, `fix(flight): <thing>`, `polish(flight): <thing>`.
- No giant rewrites. Touch the minimum to land the feature.

## DONE
- [x] Basic takeoff + landing
- [x] Throttle-scaled engine sound
- [x] Bigger world: mountains, multiple airports, volumetric clouds
- [x] HUD redesign — proper attitude indicator with bank markers, compass strip, vertical-speed needle
- [x] Stall warning + buffet — visible warning, audio beep, slight screen shake near stall AoA.
- [x] Wingtip vortex trails when pulling Gs / near stall — short tapered ribbons.
- [x] Touch-and-go scoring — each successful landing gives points based on sink rate + centerline + speed at touchdown.
- [x] Free-flight mission picker — start menu with: Free Flight, Touch & Go Challenge, Airport Hop.
- [x] Airport hop mission — fly to the next airport in a sequence, finish timer.
- [x] Procedural cities near airports — boxy buildings for visual interest on approach.
- [x] Time of day cycle — sun moves, sky color, lights on runways at night.
- [x] Weather: wind + crosswind on approach — variable wind affects rudder.
- [x] Smoke / contrails behind plane at high alt or when damaged.
- [x] External chase cam + cockpit cam toggle (C key) — cycles chase/cockpit/flyby/orbit, HUD pill shows active mode, cockpit view hides own airframe.
- [x] Replay last 30s at the end of each landing — rolling 30s buffer of plane pose plays back after touchdown/crash, banner shows REPLAY, click or press R to skip.
- [x] Mini-map in HUD corner — top-down with airports, plane, heading line.
- [x] Damage model — over-G or hard-landing gives damage %, affects handling.
- [x] Engine-out glide — fuel burns with throttle, X toggles engine kill, prop windmills on deadstick approaches.
- [x] Refuel on ground at airport — taxi onto the apron, throttle to idle, fuel ticks back up (~30s for a full tank).
- [x] AI traffic — one other plane doing circuits at the home airport.
- [x] Mobile touch controls — virtual stick on left, throttle slider on right.
- [x] Settings panel — sensitivity, FOV, audio volume (persisted to localStorage, opens via ⚙ or `,`).

## NEXT — pick the top item each loop
Ranked by impact-per-LOC. Top of the list wins next ship.

1. **Liveries / paint picker** — 3–5 color schemes for the plane.
2. **Liveries / paint picker** — 3–5 color schemes for the plane.

## How the ship loop works
Every 5 min during awake hours, an isolated agent runs:
1. Reads this ROADMAP.
2. Picks the top unchecked item under NEXT.
3. Edits `index.html` to land that feature (and only that).
4. Tests by opening with a headless check (HTML parses, no console errors in static analysis).
5. Commits + pushes to `main`. GitHub Pages auto-deploys.
6. Marks the item `[x]` and moves it to DONE in this file (same commit or follow-up).
7. Reports a one-line summary back, then exits.

If everything in NEXT is done, the agent appends 5 fresh ideas to the bottom of NEXT (impact-ranked) before picking one.
