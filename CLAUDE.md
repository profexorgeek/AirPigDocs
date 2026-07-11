# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This is the **AirPig Community Repo** — a documentation-only repository for the AirPig game engine, synced with GitBook. There is no source code, build system, or test suite. Content is authored in Markdown under `docs/` and published via GitBook.

AirPig is a niche pixel-art ARPG engine built around no-code editors (Rig, Variant, Item, Map, Animation editors) and 2D skeletal animation.

## Repository structure

- `docs/README.md` — the GitBook landing page ("AirPig Game Engine" overview), sets the icon and description for the doc site.
- `docs/SUMMARY.md` — GitBook's table of contents. **Any new page must be added here** or it won't appear in the published docs' navigation.
- `docs/*.md` — one file per doc topic (e.g. `map-editor.md`, `rig-editor.md`, `variant-editor.md`, `item-editor.md`, `animation-editor.md`, `creating-raw-content.md`, `glossary.md`).
- `docs/.gitbook/assets/` — images referenced by doc pages, named by timestamp (e.g. `2026-06-06-10-36-18.png`). Referenced via relative paths like `.gitbook/assets/<file>.png`.

## GitBook conventions

Each doc page uses GitBook-flavored Markdown:

- **Frontmatter** at the top of every page:
  ```yaml
  ---
  description: One-sentence summary shown in GitBook navigation/search.
  icon: <gitbook-icon-name>
  ---
  ```
- **Hints** — callout boxes using GitBook's hint syntax:
  ```
  {% hint style="success" %}
  ...
  {% endhint %}
  ```
  Other styles used: `warning`, `danger`.
- **Figures** — images with captions:
  ```
  <figure><img src=".gitbook/assets/<file>.png" alt=""><figcaption><p>Caption text</p></figcaption></figure>
  ```
- Unfinished pages are marked with a plain `WIP: ... coming soon!` line or wrapped in a `danger`/`warning` hint — several pages (`map-editor.md`, `animation-editor.md`, `variant-editor.md`, `item-editor.md`, `rig-editor.md`) are currently stubs. Preserve this WIP convention when a topic isn't ready to document in full.

## Domain terminology

`docs/glossary.md` is the canonical source of truth for AirPig-specific terms (Rig, Variant, Bone, Biome, Entity, Item, Gear, Keyframe, Navigation Mesh, etc.). When writing or editing docs, use terms consistently with the glossary's definitions, and update the glossary if introducing a new concept.

## Commit convention

Recent commit history shows this repo is primarily synced automatically from GitBook (commits like `GITBOOK-7: No subject`, `GITBOOK-6: Overall Layout`). Manual edits made here should still result in content that is valid GitBook Markdown, since changes may be round-tripped through GitBook's sync.
