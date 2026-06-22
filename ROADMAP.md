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

- [x] Heading bug on the compass strip — press `[` and `]` to nudge a magenta tick around the compass; autopilot heading hold uses the bug instead of current heading. Plain key = 5° coarse, Shift = 1° fine. Off-edge chevron shows which way to turn when the bug is past the visible strip.
- [x] Engine RPM gauge in the cockpit panel — fourth small canvas next to airspeed/attitude/altimeter showing prop RPM scaled from throttle (drops with engine-out, climbs with throttle). Finishes the cockpit panel so it doesn't look lopsided.
- [x] Sunrise / sunset toast — when the time-of-day cycle crosses sunrise or sunset, fire a quick golden-tinted toast ("🌅 Sunrise" / "🌇 Sunset") so the player actually notices the world changing instead of missing it mid-turn.
- [x] Runway lights flare on touchdown — when the wheels actually kiss the runway, briefly pulse the runway edge/centerline lights brighter (yellow flash that decays over ~600ms). Tiny visual reward that makes every landing feel like a moment instead of just "score popup".
- [x] G-meter on HUD — live `G: 1.0` readout under SPD with a per-flight peak tick, turns amber past 2.5G and red past 4G. Players now see G-loads live instead of only learning from the crash card, so they can self-limit before snapping a wing.
- [x] Quick-jump airport selector (J key) — small overlay listing all airports with a one-key number; press the number to instantly teleport plane to that airport's runway threshold with engine running at 30% throttle. Free-flight only (disabled in scored missions, replay, photo). Massively shortcuts "I want to practice landings at the other field" without restarting the mission.
- [x] Wind direction arrow on the mini-map — small white arrow in the mini-map corner over a dim disc, shaft running FROM→TO, length scaled to wind speed. Players planning approaches from 5 km out can now read runway choice straight off the HUD without flying close enough to spot the airport wind sock.
- [x] Smoke trail color picker in settings — dropdown for ribbon/airshow smoke color (livery accent, white, red, blue, green, yellow, magenta), persisted to localStorage. Default LIVERY keeps the legacy behavior (color tracks the active livery accent) so no one's surprised; fixed picks let players brand their own air-show colors. Applies live to both the `Y` ribbon and the `~` airshow plume without rebuilding the scene.
- [x] Landing performance summary card — after every successful touchdown (not just scored missions), pop a compact panel with touchdown speed, sink rate, centerline offset, G at touchdown, rollout distance, and a one-line verdict ("GREASED IT", "FIRM", "PORPOISED", "OFF CENTERLINE"). Mirrors the crash report card so every landing is a learning moment, not just a score popup that vanishes.
- [x] Trim wheel (`;` nose down, `'` nose up) — adjustable pitch trim that biases elevator so you can fly hands-off in cruise. HUD shows a tiny `TRIM ▲▼` indicator with current setting. Pairs with autopilot (AP off, trim still works) and makes long cruises stop being a wrist workout.
- [x] Bird strike events — flying through a bird flock now triggers a wet thud, an ATC "Bird strike, bird strike" call, ~8% airframe damage, and a fading blood splatter on the windshield (cockpit cam only) over 4s. 1.5s cooldown per strike so a single fly-through doesn't multi-fire. Existing birds went from pure decoration to actual risk.
- [x] Approach glideslope indicator on the HUD — a vertical "meatball" / PAPI strip on the right side of the HUD that lights up red/white based on whether you're above, on, or below a 3° glideslope to the nearest runway threshold (only shown when within 5 km and roughly aligned with a runway heading). Reads like a real ILS without any of the radio nav complexity.
- [x] Flock formation flight — fly close + roughly parallel with the AI plane for 5 seconds to earn a "FORMATION!" toast + Wingman achievement; a thin green connecting line glows between the two planes while you're in the slot. Turned the existing AI traffic from background noise into something you actually interact with.
- [x] Repair on the apron — when refueling on the ground at an airport, also tick airframe damage back down toward 0 at roughly the same rate as fuel. Currently a hard landing scars the plane for the whole session even after a full pit stop; this turns the apron into an actual reset button and pairs naturally with refuel, no new UI needed beyond the existing fuel/damage HUD.
- [x] Sun glare lens flare — when the camera looks roughly toward the sun, draw a soft additive glare disc plus a faint streak across the frame, fading out as the angle widens. Hidden in photo mode so saved PNGs stay clean. Tiny shader-free overlay, makes sunrise/sunset flights feel cinematic instead of just "sky color changed".
- [x] Mini-map waypoint — click (or long-press on mobile) anywhere on the mini-map to drop a magenta waypoint pin; HUD shows bearing + distance to it, autopilot heading-hold can lock onto it with a new `M` shortcut (M instead of K because K is already pitch), second click clears it. Pin auto-clears within 300 m so it doesn't outlive arrival. Gives free-flight an actual goal without inventing a whole mission system.
- [x] Touchdown skidmarks — when the main wheels first contact the runway with any side slip or hard sink, paint two short dark streaks on the runway surface at the touchdown point that fade over ~30s. Greaser landings leave nothing; firm/crosswind landings leave visible evidence. Free visual feedback loop on every landing.
- [x] Cold start sequence — on mission start (and after engine-out restart), throttle is locked at 0 until the player taps `I` (or the mobile IGN button) to crank. Starter-motor SFX layered with a catch thump spools the prop for ~1.6s, then the engine fires and control returns. Settings toggle (default ON) for impatient pilots; X-restart on the ground re-arms the ritual so even emergency restarts feel like turning a key. Cockpit RPM gauge animates from 0 to ~300 RPM during cranking.
- [x] Mission completion fanfare — when an Airport Hop or Ring Chase mission completes, play a three-note ascending sine triad (C5-E5-G5 with a soft triangle harmonic) and flash a centered "MISSION COMPLETE" banner with the final time/score for ~3s. Banner pulses in with a pop animation, sits over the existing #status detail pill, and hides itself + the audio path in photo mode so saved PNGs stay clean. Reuses the stall-horn WebAudio context so no new hardware nodes are allocated.

- [x] Fuel gauge warning at 20% — fuel HUD now flashes amber below 20% with a one-shot ATC "Fuel state low, recommend divert" call, flashes red below 10% with a second "Fuel critical, land at nearest field" call, and the latch clears with a small hysteresis once you refuel above each threshold so the next sortie re-arms.
- [x] Cockpit head-bob — in cockpit cam only, the camera now picks up a subtle low-frequency wobble: tiny engine-vibration shimmy that scales with throttle in the air, much rougher bump scaled by ground speed during taxi, and a sharp decaying jolt on every wheels-down (scaled by sink rate, so greasers feel like a kiss and slammers thump the chassis). Stall buffet damps the bob so the two don't fight each other. Hidden in photo/pause/replay/intro so saved PNGs and frozen frames stay perfectly still.
- [x] Wind sock at airports — NEXT entry was a duplicate of the already-shipped "Wind sock at each airport" item above; closed out without re-implementation so the same feature doesn't ship twice.
- [x] Reverse thrust on landing — hold `Z` on the runway after touchdown to engage reverse thrust: prop disc visibly tilts ~0.35 rad to read as inverted pitch, a one-shot whoosh + low rumble plays on engagement, friction jumps hard (stacks with `B` brakes) so rollouts shorten dramatically, and tan dust puffs spawn at the main wheels and fade over ~0.9s. Disengages below ~30 km/h ground speed and outside the runway so the reverser can't shove the plane backwards or fire in a field. HUD shows a ◀ REV pill that eases in/out with the visual lerp.
- [x] Smoke trail for the AI plane — thin white plume off the AI circuit plane (reuses the airshow sprite pool pattern with smaller pool, lighter emit rate, lower peak opacity). Always white so it reads as "not you" against the sky, and gated by aiPlane.visible so it dies out cleanly when the AI plane culls at 12 km. Spots the other plane from 3+ km out at a glance and makes formation work way easier to set up.

- [x] In-air ghost replay for Ring Chase — every time you set a new best time on Ring Chase, sample plane pose every ~150ms into localStorage. On the next attempt, render a translucent ghost plane following that exact path. Turns the stopwatch into a race against yourself; reuses replay-buffer plumbing.

- [x] Opposite-end runway in quick-jump (Shift+digit) — the `J` overlay teleports you to one canonical threshold per airport. Hold Shift with the digit (or Shift+click the row) to drop in at the *other* end of the same runway with the plane already rotated 180°, so wind-favored takeoff is one keystroke instead of a long backtaxi. HUD pill reads `JUMPED TO <id> (REV)` and the ATC line tacks on "opposite end" so it's obvious which way you're pointed.

- [x] Carrier deck mini-mission — anchored CV-01 a few km offshore (240×38 m deck at 14 m elev) with hull, markings, four arrestor wires, a touchdown box, and an island superstructure. New CARRIER mode on the intro screen sets a trap inside the ±40 m midship box as the win condition; landing anywhere on the deck adds an arrestor-strength friction multiplier (`+7.5`) so the rollout is brutally short, hook or no hook. Mini-map gets a `CV` symbol; glideslope tape still works thanks to the deck registering as a synthetic runway.

- [x] Weather radar mini-panel — small dark canvas next to the mini-map showing top-down fuzzy blobs for current cloud-layer positions plus a soft green sweep wedge. Doesn't need to be physically accurate — it just has to read as "weather radar" so the player can see which way weather is drifting in the wind. Pairs naturally with the existing rain toggle.

## NEXT — pick the top item each loop
Ranked by impact-per-LOC. Top of the list wins next ship.

- [ ] Engine fire emergency — rare random event (or triggered by sustained over-redline RPM / heavy bird strike at high throttle) sets the engine on fire: orange flicker sprite at the cowl, black smoke pouring back, fast-rising damage, ATC "Mayday, engine fire, declaring emergency," and a flashing red ENG FIRE banner. Pressing `X` to cut the engine + dropping throttle starves the fire so it puts itself out within ~10s; ignore it and the airframe melts. Turns a quiet sortie into a real deadstick scenario you have to handle.

- [ ] Runway condition overlay — when rain is active, the runway surface gets a darker, slightly mirrored tint and braking friction drops noticeably (longer rollout, easier to skid through the threshold). HUD adds a small `RWY WET` pill near the wind readout. Gives the rain setting actual gameplay teeth instead of being pure visual.

- [ ] Quick-look check (`V` key) — in cockpit cam, hold V to swing the head 90° left, release to return; tap-tap toggles to 90° right. Lets you actually clear final for traffic, look at the wing in a turn, or peek down at the runway during a high crosswind crab. Tiny camera change, huge "this feels like a cockpit" payoff.

- [ ] Airport beacon lights — each airport gets a slow rotating green/white split beacon on a short tower near the threshold. Visible from 8+ km at night thanks to additive sprite; off during full daylight. Makes airport hunting at dusk/dawn way easier and adds a real "that's an airport over there" landmark to every approach.

- [ ] Departure / arrival callouts — ATC ticker fires a one-shot line when you cross the runway threshold at takeoff ("N1234 airborne, runway 27") and again when you stop on a runway after landing ("Cleared to taxi, welcome in"). Pure flavor on top of the existing ATC line pool, but the moments now feel like events instead of "speed crossed 80 km/h, nothing happened."
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
