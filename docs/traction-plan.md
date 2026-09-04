# Traction plan

A working record of the 2026-09-04 pass over the macarchy org: what the audit
found, what was changed, and what still needs a human. Not a pitch — a
checklist with its evidence attached, so the state survives the session that
produced it.

## The audit (2026-09-04)

Eight public code repos, plus the `.github` profile repo.

| Measure | Value |
| --- | --- |
| Stars, all eight repos | **5** |
| Unique visitors, 14-day window, all eight repos | **39** |
| Moving images committed anywhere in the org | **1** |

Per-repo uniques over the same 14 days, which is where the 39 comes from:
`omarchy-aikit` 21, `omarchy-mac` 7, `omarchy-aquarium` 3, `apple-glass` 3,
`jarvis` 2, `macarchy-dfr` 1, `macarchy-install` 1, `apple-glass-light` 1.
One repo carries more than half the traffic; four are effectively undiscovered.

Four specific defects, each verified before it was written down:

- **`macarchy-dfr` had no `LICENSE` file.** GitHub reported no licence for it,
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
   The aquarium needs only `wlr-layer-shell` and GLES2 — Sway, river, Wayfire
   and labwc run it unchanged — and said "Hyprland/Omarchy". Jarvis's
   record → transcribe → think → speak loop needs only Linux, PipeWire,
   Python 3, voxtype and Claude Code, and buried that below the fold.
3. **Fix the front door and the broken self-references.** The org profile
   listed five of eight repos, omitted the installer, and asked people to
   clone three repos by hand. The aikit's links pointed at the old org.
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
| `omarchy-aquarium` | #8 | Animated GIF + h.264 clip, `make demo` to regenerate; "Without Omarchy" section; topics; unpublished outreach drafts under `docs/outreach/` |
| `omarchy-aikit` | #8 | Every `Atypical-Consulting` self-reference repointed at `macarchy`; PKGBUILD brought to a publishable state (`pkgver()` from the tag, real `depends`, `.SRCINFO` committed) |
| `jarvis` | #3 | One sentence above the fold saying the voice loop is portable; mirrored in `README.fr.md` |
| `apple-glass` | #3 | README expanded from the theme files: blur numbers and why, palette table, per-surface alphas, the aquarium as tuning target; `docs/SHOTS.md` |
| `apple-glass-light` | #3 | The same, plus the measured-contrast palette story; `docs/SHOTS.md` |
| `.github` | this PR | This document |

Repo topics were added directly (not via PR) to `apple-glass` and
`apple-glass-light`: `hyprland`, `wayland`, `glassmorphism`, `blur`,
`quickshell`. `omarchy-aquarium` gained `shader`, `live-wallpaper`,
`wlroots`, `desktop-background`, `opengl-es`.

## Left for a human

Ordered by how much is blocked behind each.

- [ ] **Merge the open PRs above.** Everything else waits on them.
- [ ] **Merge the `jarvis` release PR (#2).** Open since 2026-09-02; until it
      lands, jarvis has no release, no tag and no changelog. Same for the
      release-please PRs open on `omarchy-aikit` (#7), `apple-glass` (#2) and
      `apple-glass-light` (#2).
- [ ] **Publish the AUR package.** `omarchy-aikit`'s PKGBUILD and `.SRCINFO`
      are ready and were validated with `makepkg` locally, but pushing to the
      AUR is a publish outside GitHub and was deliberately not done here.
- [ ] **Capture the theme screenshots.** `apple-glass/docs/SHOTS.md` (12 shots)
      and `apple-glass-light/docs/SHOTS.md` (13 shots) are ordered checklists,
      about ten minutes each in one sitting. They need the live desktop, which
      is why no agent took them. Shots 01–03 and the paired light/dark frame
      should be captured in the same sitting for both themes so the window
      layout matches.
- [ ] **Post to r/unixporn.** A draft sits unpublished at
      `omarchy-aquarium/docs/outreach/unixporn-post.md`, with a standalone
      write-up beside it. Nothing was posted anywhere; that is a decision, not
      a task an agent should take.
- [ ] **Add a `LICENSE` to `macarchy-dfr`**, then the org profile can say
      "Everything is MIT-licensed" again.

## A number to treat carefully

The star count was **5** at the start of this session and **12** when
re-checked before writing this page. That is recorded because it is what the
API returned, not because anything here caused it — none of the work above was
merged or announced in between. Re-measure the 14-day uniques a
week after the PRs land; that is the number worth trusting.
