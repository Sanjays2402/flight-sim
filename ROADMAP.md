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
- [x] Landing gear stress indicator — HUD warning that flashes amber when sink rate is high enough to risk damage on touchdown, red when guaranteed damage, gives pilots a flare cue.
- [x] Achievement popups — quick toast in the corner when player hits milestones (first flight, first landing, 10 landings, perfect landing score 300+, ring chase under 60s, climbed above 1000m), stored in localStorage so each only fires once.
- [x] ATC chatter ticker — fake radio strip at top of HUD with rotating canned ATC lines tied to the current event ("Cleared to land 27", "Traffic, 2 o'clock", "Winds 240 at 12"). Pure flavor, big immersion bump for ~30 LOC.
- [x] Pause menu (Esc) — overlay with Resume / Restart Mission / Back to Menu, freezes sim + audio, also pauses the autopilot tick so nothing drifts. Currently there's no graceful way to bail mid-flight.
- [x] Runway taxi guidance arrows — when on the ground near an airport, draw a faint chevron line on the taxiway pointing to the active runway threshold so new players can find where to take off from.
- [x] Hard-deck altitude warning ("PULL UP") — when descending fast toward terrain below 150m AGL outside an airport zone, flash red "TERRAIN — PULL UP" with a sharp beep. Saves a lot of dumb crashes into mountains.
- [x] Spotter binoculars (B key) — hold B in external cam to zoom FOV way in with a subtle vignette, so you can actually look at distant airports, the AI plane, or rings before flying to them. Release to snap back.
- [x] Aerobatic ribbon trail (Y key) — toggleable colored smoke trail off the tail in the current livery accent color. Off by default, hidden in photo/replay/pause and on the ground. (Bound to Y instead of T because T already cycles time-of-day.)
- [x] Loop / roll detector — quietly track pitch and roll over time; when the plane completes a full 360° loop or aileron roll, fire an achievement-style toast ("LOOP!" / "AILERON ROLL!") and bump pilot stats. Tiny LOC, huge "wait, it noticed!" payoff.
- [x] Airshow smoke on/off button on the HUD — small `~` toggle (and tap target on mobile) that turns on a permanent colored smoke trail in the player's livery accent color. Pairs with the ribbon trail or stands alone.
- [x] Hot-air balloons drifting over the world — 4 lazy procedural balloons floating between airports, gentle bob, harmless. Pure scenery, makes the world feel less empty between airports.
- [x] Quick-restart hotkey (R outside replay) — when on the ground / crashed / paused, R restarts the current mission immediately (resetPlane + startMission, closes the pause overlay), and during a replay R also skips it and restarts. Mid-flight (healthy, in the air) keeps the legacy reset-to-runway so a stray R doesn't nuke an active sortie.
- [x] Wind sock at each airport — a small orange wind sock on a pole near the runway that tilts with the current wind direction and inflates with wind speed. Cheap to draw, makes pre-landing reads way easier than squinting at the HUD wind readout.
- [x] Crash report card — after a crash, a small panel pops up bottom-center with peak G, sink rate at impact, speed, AoA, the failure reason, and a one-line verdict ("STALLED ON FINAL", "GEAR-UP LANDING", "OVERSPEED IMPACT", etc.). Hidden in photo mode, click to dismiss, R restarts. Every wreck is now a lesson instead of just a replay.

## NEXT — pick the top item each loop
Ranked by impact-per-LOC. Top of the list wins next ship.

- [ ] Heading bug on the compass strip — press `[` and `]` to nudge a magenta tick around the compass; autopilot heading hold uses the bug instead of current heading. Real-pilot UX trick that takes ~20 LOC.
- [ ] Engine RPM gauge in the cockpit panel — fourth small canvas next to airspeed/attitude/altimeter showing prop RPM scaled from throttle (drops with engine-out, climbs with throttle). Finishes the cockpit panel so it doesn't look lopsided.
- [ ] Sunrise / sunset toast — when the time-of-day cycle crosses sunrise or sunset, fire a quick golden-tinted toast ("🌅 Sunrise" / "🌇 Sunset") so the player actually notices the world changing instead of missing it mid-turn.


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
