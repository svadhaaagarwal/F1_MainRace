# Project Driver 01 — Sunday (Race Day)

The third and final chapter of the anniversary trilogy. A browser-based Formula One
"Driver Evaluation — Final Assessment" that slowly reveals itself as a love letter.

**Canonical configuration (hardcoded, self-contained):**
Red Bull Ring · Spielberg, Austria · Dry · **Sunset** · Single flying evaluation lap.
Fully independent of the Friday/Saturday builds — no shared save data.

---

## Build status

**Phase 1 — Foundation** (this build)
- Single-page shell (no reloads / no routing)
- Red Bull colour system (hardcoded)
- Global state + Mission Controller phase machine
- Procedural Web Audio engine (boot / UI / engine / ambience)
- Asset Manager with exact-filename slots + graceful in-universe fallbacks
- Full **Boot → System Restore → Team Skin → Mission Brief → Cockpit → Ignition → Formation Countdown**
- Live cockpit frame + HUD with power-on self-test

Phases 2–5 (driving engine, pit-stop puzzles + archive recordings, DRS/finish,
identity reveal + love letter + shutdown, polish) arrive in later builds.

---

## Run locally

Because the audio engine and asset fetches need a real origin, serve the folder
rather than opening the file directly:

```bash
# any static server works, e.g.
python3 -m http.server 8000
# then open http://localhost:8000
```

Add `?reset` to the URL to clear the saved checkpoint.

---

## Deploy on Vercel

1. Push this folder to a GitHub repo.
2. In Vercel: **New Project → import the repo**.
3. Framework preset: **Other** (it is a static site — no build step).
4. Deploy. `index.html` is served at the root.

---

## Assets — EXACT filenames

The experience runs with **no assets present** (procedural sound + in-universe
placeholders). To add your real media, drop files into `/assets` using these
**exact** names and paths:

### `/assets/audio`
| File | What it is | Used in |
|------|------------|---------|
| `music_formation_f1_theme.mp3` | Brian Tyler — Formula 1 Theme (instrumental) | Formation lap |
| `music_drs_lose_my_mind.mp3` | Don Toliver — Lose My Mind (instrumental) | DRS overtake |
| `music_final_surili.mp3` | Surili Akhiyon Wale (instrumental) | Final lap / love letter |
| `archive_recording_01.mp3` | Your voice note #1 | Pit Stop One |
| `archive_recording_02.mp3` | Your voice note #2 | Pit Stop Two |

### `/assets/video`
| File | What it is | Used in |
|------|------------|---------|
| `love_letter.mp4` | The final anniversary video (with audio) | Love Letter |

### `/assets/images`
| File | What it is |
|------|------------|
| `puzzle_sliding.jpg` | Photo for the Pit Stop One sliding puzzle |
| `memory_01.jpg` … `memory_06.jpg` | The six photos for the Pit Stop Two matching puzzle |

> The three music tracks are copyrighted commercial recordings — you supply your own
> licensed files. Until a file exists, its slot falls back gracefully (procedural
> ambience for music, typed/placeholder fallbacks elsewhere) so the build never breaks.

---

## Notes

- Desktop-first (reference 1440×900). No mobile support by design.
- Controls (from Phase 2): **← / →** steer, **hold Space** throttle, **mouse** for puzzles.
  `Enter` mirrors the primary on-screen action.
