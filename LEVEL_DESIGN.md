# Ghost Flap: Skylands — Level and Challenge Design

## Status and goal

This is a design specification for future implementation, not a list of features already present in the prototype.

Create a campaign that takes approximately four hours of successful play to complete, with approachable opening minutes and an exceptionally demanding finale. Deaths, pauses, practice, and menus add to real-world play time.

The campaign is beatable. Endless Rift is deliberately unfinishable because it has no final level, not because it secretly creates unavoidable collisions.

## Core loop

Read the next gates → time a flap → control the fall → pass the obstacle → earn progress → choose a safer or harder route → reach a checkpoint.

Flapping applies a consistent upward impulse. Gravity, maximum fall speed, and the ghost's collision shape remain stable unless a clearly introduced environmental effect explicitly modifies them.

The first 30 seconds should include one safe flap lesson, one generous gate, one positive sound cue, and a clear preview of the next challenge. Do not begin with a punishment trap.

## Campaign structure

Each chapter contains four stages. Every stage lasts five minutes of active successful flight, giving 48 stages × 5 minutes = 240 minutes.

Within each chapter:

1. **Discover:** introduce one mechanic with forgiving spacing.
2. **Develop:** vary the mechanic and introduce route decisions.
3. **Combine:** mix it with previously learned mechanics.
4. **Trial:** a choreographed escape or guardian sequence.

The five-minute stage budget includes short safe glides and transitions, not five minutes of uninterrupted maximum-intensity obstacles. Stage time advances with active simulation only; menus, pause, and death screens never count.

| Chapter | World | Main mechanic | Trial | Successful flight |
| --- | --- | --- | --- | --- |
| 1 | Cottoncloud Coast | Fixed gates, basic climb and fall | Follow a friendly sky whale through wide arches | 20 min |
| 2 | Lantern Orchard | Slow vertical gate movement | Fly through a procession of swinging lantern gates | 20 min |
| 3 | Windmill Heights | Visible gust lanes with predictable pulses | Climb past alternating windmill sails | 20 min |
| 4 | Violet Quarry | Descending slabs and staggered openings | Escape a collapsing crystal corridor | 20 min |
| 5 | Rainlight Harbor | Rain and moving platforms without visual occlusion | Navigate a storm-lighthouse sequence | 20 min |
| 6 | Clockwork Canopy | Rotating frames and timed shutters | Match the rhythm of a giant clock tower | 20 min |
| 7 | Mirror Marsh | Reflections that decorate rather than hide hazards | Cross twin ruins with offset gate rhythms | 20 min |
| 8 | Ember Islands | Telegraphing vents and alternating safe channels | Escape the wake of an ember serpent | 20 min |
| 9 | Aurora Railway | Moving obstacle trains with clear schedules | Pass a sequence of sky-rail crossings | 20 min |
| 10 | Gravity Garden | Marked low-gravity zones with entry previews | Chain normal and low-gravity rooms | 20 min |
| 11 | Fracture Citadel | Faster combinations of all established mechanics | Survive four guardian movement trials | 20 min |
| 12 | The Last Sky | Precision routes and earlier motifs remixed | A five-minute final ascent, then an ending | 20 min |

Guardian scenes are obstacle encounters. Do not add weapons or combat to the first release.

## Stage pacing

Suggested five-minute stage composition:

- 0:00–0:30: clear re-entry and a readable reminder of the current mechanic.
- 0:30–1:30: first challenge sequence.
- 1:30–1:45: low-pressure scenery glide.
- 1:45–2:30: more complex sequence ending at a checkpoint.
- 2:30–3:30: second variation or optional route.
- 3:30–3:45: recovery glide with a preview of the final pattern.
- 3:45–4:45: the stage's hardest sequence.
- 4:45–5:00: safe arrival, result feedback, and transition.

These timings are initial targets, not a requirement to pad weak content. Ship fewer excellent stages before stretching the campaign to four hours.

## Difficulty rules

Tune values in units relative to ghost collision diameter and viewport height. Final physics constants must come from the actual implementation and playtests, not this document.

- Early gate openings: approximately 4.5–5 collision diameters.
- Late standard gate openings: approximately 2.5–3 diameters.
- Keep reaction lead time at least 1.8 seconds early and 1.2 seconds on late standard routes on the smallest supported viewport.
- Introduce only one new mechanic at a time.
- Show moving-hazard direction and timing before the player commits.
- Do not increase speed and shrink the gap at the same introduction point.
- Do not reduce visibility to manufacture difficulty.
- Place optional challenge routes away from the mandatory survival line.
- Avoid repetitive rapid tapping as the main source of difficulty.

These are starting constraints, not a proof of fairness. Validate the complete sequence, including entry velocity, previous gate exit, moving-hazard phase, and touch-input latency.

## Pattern generation and validation

Build a library of authored patterns rather than drawing every gate independently at random. A pattern specifies permitted entry states, obstacle motion, duration, possible exits, and difficulty tags.

Before accepting a sequence:

1. Propagate reachable position/velocity states with the same fixed-step physics as gameplay.
2. Account for obstacle movement at the relevant simulation times.
3. Reject connections with no robust safe route.
4. Require a safety margin around collision boundaries and input timing.
5. Verify representative seeds with an automated controller.
6. Human-playtest for readability, comfort, and touch feasibility.

A solver finding one perfect route is not enough. A reasonable family of input timings must succeed. Use a known-safe authored fallback when generation cannot find a valid continuation.

## Checkpoints and failure

Story Flight saves at stage entry and the midpoint, limiting lost progress to approximately 2.5 minutes of successful play. A checkpoint records the seed, stage, progress marker, score state, collected-item state, and a versioned schema.

Resume from an authored safe entry state with a countdown and a short hazard-free approach. Do not spawn the ghost directly inside a moving hazard.

On collision:

- Show an immediate visual and audio response without intense flashing.
- Freeze the result state and identify the obstacle that caused the hit.
- Offer Retry Checkpoint as the primary action.
- Preserve previously banked collectibles and never award them twice.
- Offer Practice Section and Return to Menu without a penalty.

Only Iron Ghost removes checkpoint recovery, and it requires explicit opt-in with a clear explanation. Story progress remains intact if that challenge fails.

## Reasons to replay

### Chapter medals

Award separate medals for completion, no-death completion, and collecting all optional wisps. Do not force all goals into one run.

### Wisps and cosmetics

Place collectible wisps on riskier but validated routes. Unlock trails, ghost expressions, and palette changes. Cosmetics must not alter physics, conceal hazards, or grant score advantages.

### Chapter records

Track best clean-run score and fewest retries locally. Count only active simulation time where timing is relevant. Do not reward leaving the tab open.

### Remix challenge

After the campaign, unlock curated or seeded remixes built from verified patterns. Any calendar-based challenge must remain available in an archive; no login streak or fear-of-missing-out penalty.

### Endless Rift

Unlock after Chapter 2 so players do not need to finish four hours first. Mix learned hazards, ramp difficulty gradually, and cap raw speed and minimum gap size. Increase pattern complexity only within validated safe limits.

No final boss or completion state exists. After a run, show the player's local best and allow an immediate restart. Do not advertise this as an unbeatable campaign.

### Iron Ghost

An optional prestige run through the campaign without dying. Allow pause and honest suspend/resume. Any competitive ranking or anti-cheat system is outside the initial scope; do not imply local saves are tamper-proof.

## Comfort and accessibility

- Pause on demand and when the page is hidden.
- Make a break suggestion around every 45 minutes, never during an active hazard.
- Offer reduced camera shake, disabled motion blur, and reduced background movement.
- Avoid strobe effects and mandatory rhythm-by-audio-only obstacles.
- Keep color-independent shapes and movement cues for every hazard.
- Provide a separately labeled Assist option with wider gates and lower speed.
- Keep Assist progress and completion valid; separate records only where the player needs comparable scores.

## Acceptance tests

1. Campaign successful-flight budgets total 240 minutes.
2. Pausing or backgrounding the tab does not advance simulation or hazards.
3. Reload restores the last committed checkpoint without duplicated rewards.
4. Every pattern connection has a validated route with timing tolerance.
5. Story retries lose no more than the current checkpoint segment.
6. A fresh player can understand flap, fall, and gate passage in 30 seconds.
7. Every chapter teaches its new mechanic before requiring a difficult combination.
8. Endless mode never emits an impossible layout merely to end a long run.
9. Audio-muted players receive the same necessary hazard information.
10. Final completion shows an actual ending and unlocks chapter replay.

## Playtest measurements

Record locally during development: death location, retry count, checkpoint duration, abandoned stages, missed cues, and performance spikes. Do not upload player behavior without a disclosed privacy design. Use playtest results to remove confusing difficulty before adding more obstacles.
