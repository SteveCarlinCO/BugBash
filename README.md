# BUG BASH! 

*A tower defense game for every poor bastard who sat through sprint planning and thought: "this, but with a lot more violence."*

You are the last pathetic line of defense between a JIRA ticket and production. Bugs literally crawl out of **JIRA-404**, wander across your IDE like it's a goddamn maze, and try to slam the **Merge PR** button. You stop them with linters, `rm -rf`, and microservices. Yes, really. No, I'm not sorry.

![This is how it be](https://github.com/SteveCarlinCO/BugBash/blob/Main/og-image.png?raw=true)

## What the Hell is This

Bug Bash! is a maze tower defense game lazily reskinned as a VS Code IDE having a totally shit day. There is no fixed path—every defender you plop down acts as a wall. The bugs reroute around your maze in real time. If you try to completely seal the route, the game flat-out refuses to place the tower and silently judges your stupid ass.

## How to Run This Shit

1. Open it in a browser.
2. That's it. That's the entire fucking install process.

There is zero build step. There is no `package.json`. There is no backend—it's "serverless" in the sense that there is no fucking server, and somehow even less than that. Your pathetic excuse for a database is `localStorage` dragging around `_v1` suffixes and doing a lot of hopeful, heavy lifting.

## Versioning

`git` is just a fucking rumor here. The changelog is whatever is rattling around in the memory file. The release process is literally "attach the new file and pray to the old gods you didn't make a mistake."

The in-game release branch (`release/v1.0 → prod`, sitting under the Merge PR button) increments every 5 sprints. This means the fake, make-believe project inside the game has better release discipline than this actual piece-of-shit project.

## Production's Sleep Paralysis Demons

**Invaders** (the bugs, obviously — HP and leak damage now on the Story Point poker scale, because even suffering should be estimated):
- **`404`** — Not found. Ever. Even when it's right in front of your face. (3 HP, leaks 5% uptime)
- **`NaN`** — Not a number, not a bug, not a fucking thing. `NaN !== NaN` and neither does this useless trash. (2 HP, 5%)
- **`WARN`** — "Technically" not an error. Technically. (1 HP, 5%, pays a deeply insulting ½ story point)
- **`500`** — The server is fine. Just kidding, the server is on fucking fire. (20 HP, leaks 10%)
- **`HEISENBUG`** — Flies right over your stupid walls. Observing it actually changes its position. Good fucking luck. (3 HP, 5%)
- **`RACE COND`** — Teleports 1–3 cells every few seconds. The docs call it "eventual consistency." The docs are lying to you. (8 HP, 5%)
- **`KERNEL PANIC`** — The big boss. Triggers a massive PagerDuty banner for the entire sprint, because of fucking course it does. (100 HP, leaks 25%, pays 40 story points)

**Defenders** (your arsenal, ranked cheapest first, just like your real-world tooling budget — damage per shot now climbs the poker scale with each upgrade):
- **`✏️ Linter` (5 SP)** — Bitches about the bugs' formatting until they literally die of shame. Damage: ½ → 1 → 2.
- **`💀 rm -rf` (8 SP)** — Deletes the bug. And probably your entire filesystem. Collateral damage is a feature. Damage: 3 → 5 → 8.
- **`{} Try/Catch` (13 SP)** — Catches bugs. Occasionally. The `finally` block is where all your hope goes to die. Damage: 2 → 3 → 5, splash 5 → 8 → 13.
- **`🔴 Breakpoint` (20 SP)** — Freezes those fuckers mid-execution. It has a red dot. Feels powerful. Is powerful. Damage: ½ → 1 → 2, splash 5 → 8 → 13, plus a slow for when you enjoy watching them suffer.
- **`🖧 Microservices` (40 SP)** — One defender that deals fan-out chain damage to 4 bugs. It's distributed, meaning when it inevitably shits the bed, you'll have no clue which part to blame. Damage: 1 → 2 → 3.

**Currency:** Story points, now estimated with actual Story Point poker (0, ½, 1, 2, 3, 5, 8, 13, 20, 40, 100) — because if we're running a fake economy, it might as well use the same fake numbers as your planning meetings. Defenders cost 5/8/13/20/40. Each upgrade costs the next poker value up the scale, like a Fibonacci sequence with commitment issues. Bugs pay ½ to 40. You start with 20 story points, which is 20 more than your last sprint planning gave you. Sprint-clear bonuses tier 3/5/8. Selling a tower returns 70% snapped to the nearest poker value, because the house always rounds in its favor.

## Controls (Don't Fuck These Up)

| Input | Action |
|---|---|
| Click a defender, click the board | Build a wall that shoots. |
| `1`–`5` | Select a defender using badges on the buttons, like a real IDE. |
| `U` / `S` | Upgrade or sell the selected defender. |
| `Esc` | Disarm placement, essentially disarming your own bullshit temper during a retro. |
| Click sprint button | Start the sprint, or call it early for +2 story points per remaining bug, because scope creep literally pays. |
| Hold sprint button 0.6s | Toggle auto-send. The 300–600ms gap is a dead zone, much like the middle of every planning meeting you've ever attended. |
| 🤖 | Auto-build: the game plays its damn self. This is the dream. This is the *whole* dream. |
| Logo click | Cycle through 8 themes. Alt+click or right-click toggles dark/light mode. Choosing a color scheme is the real endgame, and light themes are for absolute suckers. |

## Features (An incomplete list, just like your last sprint)

- **12 sprints + endless mode**, because the fucking backlog never dies and neither does this game.
- **Maze routing** — Bugs steer down one shared reverse-BFS flow field computed from the exit. It used to be per-bug pathfinding, back when we hated your CPU personally. Try to seal the route and the game vetoes your dumb ass.
- **Uptime SLA** — You get 20 lives, starting at 100.00%, losing 5% per escaped bug. Drop below 50% and the Merge PR button flashes `⚠ merge conflicts`. Drop below 30% and the uptime percentage itself turns red, like your manager's face during the incident review.
- **Bounty board** — 2–3 optional bounties per sprint (🎯), paying out in poker-scale story points, because nothing motivates you like side quests during crunch.
- **Breach log** — Leak forensics. Every bastard bug that escapes gets a timestamp and an HP% logged for the postmortem. There is always a postmortem.
- **ROLLBACK terminal** — When you lose, you get a terminal with ASCII box-drawing `ROLLBACK` art, death timestamps, and a random epitaph. Dying has never been this strictly on-brand. Dying also locks every gameplay control — only reset and retry stay live, because the game respects your grief but not your autonomy.
- **Build status panel** — Sits there showing a color-coded `git reset --hard HEAD` until the first leak. Then it gets a red border, screams `Build Failed`, and tracks your error count. We've all been there.
- **Defender icons** — Shop buttons and battlefield towers show icons (✏️ 💀 {} 🔴 🖧), for players who can't read but can tap.
- **`\BRANCHES`** — The CODE TREE panel is now `\BRANCHES`, because backslashes make everything look 40% more technical.
- **Sound** — Seven distinct destruction sound signatures for each invader, synthesized live using Web Audio. It starts muted so you don't piss off your coworkers.
- **Best-run records** — Saved in `localStorage` so your humiliating failures survive between sessions.

## Architecture (Abandon all hope, view-source is hell)

- **One fucking file.** 1,964 lines. 104KB. HTML, CSS, and JS crammed into a single document like it's 2004 and we've learned absolutely nothing.
- **One global state object**, `S`, referenced 359 damn times. There is no data flow. There is no unidirectional bullshit. Every function raw-dogs `S` like a raccoon diving into a trash can. It has only gotten worse. We're not fixing it. Don't ask.
- **No modules, no bundler, no framework, no TypeScript.** The entire type system is "well, it ran once."
- **`6.29` is used as 2π in 29 places.** Not `Math.PI * 2`. Not a named constant. Twenty-nine hardcoded `6.29`s smeared everywhere. The constant has reproduced since the last count. We don't know how. We're afraid to ask.
- **Magic numbers out the ass:** 35px cells, 28×17 grid, 0.6s hold threshold, 3s auto-start countdown, and now an entire poker scale (0, ½, 1, 2, 3, 5, 8, 13, 20, 40, 100) governing prices, damage, and HP. All tuned by feel, documented literally nowhere. This paragraph is the only documentation.
- **Canvas, now with caching (we're as surprised as you are):** The whole UI *was* redrawn from scratch every frame, until someone discovered offscreen canvases and ruined a perfectly good bit. Static IDE artwork and the route ribbon are cached; rgba strings are memoized with quantized alpha; obstacle tooltips only rebuild when you hover a different block. The menu bar is still painted *last* to stay on top, which is both a rendering strategy and a sad metaphor.
- **Pathfinding for people in a hurry:** One reverse BFS over an `Int32Array` head-index queue with a generation-stamped visited buffer and packed parents. Hot loops allocate nothing — lookup tables, in-place compaction, squared distances everywhere. Ten performance passes, applied one at a time, like ripping off ten band-aids very slowly while someone watches.
- **Theme system:** 8 themes × dark/light, saved under `bugbash_theme_v1`. This trash game has a more sophisticated theming architecture than most funded startups.

## Known Issues (Filed by QA, totally ignored by Dev — a tradition)

- **Fixed in v77:** 16 quoted `'ga(...)'` strings were passed as canvas colors. The canvas silently ignored them because they aren't colors, they are *cries for help*. Several elements simply didn't render for three whole versions and no one gave a shit.
- **Fixed in v105:** The BUILD error counter read a breach log that capped at 8 entries, so "8 errors" actually meant "8 or more, we've stopped counting, much like your manager."
- **Fixed in v119:** Arming auto-start before the first sprint changed the button label to "Sprint 1 incoming" and then did absolutely nothing. The label was aspirational. The timer was not.
- **Fixed in v131:** Dying no longer lets you keep building towers from beyond the grave. Death now revokes your commit access.
- **Fixed in v132:** The incident toast and PROBLEMS panel spell out RACE CONDITION in full, because "RACE COND" was technically a different bug and legally distinct.
- **Fixed in v154:** Uptime below 30% turns the percentage red. Previously it just sat there being low and green, which felt dishonest.
- **Ongoing:** Wave 1 was cleared by a bot. Waves 2–12 are completely theoretical. Balance is a myth.
- **Ongoing:** Zero live browser verification has ever occurred. Localhost is completely unreachable from the dev VM, so every release is validated by a headless stub harness and a terminal amount of unearned confidence.

## Testing

We forgot to hire QA.

## Backlog (The Graveyard)

Out of 20 proposed improvements, exactly 9 were built — #12 (leak screen shake) finally crawled out of the graveyard in v155, the rest are still rotting in the backlog just like your actual job:

2. Standalone leakless bounty · 4. Per-defender targeting priorities · 6. Memory Leak bug (the tragic irony of deprioritizing this isn't lost on anyone) · 7. Defender synergies · 9. Range preview · 13. Endless boss affixes · 16. `SHIPPED v1.0` victory sequence · 17. Upgrade specializations · 19. Maze templates · 20. Run report.

They'll get built right after the tech debt sprint. You know exactly the fucking one I mean.

## Contributing

Don't. There are 154 files and every single one is load-bearing. If you absolutely must, the workflow is: copy the latest file, increment the number, change one thing, attach the new file, and never overwrite the old one. The cache is always watching.

## License

MIT: *Merge It, Trash-it.* Do whatever the hell you want. The bugs certainly do.
