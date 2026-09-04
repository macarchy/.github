# Traction plan

A working record of the 2026-09-04 pass over the macarchy org: what the audit
found, what was changed, and what still needs a human. Not a pitch — a
checklist with its evidence attached, so the state survives the session that
produced it.

Repo names throughout are the current ones. Two were renamed after this pass:
`omarchy-mac` became `macarchy-core`, because `omarchy-mac/omarchy-mac` is a
separate and far more popular upstream project — the Arch/Hyprland distro for
Apple Silicon — and our repo collided with its name; and `macarchy-dfr` became
`macarchy-touchbar`, because "DFR" is Apple jargon and "touchbar" is the word
people search for.

## The audit (2026-09-04)

Eight public code repos, plus the `.github` profile repo.

| Measure | Value |
| --- | --- |
| Stars, all eight repos | **5** |
| Unique visitors, 14-day window, all eight repos | **39** |
| Moving images committed anywhere in the org | **1** |

Per-repo uniques over the same 14 days, which is where the 39 comes from:
`omarchy-aikit` 21, `macarchy-core` 7, `omarchy-aquarium` 3, `apple-glass` 3,
`jarvis` 2, `macarchy-touchbar` 1, `macarchy-install` 1, `apple-glass-light` 1.
One repo carries more than half the traffic; four are effectively undiscovered.

Four specific defects, each verified before it was written down:

- **`macarchy-touchbar` had no `LICENSE` file.** GitHub reported no licence for it,
  which also made the org profile's "Everything is MIT-licensed" untrue.
- **`omarchy-aikit`'s README pointed at `Atypical-Consulting`**, the org's
  former name. The CI badge, the `omarchy plugin add` line meant to be copied,
  the `git clone` line, and the PKGBUILD `url`/`source` all sent a reader
  somewhere other than the page they were reading — in the single
  most-visited repo of the org.
- **`jarvis` had 0 releases.** Its release-please PR (#2) had been open since
  2026-09-02, so the tag, the changelog and the release page did not exist.
- **One moving image org-wide.** `jarvis/docs/media/fish.gif`, committed
  2026-09-02. Every other repo in the org is about something that moves —
  an animated shader background, a live glass blur, a Touch Bar, a voice
  loop — and showed it as a still frame.

## The four moves

1. **Show the thing moving.** The org's whole differentiator is motion, and it
   was being advertised in still frames. A GIF now leads the aquarium README
   and the org profile; the theme repos got a shot list for the clips they
   still need.
2. **Say who it is for.** Several repos excluded their own audience by name.
   The aquarium binds exactly three Wayland globals — `wl_compositor`,
   `wl_output` and `zwlr_layer_shell_v1` (`src/main.c`) — and otherwise needs
   only GLES2, so it *should* run unchanged on any wlr-layer-shell compositor:
   Sway, river, Wayfire, labwc. It has only ever been run on Hyprland; nobody
   has tested the others, and its README now names Hyprland as the only
   compositor it is developed and tested on. Before, it just said
   "Hyprland/Omarchy". Jarvis's record → transcribe → think → speak loop
   needs only Linux, PipeWire, Python 3, voxtype and Claude Code, and buried
   that below the fold.
3. **Fix the front door and the broken self-references.** The org profile
   listed five of eight repos, omitted the installer, and asked people to
   clone two repos by hand. The aikit's links pointed at the old org.
4. **Write down what only this project can say.** The theme READMEs were
   21-line stubs; the blur numbers, the measured-contrast palette and the
   fact that both were tuned against the animated aquarium existed only in
   source comments.

## Done in this pass

All as pull requests. **Nothing was merged**, and nothing was published
outside GitHub.

| Repo | PR | What |
| --- | --- | --- |
| `.github` | #1 | All eight repos on the profile, grouped by what hardware they need; animated hero; one-line install first |
| `omarchy-aquarium` | #8 | Animated GIF + h.264 clip, `make demo` to regenerate; "Without Omarchy" section; unpublished outreach drafts under `docs/outreach/` |
| `omarchy-aikit` | #8 | Every `Atypical-Consulting` self-reference repointed at `macarchy`; PKGBUILD brought to a publishable state (`pkgver()` from the tag, real `depends`, `.SRCINFO` committed) |
| `jarvis` | #3 | One sentence above the fold saying the voice loop is portable; mirrored in `README.fr.md` |
| `apple-glass` | #3 | README expanded from the theme files: blur numbers and why, palette table, per-surface alphas, the aquarium as tuning target; `docs/SHOTS.md` |
| `apple-glass-light` | #3 | The same, plus the measured-contrast palette story; `docs/SHOTS.md` |
| `macarchy-touchbar` | #6 | The missing `LICENSE` (MIT); README rewritten to speak to tiny-dfr's users; an animated `docs/media/touchbar.gif` |
| `.github` | this PR | This document |

### Descriptions and topics

Repo metadata was set directly with `gh repo edit` (not via PR), and the pass
was redone across all nine repos rather than the two it started with. Every
description was rewritten to 110 characters or fewer — around where GitHub
search results and topic pages truncate — and every code repo now carries
12–18 topics. Two corrections worth naming: `macarchy-core` lost the stale
`touchbar` topic (the Touch Bar moved out to `macarchy-touchbar`), and
`macarchy-touchbar` carries both `touch-bar` and `touchbar`, since people search
for it both ways.

The state as of 2026-09-04, read back from the API
(`gh api repos/macarchy/<name> --jq '.description, (.topics|join(" "))'`):

| Repo | Description | Topics |
| --- | --- | --- |
| `omarchy-aikit` | Your backlog, one keystroke away — launch Claude Code sessions from the Omarchy bar, off a local GitHub mirror | 16 — `ai` `ai-agents` `arch-linux` `automation` `claude` `claude-code` `developer-tools` `github-cli` `hyprland` `linux` `omarchy` `omarchy-plugin` `quickshell` `sqlite` `tmux` `wayland` |
| `macarchy-core` | macOS behaviours for a MacBook on Omarchy/Asahi: dock, Cmd keys, Cmd+Tab, pinch gestures, auto-brightness | 13 — `apple-silicon` `arch-linux` `asahi-linux` `battery` `dock` `gestures` `hyprland` `linux` `macbook` `macos` `omarchy` `trackpad` `wayland` |
| `omarchy-aquarium` | A live aquarium as your desktop background: one GLSL shader on a Wayland layer surface, any wlroots compositor | 17 — `asahi-linux` `desktop-background` `fragment-shader` `glsl` `hyprland` `layer-shell` `linux` `live-wallpaper` `omarchy` `opengl-es` `ricing` `screensaver` `shader` `unixporn` `wallpaper` `wayland` `wlroots` |
| `apple-glass` | macOS-inspired dark glass for Omarchy and Hyprland: translucent blur, vibrancy, a light twin at sunrise | 17 — `alacritty` `blur` `color-scheme` `dark-theme` `desktop-theme` `glassmorphism` `hyprland` `kitty` `linux` `macos` `omarchy` `omarchy-theme` `quickshell` `ricing` `theme` `unixporn` `wayland` |
| `apple-glass-light` | macOS-inspired light glass for Omarchy and Hyprland: translucent blur, vibrancy, a dark twin at sunset | 17 — the same set with `light-theme` in place of `dark-theme` |
| `jarvis` | A bilingual voice assistant for Linux: Whisper transcribes locally, Claude thinks, the shell is its hands | 18 — `ai-assistant` `bash` `claude` `claude-code` `french` `hyprland` `linux` `llm` `local-first` `piper-tts` `pipewire` `speech-to-text` `stt` `text-to-speech` `tts` `voice-assistant` `wayland` `whisper` |
| `macarchy-touchbar` | A Touch Bar daemon for MacBooks on Linux — draws every pixel over DRM, follows the focused app, takes modules | 17 — `apple-silicon` `asahi-linux` `cairo` `daemon` `drm` `evdev` `hyprland` `linux` `macbook` `macbook-pro` `omarchy` `python` `systemd` `tiny-dfr` `touch-bar` `touchbar` `wayland` |
| `macarchy-install` | One command from a fresh Omarchy-on-Asahi install to the whole macarchy suite — idempotent, with a doctor | 12 — `apple-silicon` `arch-linux` `asahi-linux` `bootstrap` `dotfiles` `hyprland` `installer` `linux` `macbook` `omarchy` `setup-script` `wayland` |
| `.github` | Profile and shared community-health files for the macarchy org | 5 — `apple-silicon` `asahi-linux` `hyprland` `macbook` `omarchy` |

`.github` deliberately keeps a short description and a small topic set: it is
the profile repo, not something anyone should find by searching for a tool.

## Left for a human

Ordered by how much is blocked behind each.

- [ ] **Merge the eight documentation PRs in the table above** (this one
      included). Everything else waits on them. `macarchy-touchbar` #6 is the one
      that also carries the missing `LICENSE`, so until it lands the org
      profile still cannot honestly say "Everything is MIT-licensed".
- [ ] **Merge the four pending release-please PRs:** `omarchy-aikit` #7
      (0.3.0), `jarvis` #2 (1.4.0), `apple-glass` #2 (0.2.0) and
      `apple-glass-light` #2 (0.2.0). Jarvis's has been open since 2026-09-02;
      until it lands, jarvis has no release, no tag and no changelog.
- [ ] **Publish the `aikit-git` AUR package.** `omarchy-aikit`'s PKGBUILD and
      `.SRCINFO` are ready and were validated with `makepkg` locally, but the
      AUR push needs the maintainer's own AUR SSH key and is a publish outside
      GitHub, so it was deliberately not done here.
- [ ] **Capture the theme screenshots.** `apple-glass/docs/SHOTS.md` (12 shots)
      and `apple-glass-light/docs/SHOTS.md` (13 shots) are ordered checklists,
      about ten minutes each in one sitting. They need the live desktop, which
      is why no agent took them. Shots 01–03 and the paired light/dark frame
      should be captured in the same sitting for both themes so the window
      layout matches.
- [ ] **Post the aquarium clip to r/unixporn.** A draft sits unpublished at
      `omarchy-aquarium/docs/outreach/unixporn-post.md`, with a standalone
      write-up beside it, and the clip it needs is the GIF landing in
      `omarchy-aquarium` #8. Nothing was posted anywhere; that is a decision,
      not a task an agent should take.
- [ ] **Decide the `terminal`-tag change in both theme repos.** `apple-glass`
      and `apple-glass-light` each have an uncommitted, finished hunk in
      `hyprland.lua` that replaces the hand-written terminal class regex
      (`^(Alacritty|foot|footclient|kitty|org\.omarchy\.agent)$`) with
      Omarchy's own `tag = "terminal"`, which would cover per-app TUI ids as
      they appear. It is the maintainer's own work in progress and was left
      untouched; the theme READMEs describe only what is committed. Commit it
      or drop it — either way the READMEs then need one sentence back.

## A number to treat carefully

The star count was **5** at the start of this session and **12** when
re-checked before writing this page. That is recorded because it is what the
API returned, not because anything here caused it — none of the work above was
merged or announced in between. Re-measure the 14-day uniques a
week after the PRs land; that is the number worth trusting.
