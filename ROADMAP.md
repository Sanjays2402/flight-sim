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
- [x] Liveries / paint picker — 5 color schemes (Classic, Navy, Forest, Sunset, Stealth) in settings panel, persisted to localStorage.
- [x] Ring-chase challenge mode — fly through a chain of 11 glowing rings against the clock, active ring pulses green, best time saved to localStorage.
- [x] Autopilot altitude + heading hold — press `H` to lock current altitude and heading (A is roll, so H = hold), HUD shows AP ON with locked alt/hdg, any stick input disengages, auto-off on ground or crash.
- [x] Persistent pilot stats screen — total flights, landings, crashes, best landing score, average score, longest flight, total air time. Opens from main menu via 📊 PILOT STATS button, stored in localStorage, reset with confirm.
- [x] Photo mode — press `P` to pause sim, free-orbit camera (drag + wheel), hide HUD, one-tap PNG download (`S` or SAVE button).
- [x] Gear and flaps sound effects + animated flaps — clunk on gear up/down, whoosh on flaps, flap surfaces visibly deflect on the wing.
- [x] Cockpit instrument panel — airspeed, attitude, and altimeter gauges drawn on small canvases at the bottom-center; only shown in cockpit cam (C key) so the cockpit view actually feels like sitting behind a panel.
- [x] Birds — small flocks of birds drift around low-altitude near airports, gentle flap animation, harmless but adds life to the scene.
- [x] Rain weather toggle — settings option for rain, adds tilted streaks across the screen, dims the sky toward overcast gray, persisted to localStorage. Hidden in photo mode so saved PNGs stay clean.

## NEXT — pick the top item each loop
Ranked by impact-per-LOC. Top of the list wins next ship.

- [ ] Landing gear stress indicator — HUD light flashes amber when sink rate is high enough to risk damage on touchdown, red when guaranteed damage, gives pilots a flare cue.
- [ ] Achievement popups — quick toast in the corner when player hits milestones (first landing, 10 landings, perfect landing score, ring chase under 60s, etc.), stored in localStorage so each only fires once.

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
