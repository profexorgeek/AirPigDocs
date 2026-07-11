---
name: gitbook
description: Mandatory workflow for writing/editing AirPigDocs documentation from a GitHub issue — audience/voice rules, the agent-ready label gate, branch naming, sibling-repo research, and the needs-image marker for missing screenshots. Use whenever asked to write, edit, or plan documentation in this repo, or to work a specific issue number.
---

# GitBook Documentation Workflow

AirPigDocs is a GitBook-synced docs site (see `CLAUDE.md` for file structure and GitBook Markdown syntax). This skill covers how documentation work gets planned, written, and shipped as issues/PRs.

## Audience and Voice

The audience ranges from **teenagers with no coding experience** to **adult artists/designers with gamedev experience but no programming background**. Nobody in the target audience is assumed to be a developer. This matches how AirPig presents itself in `docs/README.md` ("no code!", "accessible for new game developers").

- Write in plain language. Avoid programming jargon (don't say "instantiate", "parameter", "null" — say "create", "setting", "empty").
- Explain game-dev and engine concepts the first time they appear on a page; lean on `docs/glossary.md` terms and link to it rather than re-defining a term differently in multiple places.
- Prefer short paragraphs and concrete examples over abstract descriptions. Screenshots/figures carry a lot of weight for this audience — see "Missing Images" below.
- Keep the friendly, encouraging tone already present in the existing pages (e.g. `docs/README.md`, `docs/creating-raw-content.md`) rather than a dry reference-manual tone.
- Document editor **usage** (what to click, what a field does) as the primary content. Only explain underlying engine mechanics when they change what the user should do in the editor (e.g. explaining biome tile layout because it affects how you author a biome PNG).

## Issue-Driven Workflow

Documentation work is tracked as GitHub issues on this repo's origin (`profexorgeek/AirPigDocs`), following the same lifecycle and label gate as the AirPig engine repo's `github-issues` skill:

1. **`agent-ready` label is the gate.** Only start writing/editing docs against issues labeled `agent-ready`. If asked to work an issue that isn't labeled, push back and ask for the label or a fleshed-out spec first — don't proceed unprompted. Reading/discussing/commenting on any issue is fine regardless of label.
2. **Fresh main** — `git checkout main && git pull` before branching.
3. **Branch name** — `YYYY-MM-issue-title-hint`, e.g. `2026-07-rig-editor-bone-tools`. Use the current year/month, not the issue's creation date. Always branch fresh off `main`; never stack on another issue's branch.
4. **Write the docs** — see "Writing the Page" below.
5. **Missing images** — see "Missing Images" below. If a page needs a screenshot you can't produce, add a `danger`-style hint placeholder and label the issue `needs-image` (create the label if it doesn't exist) instead of blocking the whole page on it.
6. **Implementation notes** — before opening the PR, comment on the issue summarizing what was written, which pages/sections changed, and any open questions (e.g. terminology decisions, missing screenshots).
7. **PR** — this is the expected final step, same as AirPig's workflow; no need to ask before opening it. Body includes `Fixes <full issue URL>` (via `gh issue view <n> --json url --jq .url`). Never merge it yourself. GitBook's Git Sync only publishes from the branch it's bound to (normally `main`) on merge — an open PR against a feature branch doesn't touch the live docs site, and GitBook adds its own preview-URL status check to the PR so you can sanity-check rendering before merging.
8. **Blocked** — if you can't complete the doc (e.g. the feature doesn't exist yet in the engine source, or behavior is ambiguous), comment describing the blocker rather than guessing or shipping speculative docs.

## Comment/Issue Attribution

Same convention as the AirPig engine repo's `github-issues` skill. Prefix the body of every issue, comment, or PR you post — in this repo or a sibling repo — with this header, then a blank line, then the content:

```
🤖 *Posted by Claude Code on behalf of @profexorgeek.*

<body>
```

Use a header, not a footer, so it's visible before scrolling.

## Researching Ground Truth

Docs must describe actual editor/engine behavior, not assumed behavior. Two sibling repos on disk are available for research (read-only — never edit them from this repo's context):

- **`../Airpig`** — the AirPig engine/editor source code. Use this to verify what a feature actually does, what fields/options exist, and correct terminology before documenting it. If the source contradicts an assumption in the issue, flag it in your implementation notes rather than silently documenting the source's behavior — the issue author may want the discrepancy fixed in-engine instead. **For anything UI-facing** (an editor screen, tool pane, panel, or field a user interacts with), use the `ui-research` skill to actually locate the layout/codebehind/viewmodel before describing it — don't guess at editor layout from the issue text alone.
- **`../CarrowMoor`** — an example game project used to dogfood AirPig. Use it for realistic example content (real biome files, item data, project folder layout) when a doc needs a concrete example rather than an invented one.

## Writing the Page

- Every page needs GitBook frontmatter (`description`, `icon`) — see `CLAUDE.md` for the exact format and existing hint/figure syntax.
- Add new pages to `docs/SUMMARY.md` or they won't appear in navigation.
- Use `docs/glossary.md` as the terminology source of truth; add new terms there when a doc introduces a concept not yet defined.
- If a page is only partially ready (e.g. one section done, another pending follow-up work), mark the unfinished section with a `WIP: ... coming soon!` line or hint, following the existing stub convention — don't leave it silently blank.

## Missing Images

When a page needs a screenshot or other image that you can't produce yourself, mark the spot inline so a human editor can find it, using the same `{% hint %}` danger style already used for WIP markers (see `docs/creating-raw-content.md`):

```
{% hint style="danger" %}
Screenshot needed: <brief description of what the image should show>
{% endhint %}
```

Then label the issue `needs-image` (in addition to, or in place of, closing it out) so it surfaces as needing a human follow-up pass. Don't let a missing screenshot block writing the rest of the page — write the text, mark the gap, move on.

## Follow-ups

If you notice a doc gap or inconsistency *within this repo* while working an issue, open a new placeholder issue here (`gh issue create`, unlabeled) rather than fixing it inline or only mentioning it in chat.

If instead you notice something that's actually an **engine** problem — a bug, unused code, confusing/undocumented behavior in the AirPig source that made it hard to write accurate docs — that belongs in the `AirPig` repo, not here. File it there instead of fixing it inline or just mentioning it in chat:

```
gh issue create --repo profexorgeek/Airpig --title "..." --body "🤖 *Posted by Claude Code on behalf of @profexorgeek.*

<body>"
```

Leave it unlabeled unless you're reasonably confident it's a genuine bug — undefined/broken behavior, or behavior that's "working as designed" but the design itself is broken. In that case it's fine to add the `bug` label; it's low-risk since the user can easily remove it or close the issue if you're wrong. Mention in your implementation notes on the AirPigDocs issue that you filed it, with a link. Don't try to fix engine code from this repo.
