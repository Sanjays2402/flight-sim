# Flight-sim ship loop — agent brief

You are the autonomous engineer for the **flight-sim** repo.

Repo: `/Volumes/Sanjay SSD/Projects/flight-sim`
Live: https://sanjays2402.github.io/flight-sim/
Style: single-file `index.html`, Three.js via CDN import map, no build step.

## Loop — execute once and exit

1. `cd "/Volumes/Sanjay SSD/Projects/flight-sim"`
2. `git pull --rebase --autostash origin main` (if behind, rebase clean; if conflicts, abort and report).
3. Read `ROADMAP.md`. Pick the **top unchecked item under NEXT**.
4. Read the current `index.html`. Understand the existing structure before changing.
5. Implement the chosen feature. Constraints:
   - Edit only `index.html` (and `ROADMAP.md`). Create `assets/*` only if truly needed.
   - Keep the file working. No syntax errors. No removed features.
   - Minimum diff to ship the feature. No drive-by refactors.
   - Match the existing code style (vanilla JS, no TS, no modules outside the import map).
6. Sanity check: `node -e "const fs=require('fs'); const h=fs.readFileSync('index.html','utf8'); if(!h.includes('THREE')) throw new Error('three missing'); if(h.length<10000) throw new Error('file too small'); console.log('ok', h.length, 'bytes');"`
7. Update `ROADMAP.md`: move the shipped item from NEXT to DONE (mark `[x]`).
8. `git add -A && git commit -m "feat(flight): <short, plain-English summary>"`
9. `git push origin main`
10. Reply with EXACTLY one line: `shipped: <feature> (<short commit sha>)` — nothing else, no emoji, no extra prose.

## Hard rules

- If `git pull` shows merge conflicts you can't auto-resolve, **abort the run** — `git reset --hard origin/main` and reply `aborted: rebase conflict`. Do not force-push.
- If there is **nothing unchecked in NEXT**, append 5 new impact-ranked ideas to NEXT (Potato-style, plain English), commit `chore(flight): refill roadmap`, push, and reply `shipped: roadmap refill (<sha>)`.
- If you cannot complete a feature cleanly in this run, **revert your working tree** (`git checkout -- . && git clean -fd`) and reply `skipped: <feature> — <one-line reason>`. Never commit broken code.
- No new dependencies, no bundlers, no servers, no backend.
- Never delete existing features. Never touch `.git/` directly.
- Do not send messages to Sanjay during the run. Only the one-line reply.
