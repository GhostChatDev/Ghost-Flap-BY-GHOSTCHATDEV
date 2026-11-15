# Ghost Flap: Skylands — Audio and Web Delivery Guide

## Status

This is an implementation brief. No audio recordings, music files, licenses, or completed web-game code are included with these documents.

## Creative direction

Warm, dreamy lo-fi beats against a floating fantasy world: soft electric piano, restrained bass, dusty percussion, airy pads, and occasional bell-like ghost motifs. Keep the mix relaxing enough for long sessions while hazards remain immediately readable.

Do not imitate a specific artist, sample a commercial recording without permission, or use music taken from Fortnite or a streaming playlist.

## Music plan

Commission or license six original, loopable musical themes plus menu and ending cues. Reuse themes across paired chapters with alternate stems and arrangements; avoid making a single short loop carry four hours.

| Cue | Placement | Suggested tempo | Character |
| --- | --- | --- | --- |
| Home in the Clouds | Title and settings | 72 BPM | Soft keys, warm pad, light texture |
| Cottoncloud Drift | Chapters 1–2 | 76 BPM | Gentle drums, plucked melody |
| Wind and Crystal | Chapters 3–4 | 82 BPM | Swinging hats, airy arpeggios |
| Rain on the Clocktower | Chapters 5–6 | 84 BPM | Muted keys, precise percussion |
| Embers at Dusk | Chapters 7–8 | 88 BPM | Rounded bass, restrained tension |
| Aurora Express | Chapters 9–10 | 92 BPM | Driving groove, bright pads |
| Last Light | Chapters 11–12 | 96 BPM | Wider arrangement, hopeful finale |
| A Ghost Comes Home | Campaign ending | 72 BPM | Gentle resolution of the main motif |

Tempo is musical direction, not an input timing requirement. The game must remain playable with music muted.

## Asset requirements

For each gameplay theme, request:

- Approximately 3–5 minutes of musical material with a seamless loop region.
- Separate ambient, beat, and tension stems with exactly aligned duration and sample rate.
- A clean intro and optional ending when budget allows.
- No clipping, obvious loop clicks, or abrupt reverb cuts.
- Source WAV masters plus web delivery encodes tested in supported browsers.
- Written license and attribution requirements.

Tempo changes between themes should be handled by a deliberate transition, not by abruptly stretching all audio. Repeated material should vary through authored stem arrangements without becoming distracting.

## Adaptive playback

- Menu: ambient and melody at low intensity.
- Standard flight: add the relaxed beat stem.
- Trial approach: introduce a quiet tension stem after a visible warning.
- Trial: raise musical energy modestly, not overall loudness dramatically.
- Checkpoint: play a short confirmation cue over a temporary music dip.
- Collision: play a soft impact and short failure cue; avoid startling volume spikes.
- Pause: pause or gently fade gameplay audio while preserving the chosen settings.
- Resume: restore audio after the countdown, following browser permission rules.

Crossfade between music themes over roughly 2–4 seconds. Share scheduling between stems so they remain aligned. Do not restart the track every time the player retries a short section.

## Sound effects

| Event | Sound direction | Behavior |
| --- | --- | --- |
| Flap | Soft airy puff | Short; cap overlapping voices |
| Gate passed | Light rounded chime | Clear without piercing high frequencies |
| Wisp pickup | Tiny glassy sparkle | Different from score confirmation |
| Checkpoint | Warm three-note phrase | Unmistakable positive confirmation |
| Hazard warning | Gentle directional pulse | Always paired with a visual warning |
| Wind zone | Filtered air | Fade smoothly on entry and exit |
| Moving machinery | Quiet wooden or metallic rhythm | Decorative unless visually telegraphed |
| Collision | Soft thump and dispersing air | No loud explosion |
| Death result | Brief descending motif | Avoid shaming or mocking the player |
| Retry countdown | Three restrained ticks | Also display the countdown visually |
| Chapter completion | Short celebratory phrase | Never obscure menu controls |
| Campaign completion | Longer original resolution | Skippable presentation |
| Button focus/select | Subtle tick or tap | Optional with effects volume |

Use a small pool of flap and pickup variations to prevent fatigue. Limit simultaneous effects and prioritize collision, warnings, and checkpoint feedback above decorative ambience.

## Mixer and user controls

Provide Master, Music, and Effects volume controls plus a clear Mute button. Remember settings locally when storage is available. Make all controls usable with keyboard and touch.

Use separate gain buses for music and effects. Duck music briefly for essential cues. Prevent clipping at the master output; a dynamics compressor can provide a final safety stage but is not a substitute for sensible asset levels.

Default volume should be conservative. If storage fails, the game must still work and should explain that settings may not persist.

## Browser audio behavior

1. Load the title screen silently.
2. Enable or resume the AudioContext from a user interaction such as Start Flight or Enable Audio.
3. If audio cannot start, continue silently and offer an Enable Audio button.
4. Pause gameplay when the page is hidden; stop or suspend its active audio as appropriate.
5. On return, show a resume interaction when browser policy requires it.
6. Recover from audio interruptions without advancing the game behind the player's back.

Do not assume a browser will permit autoplay or automatically resume audio. Test actual Safari and Chrome behavior on mobile hardware.

## Web asset delivery

Use short decoded buffers for responsive sound effects. For longer music, choose streaming media or a carefully budgeted decoded-stem system after measuring memory use on phones. Several minutes of uncompressed multichannel audio can consume significant memory.

Start with menu audio and the first chapter's required assets. Load later chapter music ahead of transitions, with a silent or ambient fallback if loading fails. Do not make the entire four-hour campaign soundtrack a startup download.

Host assets over HTTPS with correct content types and caching. If files are hosted on another origin, configure and test its CORS behavior. Offline support requires an explicit service-worker and caching design; it is not automatic.

## Licensing checklist

Keep an asset ledger containing title, creator, source, purchase or permission record, license version, attribution text, and any restrictions.

Confirm rights for:

- Commercial web-game use if monetization is possible.
- Interactive playback and looping.
- Editing, mixing, and creation of stems where needed.
- Distribution of audio assets as part of browser delivery.
- Trailers and promotional videos if those are planned.

A streaming subscription is not a game distribution license. “Royalty-free” does not mean unrestricted. If using generative audio, review the service's terms and provenance risks; do not promise exclusive rights without a basis.

Publish required credits in the game and repository. Keep proof of permission outside the public repository when it contains private purchase details.

## Suggested implementation milestones

### 1. Playable web slice

One world, core movement, collision, restart, responsive controls, one music theme, and essential effects. Confirm the game is fun before expanding content.

### 2. Progress foundation

Versioned saves, checkpoints, chapter selection, settings, pause/background handling, and restore tests.

### 3. Campaign production

Build and validate authored patterns, then ship chapters in playable batches. Test visual clarity, input latency, route solvability, and asset streaming.

### 4. Replay and polish

Cosmetic unlocks, practice, Endless Rift, optional Iron Ghost, adaptive music, accessibility, and lower-end device tuning.

### 5. Web release

Production build, HTTPS hosting, real-device browser testing, privacy notice, credits, error fallbacks, and honest feature descriptions.

## Audio acceptance tests

- Nothing audible plays before a permitted user interaction.
- Mute silences every audio bus, including menu sounds.
- Music and effects sliders act independently.
- Saved preferences restore when browser storage is available.
- Flapping repeatedly does not produce distortion or unlimited voices.
- Music loops without an audible click or growing stem drift.
- Pause, tab switches, phone interruptions, and resume do not double the soundtrack.
- Failed or missing audio files do not stop gameplay.
- Essential warnings remain understandable with all audio off.
- The quietest and loudest sections are comfortable during headphone testing.
- All shipped assets have recorded permission and required credits.
