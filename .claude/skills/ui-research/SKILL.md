---
name: ui-research
description: How to locate the actual editor UI implementation for a named feature (e.g. "Rig Editor", "Item Editor", "Map Editor") in the sibling AirPig repo, so docs describe what the UI really does rather than an assumed/guessed layout. Use whenever documenting or fact-checking any AirPig editor screen, tool pane, or panel — before writing about buttons, fields, options, or workflow steps a user would interact with.
---

# UI Research

The AirPig editor's actual interface — the buttons, fields, and panels a user sees — is defined by three layers of source in the sibling `../Airpig` repo, not by anything in this repo. When documenting editor usage, go find the real implementation rather than describing it from memory or the issue text alone. This skill is about the *method* for finding it, since exact filenames will drift as the engine evolves — don't treat any specific path below as guaranteed current; verify with `Glob`/`Grep` first.

## The Layers, Per UI Element

1. **Layout** — a Gum XML file, `*.gucx` (occasionally `*.ganx`), under `Airpig.Engine/Content/Gum/Components/`. Defines the visual structure: what's on screen and how it's arranged.
2. **Codebehind** — a C# class under `Airpig.Engine/UI/`, in a subfolder mirroring the `.gucx` location. Wires the layout's named elements to bindings and event handlers — this tells you what a field actually *does*, and what values/options it accepts.
3. **ViewModel** — the data/behavior backing the codebehind. Often defined **in the same .cs file** as the codebehind (e.g. a `FooToolPaneModel : ViewModel` class living right in `FooToolPane.cs`), not in a separate folder — don't assume a dedicated ViewModels directory exists. This is where to look for validation rules, computed/derived values, and what happens when the user changes something.

Both `.gucx` and codebehind live in matching subfolders, one of: `Controls/`, `Elements/`, `Viewers/`, `ToolPanes/`, `IShowableMenus/`, `Screens/`.

## The Hierarchy

The highest-order component is a **Screen** (`Components/Screens/`, codebehind `UI/Screens/`). The main editor screen owns one **ToolPane** per editing mode (`Components/ToolPanes/`, codebehind `UI/ToolPanes/`), each of which typically manages its own ViewModel and composes smaller **Viewers**/**Controls** for individual fields and sub-panels.

So: a doc page about a top-level editor (Rig Editor, Item Editor, Map Editor, Variant Editor, Animation Editor) almost always corresponds to one **ToolPane**. A doc section about one specific field or sub-panel within that editor corresponds to a **Viewer** or **Control** the ToolPane composes.

## Mapping a Doc Topic to Source

1. Guess the ToolPane name from the doc topic and confirm with `Glob`: `Airpig.Engine/Content/Gum/Components/ToolPanes/*.gucx`. **Don't assume the doc-facing name matches the source name** — check the "Known Code ↔ User-Facing Term Map" below first, since AirPig's source and docs sometimes use different words for the same concept on purpose (see "Terminology" section).
2. Read the `.gucx` to see the actual layout and every named element.
3. Read the matching codebehind (`UI/ToolPanes/<Name>.cs`) to see what each element is bound to, what it does on interaction, and what its ViewModel class is called.
4. If the ViewModel isn't defined in that same file, `Grep` for its class name to find where it lives.
5. For a sub-panel or specific field, repeat the same three-layer lookup against the `Viewers/` or `Controls/` folder instead of `ToolPanes/`.

## Terminology: Code Names vs. User-Facing Names

Internal code identifiers (class names, file names, C# properties, XML instance names) frequently won't match the term docs use, and **that's fine — it's not a bug, and it's not worth the risk/cost of renaming code just to match docs.** Never file an issue and never suggest a code rename purely because a class or file name differs from the doc term.

What actually has to stay consistent is the **user-facing surface**: `docs/glossary.md`, and the real text the running editor displays — button labels, tooltips, menu titles, i.e. the literal strings in a `.gucx`'s `<Value>` elements for `Text`/`Tooltip`-type properties. (Not instance names or property names in that same file — those are still internal identifiers, just XML instead of C#.)

- When researching a feature, note the code-side identifier if it's useful for finding things again fast, but **write the doc using whatever term the glossary establishes**, which is normally whatever the live UI actually displays. Add new rows to the map below when you find a new mismatch worth remembering.
- If the glossary doesn't yet have a term for something you're documenting, add it — the glossary should be the single source of truth for user-facing terminology, and doc pages should stay consistent with it.
- **Only** raise a follow-up/cross-repo issue when the *live UI text itself* is inconsistent — e.g. two different tooltips/labels in the running editor use different words for what should be one concept, or a label directly contradicts the glossary's established term. A code identifier differing from the doc term is never, by itself, a reason to file anything.
- **Exception — deliberate terminology migrations.** Occasionally the user decides to retire a term outright (see "Item" and "Polygon" in the map below) even though the live UI hasn't caught up yet. In that case the glossary leads and the live UI is expected to follow — don't treat the live UI still saying the old term as a new inconsistency to flag; it's already tracked by a checklist issue filed in `AirPig` (linked in the map). Just don't introduce the retired term in new docs.

### Known Code ↔ User-Facing Term Map

Keep this list growing as new mismatches are found — it saves re-deriving the same mapping on every future doc pass.

| User-facing term (docs/glossary) | Code identifiers | Notes |
|---|---|---|
| Item | `Models/Gear/*`, `GearToolPane`, `GearLibrary`, `GearChooser` | **Deliberate migration** (AirPigDocs #8): "Gear" is retired in favor of "Item" everywhere — glossary, docs, and eventually the live UI (checklist filed in `AirPig`, linked from #8's implementation notes). Code identifiers still say Gear; not worth renaming. Don't reintroduce "Gear" in new docs, even though some live tooltips/labels still say it. |
| Polygon (a polygon's points are **Node**s) | `PolygonModel`, `PolygonListViewer` (code is inconsistent internally — `ZoneBehavior`, `ZonePropertiesViewer` say "Zone") | **Deliberate migration** (AirPigDocs #9): "Zone" is retired in favor of "Polygon" — it was only ever used inconsistently. Glossary/docs, and eventually the live UI (checklist filed in `AirPig`, linked from #9's implementation notes). Don't reintroduce "Zone" in new docs, even though some live tooltips/labels still say it. |

## When Source Contradicts the Doc Issue

This is about **behavior**, not naming — see "Terminology" above for naming. If what you find in source disagrees with a behavioral assumption in the GitHub issue you're working (a field that doesn't exist, different behavior than described), don't silently document the source's behavior as if it were always known — flag the discrepancy in your implementation notes per the `gitbook` skill, since the issue author may want it fixed in-engine rather than just documented as-is.
