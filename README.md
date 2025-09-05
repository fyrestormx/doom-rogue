# Doom Rogue

*A progression & scaling layer for classic **DOOM**, built for **GZDoom 4.14.2**. Vanilla feel, a ticking timer, and tiered monster variants.*

---

## What is this?

**Doom Rogue** is an experiment: it is **100% written by ChatGPT 5 Thinking and Agent mode**, to see if an AI can author and balance a DOOM mod end-to-end.
**fyrestorm** prompt-engineers and playtests the builds.

Design pillars:

* **Timer-driven difficulty (“stages”)** — as the **run timer** crosses stage thresholds, monsters **scale up** via conservative internal scalars.
* **Vanilla-inspired monster tiers** — additional variants are defined in **DECORATE** and are **randomized from the start** (their odds do **not** increase with stage).
* **Automatic boons** — passive bonuses are granted from a rarity pool (**Common → Mythic**). There are **no menus and no player choices**.
* **No bleed/DoT**, no speed buffs, no free-ammo gimmicks, no splash-invulnerability; keep the classic DOOM cadence.

---

## Core Features

### ⏱️ Stage Timer & Difficulty Scaling

* A visible **timer** advances **STAGE** at fixed intervals.
* **When a new stage begins**, monsters receive increased difficulty scaling (e.g., HP/related scalars).
* Stages build tension without altering vanilla behavior cadence.

### 🧟 Monster Tiers (DECORATE)

* DECORATE introduces tiered variants (e.g., `_T2…`) that stay faithful to vanilla pacing.
* **Randomized from the start** via RandomSpawners; palette tints (via `TRNSLATE`) keep them readable.

### 🧰 Boons (Automatic • Rarity-Based)

Boons are **implemented and active** in this build and are drawn from a Common→Mythic pool. You **don’t** pick them; they are granted automatically with short, clean toasts.

### 🖥️ HUD & Feedback

* Left panel: key status.
* **TIME** and **STAGE** are shown so you can anticipate the next spike.
* Toasts use a concise two-line format (no “Boon Gained” preamble).

### 🔬 Diagnostics (Opt-in)

Concise console tags for testing and balance:

* `[DR HIT]`, `[DR DMG OUT]`
* Timer/stage and boon events (as applicable)
* Throttled to avoid spam in long sessions.

---

## Requirements

* **GZDoom**: **4.14.2** (pinned target)
* **IWAD**: DOOM/DOOM II (e.g., `DOOM2.WAD`)

---

## Install & Run

1. Download the **PK3** from this repository.
2. Launch GZDoom with the PK3:

   * **Windows**

     ```bat
     gzdoom.exe -iwad DOOM2.WAD -file doom_rogue_<version>.pk3
     ```
   * **macOS/Linux**

     ```bash
     ./gzdoom -iwad DOOM2.WAD -file doom_rogue_<version>.pk3
     ```

### Optional: Logging for Bug Reports

```bat
gzdoom.exe -iwad DOOM2.WAD -file doom_rogue_<version>.pk3 ^
  +logfile "gzdoom_doomrogue.log" ^
  +set developer 1 ^
  +set dr_dbg 1 ^
  +set dr_dbg_hits 1
```

Attach the log to issues with your command line and GZDoom version.

---

## Configuration (CVARs)

These CVARs are available in the current PK3:

| CVAR          | Type  | Default | Description                                         |
| ------------- | ----- | ------- | --------------------------------------------------- |
| `dr_dbg`      | Int   | `0`     | Master debug switch (0 off; >0 on).                 |
| `dr_dbg_hits` | Int   | `0`     | Hit/kill logging level (0 off, 1 basic, 2 verbose). |
| `dr_log_rate` | Float | `50.0`  | Debug print throttle (messages/sec).                |

---

## File Layout (inside the PK3)

* `DECORATE` — tiered monsters + RandomSpawners (vanilla-inspired, randomized from start)
* `TRNSLATE` — palette tints for readability
* `ZSCRIPT` — timer/stage logic, HUD, diagnostics, boons
* `MAPINFO` — registers event handlers
* `CVARINFO` — declares `dr_*` CVARs
* `SNDINFO` — sound aliases as needed

---

## Contributing

* **Issues**: include GZDoom version, your command line, IWAD, other mods, and a log (`+logfile … +set developer 1 +set dr_dbg 1 +set dr_dbg_hits 1`).
* **PRs**: keep changes **surgical**; preserve vanilla feel; align with the timer/stage philosophy and automatic boons.

---

## Credits

* **id Software** — DOOM
* **GZDoom** team & contributors
* **Experiment authored by**: **ChatGPT 5 Thinking + Agent mode (100%)**
* **Prompt engineering & playtesting**: **fyrestorm**
* Community testers and stream viewers for feedback, logs, and ideas

---

## License

See **LICENSE** (open an issue if missing; **MIT** is recommended).
