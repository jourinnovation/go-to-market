# Launch, Prove, Scale

**A go-to-market strategy game for student venture teams.**

Teams build a route from their first adopter to a repeatable way of reaching the next market, pitch it to another team playing a buyer, adapt to a random curveball, and leave with a slide-ready summary for their pitch deck.

Built for JOUR 3385 (Media Innovation & Entrepreneurship) at Cal Poly San Luis Obispo.

---

## How it plays

The game runs in five rounds, followed by a peer-review and slide screen. A sidebar route map fills in as teams work, so they can see their whole strategy at a glance.

| Round | Focus | What teams do |
|---|---|---|
| 1 · Choose a starting point | Beachhead | Enter a team name, describe the offer, and name a specific, reachable first adopter. |
| 2 · Set the proof threshold | Pilot evidence | Name one observable result from a pilot that would justify approaching the next adopter. |
| 3 · Build a repeatable path | Scale strategy | Pick a primary growth route and explain where it leads next and why it fits. |
| 4 · Pitch & get a reaction | Buyer role-play | Pair with another team, pitch to a randomly drawn buyer using the built-in 60-second timer, and record the decision and reason. |
| 5 · Adapt your strategy | Curveball | Draw a constraint, huddle for two minutes on the built-in timer, and describe one change that keeps the plan believable. |
| Final · Pitch-deck slide | Review & export | Peer-review the route against four strategy checks, then copy the slide text or print/save it as a PDF. |

### Scale paths (Round 3)

License / white-label, Direct sales, Partnerships, Audience growth, Syndication / distribution, or Other route.

### Buyer cards (Round 4)

Drawn at random, with a redraw option:

- Student newsroom editor
- Potential partner
- Campus decision-maker
- Reader or community member
- Sponsor or advertiser
- Next-market adopter

Each card gives the buyer an in-character question to open with. The buyer answers **Yes**, **Maybe**, or **No**, and the pitching team records the condition or concern behind it.

### Curveballs (Round 5)

Drawn at random, with a redraw option: Customization trap, Slow approval, No launch budget, Proof gap, Trust barrier, Limited capacity, Different buyers, and Platform shift.

### Strategy checks (Final screen)

1. Our first adopter is specific and reachable.
2. Our pilot produces observable proof.
3. Our scale path can repeat with the next market.
4. We adjusted for a real buyer concern or constraint.

Teams check a box only when they can point to the part of their plan that supports it. Unchecked items are the revision targets before the slide goes into a deck.

---

## Running a session

**Time:** roughly 35–50 minutes, depending on how long you give the pitch round and the debrief.

**Suggested pacing**

- Rounds 1–3: 15–20 minutes of team work
- Round 4: about 5 minutes per pairing (60-second pitch, buyer response, swap roles)
- Round 5: 2–3 minutes per team
- Final screen and peer review: 5–10 minutes
- Whole-class debrief: as long as you like

**Setup**

- One device per team, with the game open in a browser.
- Before Round 4, assign team pairings. One team pitches while the other plays the buyer card shown on the pitching team's screen, then they switch.
- Work saves automatically, so a team can close the tab and pick up later on the same computer. If teams will switch computers between class meetings, have them use **Export** at the end of class.
- On shared lab computers, each team should use **New route** so they don't overwrite another team's work, and pick their team's name from the route menu when they return.
- For submission, ask for the exported `.json` file, the printed PDF, or both.

**Debrief prompts**

- Which buyer objections showed up across several teams?
- Did any team get a "No" that changed their beachhead or proof point?
- Which curveballs forced the biggest changes, and which were easy to absorb?
- Where do the audience and the buyer differ in your plan?

---

## Deploying

The game is a single self-contained `index.html` file with no build step, no external libraries, and no network requests.

**GitHub Pages**

1. Add `index.html` and this `README.md` to a repository.
2. In the repository's **Settings → Pages**, set the source to the main branch, root folder.
3. Share the published URL with students.

**Other options:** open the file directly in a browser, or upload it to any static web host or LMS page that allows HTML files.

---

## Saving and data

- **Autosave.** Every answer, card draw, buyer decision, and strategy check saves to the browser's `localStorage` as teams work. Refreshing or closing the tab doesn't lose anything, and the intro screen offers to continue where the team left off.
- **Multiple routes per browser.** The route menu in the header holds any number of saved routes, labeled by team name. **New route** starts a blank one, and **Delete** removes the current one after a confirmation.
- **Export and Import.** **Export** downloads the current route as a `.json` file. **Import** loads that file on any computer as a new route, opening at the round where the team stopped. This is how teams move work between machines, keep a backup, or turn in a submittable file.
- **Slide output.** **Copy slide text** puts a plain-text version on the clipboard, and **Print / save as PDF** prints only the slide card.
- **Privacy.** Saved routes stay in the browser that created them. Nothing is sent to a server, and there are no accounts or logins. Clearing browser data, or using a private/incognito window, erases saved routes, so teams should export anything they need to keep.
- **Timers** are not saved. They reset when a team leaves the round or reloads the page.

---

## Customizing

All game content is defined near the top of the `<script>` block in `index.html`:

| To change… | Edit |
|---|---|
| Scale path options | `scaleOptions` |
| Buyer cards and their opening questions | `buyers` |
| Curveball cards | `curveballs` |
| Round names in the progress bar | `progressNames` |
| Strategy checklist | the `checks` array inside `renderFinal()` |
| Timer lengths and labels | `TIMERS` (keyed by round index: `3` is Round 4, `4` is Round 5; values in seconds) |

Each card is a two-item array of `[title, description]`. Add or remove entries freely; the random draws adapt to the list length.

Colors are CSS variables in `:root` at the top of the `<style>` block, set to Cal Poly green (`--green`, #154734) and gold (`--gold`, #BD8B13), with lighter tints for highlights.

Saved routes are stored under the `localStorage` key `launch-prove-scale:v1`. If you change the game's fields in a way that makes old saves incompatible, change the key so students start fresh. Exported files are checked for `"app": "launch-prove-scale"` before import, and unknown or malformed fields are ignored.

---

## Browser support

Works in current versions of Chrome, Edge, Firefox, and Safari, on desktop and mobile. The layout collapses to a single column on narrow screens, with the route map moving above the round content. **Copy slide text** requires the page to be served over HTTPS (as on GitHub Pages) or opened locally; if the clipboard isn't available, the game prompts teams to use Print / save as PDF instead.
