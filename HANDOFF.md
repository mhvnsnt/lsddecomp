# HANDOFF — lsddecomp

**Last updated: 2026-11-22 (America/New_York).**
**Repo:** `mhvnsnt/lsddecomp` (PUBLIC), default branch `main`.
**Purpose of this file:** any agent that picks up work here reads this FIRST, then the linked docs. It states what we've done, where we're at, and what we're working toward — so the owner can say "go to this repo, pick up the work" and you just know. Update this file in the same PR whenever the state changes (add, don't delete).

## 1. What this repo is

A complete, matching decompilation of **LSD: Dream Emulator** (PlayStation, 1998, Asmik Ace / OutSide Directors Company, SLPS-01556) — mirrored into the owner's account 2026-11-20. The C in `src/` compiles into an executable byte-for-byte identical to the one on the retail disc. Every one of the game's functions is done, named, and documented. To play it on a PC rather than rebuild the PS1 executable, see lsd-port (builds this same C as a native program).

This is the brian-oblivion lineage. It is NOT the same as the owner's other LSD decomps — see §5. How they relate:
- `mhvnsnt/lsd-decomp` — the AI-written matching decomp, actively documented (1,447/1,447 functions read, discoveries docs). Also complete; different codebase and docs.
- `mhvnsnt/lsd_decompiled` — the cawfee lineage, early-stage work-in-progress decomp.
- `mhvnsnt/lsddecomp-1` — the FirecatFG first attempt from 2024, assumption-heavy, last touched 2024-09-13.
- `mhvnsnt/LSDRevamped` — Figglewatts' Unity remake of the game (not a decomp).
- `mhvnsnt/libLSD` — Figglewatts' C# library for loading LSD data files.

## 2. Where we're at

### DONE
- **Complete matching decomp:** every game function in C; the build is verified byte-for-byte against retail SLPS_015.56 (SHA1 `76322eeade5ebb22dca57fdeac7d68c30f06308d`). A good build ends with `OK: build matches retail SLPS_015.56`.
- **64-bit host build (2026-10-05):** "Merge host-64-bit: the game's C builds and plays as a 64-bit host pro…" (`95f67e0`).
- **README rewrite (2026-10-17, `90a398e`):** "README: shorter, written for someone building or reading the game." Last push 2026-10-17.
- **Mirrored into this account 2026-11-20** (repo created here that day; history carried over).
- **Docs:** `docs/ARCHITECTURE.md` (start here), `docs/CONTRIBUTING.md` (read before changing code and keeping it matching).

### IN PROGRESS
- Nothing in progress. No open PRs, no releases in this mirror.

### BLOCKED
- Nothing blocked. The decomp is complete and verified.

## 3. What we're working toward

Reference and building block. The decomp is done; the work now is using it: for the owner's Sato games work (Western Heart pulls LSD in as a main Eastern Mind pair), this repo is the code-level reference for how LSD works — `src/app/` (application, memory pool, object framework, controller), `src/cd/` (disc reads), `src/graphics/` (screen, models, sprites, textures, FMV), `src/world/` (the dream: clock, stages, characters, mood graph), `src/sound/`, `src/ui/`, `src/psyq/` (Sony library functions rebuilt from disassembly). Pull understanding from here; do not re-derive it. If changes are ever made, they keep the match — read `docs/CONTRIBUTING.md` first.

## 4. Standing rules that apply here

- **Branch → PR → merge, always.** Never push to main directly. Add-only, zero-conflict PRs, no force pushes. (This is a public matching decomp — a bad merge breaks the byte match for everyone.)
- **Checkpoint-and-save law:** CHECKPOINT.md first, update after every step; the repo is the save; resume, never restart.
- **No-temp-storage law:** nothing in /tmp or any wipeable location, ever. Everything goes straight into the repo or a durable folder the second it exists.
- **Real-source-only:** this whole repo IS the real source. A change is kept only when the build still matches retail — that is the repo's own rule.
- **Licence/source logged honestly:** this project's own work (the C, headers, config, tools) is CC0 1.0. The game, Sony's SDK, and the maspsx patches in `tools/patches/` are not. This repo contains no game data and no Sony files — you need your own disc (SLPS-01556) and Sony's Psy-Q SDK (three redump zips from archive.org/download/ps1_sdks, in `sdk/`, still zipped, original names).
- **Never kill in-progress work.** Never delete game files or other lanes' work without the standing verification rules.

## 5. Key files and paths

| What | Where |
|---|---|
| Start reading | `docs/ARCHITECTURE.md`, then `include/basic_class.h` |
| Game code | `src/app/`, `src/cd/`, `src/graphics/`, `src/world/`, `src/sound/`, `src/ui/`, `src/psyq/` |
| Build + verify | `tools/setup.sh` (one time), `./build-and-verify.sh` (every build after) — must end `OK: build matches retail SLPS_015.56` |
| Build check hashes | `build.sha1`, `check.sha1` |
| Contributing (keep the match) | `docs/CONTRIBUTING.md` |
| Licence | `LICENSE` (CC0 for this project's own work) |
| Related repos (NOT this one) | `mhvnsnt/lsd-decomp`, `mhvnsnt/lsd_decompiled`, `mhvnsnt/lsddecomp-1`, `mhvnsnt/LSDRevamped`, `mhvnsnt/libLSD` |

## 6. Open decisions needing the owner

- **Which LSD decomp is the one to build on?** This repo (brian-oblivion lineage, complete, CC0) vs `lsd-decomp` (documented, 1,447/1,447 read). Both are complete matching decomps; the code and docs differ. The Sato-games pull into Western Heart needs one canonical source — his call, not a lane's.

## 7. How to pick up

1. Read this HANDOFF.md first, then `README.md` and `docs/ARCHITECTURE.md`.
2. To build: your own Japanese retail disc (SLPS-01556, SHA1 `76322eeade5ebb22dca57fdeac7d68c30f06308d`) in the repo root or extracted into `disk/` (`python3 tools/extract_exe.py "<bin>"`), plus the three Psy-Q SDK zips in `sdk/`. Then `./tools/setup.sh`, then `./build-and-verify.sh`.
3. Never commit game data, SDK files, or disc images. Never break the byte match — if the build doesn't say OK, the change does not land.
4. Land work branch → PR → merge, add-only.
5. Update this HANDOFF.md in the same PR when the state changes.
