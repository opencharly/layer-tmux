# AGENTS.md — layer-tmux

Standalone candy repo for the `tmux` layer — the terminal multiplexer used by
Charly's typed terminal provider. The candy lives in `charly.yml` at the repo
root: the `package:` section and the `check:` assertions. This repo carries **no
`skill:` entity**, so there is no owning `/charly-<family>:<name>` skill
projected into the marketplace corpus for it (recorded against
opencharly/opencharly#291).

Canonical files:

- `charly.yml` — the `tmux:` candy entity (the `package:` section and the
  `check:` assertions).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-infrastructure:tmux-layer` — the closest existing skill: the tmux
  candy's package and binary contract. There is no per-repo owning skill; the gap
  is recorded against opencharly/opencharly#291.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, service declarations). Load before editing any entity field or plan
  step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence. The detached
  session check (`new-session` → `has-session` → `kill-session`) is the live
  proof; keep it runnable on every distro arm.
- `tmux` ships the same package name on RPM, DEB, and PAC — no `package_map`
  needed.

## Modify this repo

- Edit the `tmux:` candy entity in `charly.yml`. A behaviour change belongs in
  the `plan:` as an observable `check:` step.
- Since this repo has no `skill:` entity, there is no projected skill body to
  mirror; the corpus gap is tracked in opencharly/opencharly#291.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
