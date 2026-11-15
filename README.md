# Ghost Flap: Skylands

> One little ghost. A sky full of trouble.

Ghost Flap: Skylands is a proposed single-player web arcade game: guide a small ghost through floating islands, luminous gates, moving ruins, storms, and shifting dream worlds. Simple flap controls meet a demanding, approximately four-hour campaign and an escalating endless mode.

## Project status

This README describes the intended web game, not a finished implementation. Browser prototypes and a separate native Swift concept have been explored; feature parity and production readiness have not been verified. Campaign progression, saved checkpoints, advanced hazards, and the full soundtrack are planned features.

See `LEVEL_DESIGN.md` for progression and `AUDIO_GUIDE.md` for sound requirements.

## The experience

- Immediate controls: tap, click, or press Space to flap; release to fall.
- A readable, stylized 3D world with floating islands and a charming ghost.
- Twelve campaign chapters targeting 240 minutes of successful play.
- Escalating challenges that teach skills before combining them.
- Original or properly licensed lo-fi music and responsive game sounds.
- Local progress saves, pause/resume, and quick retries.
- An optional endless mode with no final victory screen.

The visual goal is colorful, polished, stylized 3D—not a promise to match Fortnite's production budget. Use original characters, scenery, interface, and sounds; do not copy Fortnite assets or branding.

## Smallest version worth shipping

First ship one polished, approximately ten-minute chapter before building four hours of content.

1. Title screen with Play, Continue, Settings, and Controls.
2. One playable environment with three clearly taught obstacle families.
3. Reliable collision, scoring, death, checkpoint, and restart behavior.
4. One licensed music loop and a small sound-effect set.
5. Completion screen with best time and optional challenges.
6. Keyboard and touch controls, audio settings, and reduced-motion options.

Expand only after this slice is enjoyable, readable, and reliable on phones.

## Main flow

Title → New Game or Continue → Chapter Introduction → Flight → Checkpoint → Chapter Finish → Next Chapter → Final Trial → Campaign Complete.

On death, show a short, skippable result panel and allow immediate retry. Never require watching an advertisement to continue.

## Campaign and modes

| Mode | Purpose | Completion |
| --- | --- | --- |
| Story Flight | The core four-hour journey with checkpoint saves | Finish all 12 chapters |
| Practice | Replay unlocked sections without progression pressure | Player chooses when to stop |
| Endless Rift | Increasing difficulty and optional high-score chasing | Ends on a collision; no final victory |
| Iron Ghost | Optional no-death run after campaign completion | Finish the campaign without dying |

A first campaign clear will usually take longer than four hours because of retries. Exact duration must be tuned with playtesting.

## Challenge without unfairness

The campaign must be extremely difficult but physically beatable. Do not use invisible collisions, impossible random layouts, sudden unannounced physics changes, fake close calls, or difficulty secretly adjusted to cause a loss.

Every generated pattern must have a validated route from its permitted entry state. Boss encounters test movement and timing rather than requiring combat.

Replay value comes from mastery: route choices, optional collectibles, clean-run medals, chapter records, cosmetic rewards, and remix challenges. No paid power upgrades, energy timers, lost login streaks, or progress-erasing pressure.

## Pause, saves, and long sessions

Four hours describes the target successful campaign route, not a mandatory uninterrupted session.

- Allow pause at any time outside short transitions.
- Automatically pause when the tab becomes hidden.
- Save at checkpoints and chapter completion.
- Offer a dismissible break reminder around every 45 minutes.
- Resume a saved run from its last checkpoint after reloading.
- Clearly explain that local browser saves can be removed by clearing site data or private-browsing behavior.

## Proposed web architecture

- TypeScript with a modular game loop and a WebGL renderer such as Three.js.
- HTML/CSS menus with accessible buttons and visible keyboard focus.
- Fixed-timestep simulation, separate from rendering.
- Web Audio API for music and effects, unlocked by a user gesture.
- IndexedDB for versioned local progress; small preferences may use localStorage.
- Static hosting over HTTPS; no account or backend needed for the first release.

Three.js is proposed because it provides real 3D rendering without building a renderer from scratch. Pin the dependency version and bundle dependencies/assets rather than relying on a live CDN in production. These are web architecture recommendations, not changes to the native Swift app.

## Performance and accessibility

Target 60 fps on the agreed reference devices; offer a 30 fps low-power option. Reduce shadows, particles, scenery density, and resolution before changing gameplay. Keep simulation and hitboxes identical across quality settings.

Support remappable keyboard controls, touch input, separate music/effects volume, mute, readable text, reduced camera movement, non-color-only hazard cues, and no flashing effects. Menus should be screen-reader accessible. Fully nonvisual action gameplay is outside the first release and must not be implied.

## Audio

Use gentle lo-fi textures for exploration and more rhythmic arrangements for difficult sections. Important hazard cues must remain audible above the music and also have visual equivalents. Never autoplay audible music before consent through the Start or Enable Audio button.

Only distribute sounds and music with documented rights. See `AUDIO_GUIDE.md`.

## Release checks

- Verify chapter order, checkpoint restore, completion, and retry behavior.
- Validate generated routes and test difficult transitions with human players.
- Test Safari on iPhone/iPad, Android Chrome, and desktop Safari/Chrome/Firefox.
- Test tab switching, device rotation, audio interruption, storage failure, and reload.
- Publish asset credits, a privacy notice, and accurate browser requirements.
- Avoid claiming global leaderboards, cloud saves, or offline support until implemented.

## Deliberately excluded from the first release

Multiplayer, chat, accounts, global leaderboards, paid currencies, loot boxes, licensed commercial songs, and live-service events.

## Supporting documents

- `LEVEL_DESIGN.md` — campaign, hazards, challenge modes, and acceptance criteria.
- `AUDIO_GUIDE.md` — lo-fi music, sound effects, browser behavior, and licensing.

## Rights and credits

Choose a code license before publishing the repository. Track music, models, fonts, textures, and effects separately: a code license does not grant rights to third-party assets. Do not publish an asset whose redistribution rights are unclear.
