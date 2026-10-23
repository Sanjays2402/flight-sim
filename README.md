# Browser Flight Simulator ✈️

A procedural browser flight simulator. Vanilla JS + [Three.js](https://threejs.org/) via ES module import-map. **Zero npm. Zero build. Single `index.html` (~50 KB).**

Features a 30 km × 30 km procedural heightmap world with grass plains, forested hills, gray rock and snow-capped mountains, a distant mountain ring, a lake and ocean coastline, drifting volumetric-feel clouds at multiple altitudes, sparse instanced trees and rocks, and three landable airfields scattered across the terrain.

Open `index.html` in any modern browser (or visit the live page) and fly.

## Live

→ **<https://sanjays2402.github.io/flight-sim/>**

## Controls

| Action | Key |
|---|---|
| Throttle up / down | `W` / `S` |
| Pitch (nose up / down) | `I` / `K` |
| Roll (ailerons) | `A` / `D` |
| Yaw (rudder) | `Q` / `E` |
| Gear up / down | `G` |
| Flaps cycle (0 / 20° / 40°) | `F` |
| Brakes (on ground) | `B` |
| Camera cycle (chase / cockpit / fly-by / orbit) | `C` |
| Reset to runway | `R` |
| Dismiss intro | Click or `Space` |
| Invert pitch axis | Settings (`,` key) → INVERT PITCH |
| Invert roll axis | Settings (`,` key) → INVERT ROLL |

## How to fly

### Takeoff
1. Throttle to ~80–100% (`W`).
2. Hold the brakes off, watch speed climb.
3. At **~140 km/h (Vr)**, pull back gently with `I`.
4. Once climbing, retract gear (`G`).
5. Hold ~10° nose-up for a positive climb.

### Pattern & approach
1. Climb to ~400 m, turn crosswind, downwind, base, final.
2. On final: gear down (`G`), flaps to 20° then 40° (`F` cycles).
3. Aim for the **PAPI** at the bottom of the screen:
   * 4 red = way too low
   * 2 red / 2 white = on the 3° glideslope ✅
   * 4 white = too high
4. Cross the threshold at ~120 km/h, flare a touch, idle the throttle.

### Landing verdicts
* **GREASED IT** — sink rate under 2.5 m/s, on the runway, gear down
* **GOOD LANDING** — soft sink, on the runway, gear down
* **HARD LANDING** — too steep, banked, or off-axis but survivable
* **CRASHED** — gear up, off-runway, or hammer-of-thor sink rate

## Physics

* Lift = ½ρv² · S · Cl with linear Cl(α) up to ~16° AoA, then post-stall taper
* Drag = ½ρv² · S · (Cd₀ + k·Cl² + flap drag + gear drag)
* Thrust scales linearly with throttle; gravity always pulling
* Stall warning when AoA ≥ ~14° in the air
* Positive longitudinal stability: airframe weather-vanes toward velocity vector

## Settings

Open Settings with `,` (comma) to tweak sensitivity, FOV, weather, liveries, and control preferences. The **INVERT PITCH** / **INVERT ROLL** toggles flip the pitch and roll axes (keyboard + virtual stick) for players who expect the opposite stick feel — autopilot and trim are unaffected. All settings persist in the browser via localStorage.

## HUD

Top-left: airspeed, altitude, heading, vertical speed, throttle %, flap setting, gear status, AoA, stall warning.

Top-right: artificial horizon (attitude indicator) with pitch ladder and bank angle.

Bottom-center: PAPI glideslope lights.

## Tech

* [Three.js 0.160](https://threejs.org/) loaded via ES module import-map from UNPKG
* All geometry, sky shader, and clouds are procedural — no images, no assets, no fetch
* Custom shader for the sky gradient dome
* Custom 2D canvas for the attitude indicator

## Local dev

```sh
python3 -m http.server 8000
open http://localhost:8000
```

No bundler, no node_modules.

## License

MIT

## Terms & Disclaimer

By using this project you agree to the following.

- **No warranty.** This software is provided "as is", without warranty of any kind, express or implied, including merchantability, fitness for a particular purpose, and non-infringement.
- **No liability.** To the maximum extent permitted by law, the author and contributors are not liable for any claim, loss, or damage (direct, indirect, incidental, or consequential, including lost data or profits) arising from its use.
- **Your responsibility.** You use it at your own risk and are responsible for complying with the laws that apply to you.
- **Game.** Provided for entertainment. Take breaks; it is not designed for people with photosensitive epilepsy, and flashing effects may occur.
- **Entertainment only.** This simulator is not flight training and is not approved by any aviation authority (FAA, Transport Canada, or DGCA).
- **Third parties.** Names, logos, APIs, and services of others belong to their owners and are used for identification only; no affiliation or endorsement is implied.
- **Your statutory rights.** Nothing here limits rights that cannot be waived by agreement, including under consumer-protection laws in the USA, Canada (including Quebec), and India (Consumer Protection Act, 2019).
- **License.** Use, copying, and distribution are governed by the [LICENSE](LICENSE) file; if anything here conflicts with it, the license controls.

## Content, Assets & Fair Use

- **Original work.** Unless noted otherwise (including below), the code, text, design, and images in this repository were created by the author.
- **Libraries, fonts, and icons.** Third-party libraries, fonts (for example Google Fonts), and icon sets belong to their creators and are used under their own licenses; see the dependency manifests and each source for terms.
- **Logos, brands, and screenshots.** Third-party names, logos, and screenshots appear only to identify or describe their products (nominative use). They remain the property of their owners and do not imply affiliation or endorsement.
- **Ideas and inspiration.** Where this project is inspired by another product, game, or idea, it is an independent implementation. It borrows only general ideas, mechanics, or styles, which are not anyone's exclusive property, and is meant to contain no third-party code or artwork used without permission.
- **Fair use and fair dealing.** Any third-party material is used in limited ways for purposes such as education, research, review, commentary, or identification, relying on fair use in the USA (17 U.S.C. § 107), fair dealing in Canada (Copyright Act, ss. 29–29.2), and fair dealing in India (Copyright Act, 1957, s. 52), where they apply.
- **Concerns and takedown requests.** If you own rights in something here and believe it is used improperly, [open an issue](https://github.com/Sanjays2402/flight-sim/issues) or contact the author through their GitHub profile with a link to the material and your claim. It will be reviewed promptly and credited, changed, or removed as appropriate. You may also use GitHub's DMCA process.
- **Contributions.** By contributing, you confirm you have the right to submit your contribution and agree it is licensed under this repository's license.
- **Website.** The project site has its own [Terms](https://sanjays2402.github.io/flight-sim/terms.html) and [Fair Use](https://sanjays2402.github.io/flight-sim/fair-use.html) pages.
