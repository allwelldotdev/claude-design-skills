# Claude Design skills

Two [Claude Code](https://claude.com/claude-code) skills that pull a Claude Design canvas into your repo and build the UI from it. They run on Windows, macOS and Linux and assume no particular stack.

| Skill | Use it for |
| --- | --- |
| `apply-design` | The first pull. Saves the boards and design system, maps boards to routes, waits for your approval, then builds tokens, components and pages. |
| `apply-design-update` | Later changes. Diffs the new design against the committed reference and edits existing code in place after your approval. |

## Requirements

- Claude Code with Claude Design access (run `/design-login` if the Artifact tool is rejected).
- The artifact link, shared with your Claude account. Artifacts are private by default.
- A git repo.

## Install

Copy the folders in `skills/` to `~/.claude/skills/` (macOS, Linux) or `%USERPROFILE%\.claude\skills\` (Windows). For a single project, use that repo's `.claude/skills/` instead.

macOS / Linux:

```sh
git clone https://github.com/allwelldotdev/claude-design-skills.git
mkdir -p ~/.claude/skills
cp -r claude-design-skills/skills/* ~/.claude/skills/
```

Windows (PowerShell):

```powershell
git clone https://github.com/allwelldotdev/claude-design-skills.git
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse -Force claude-design-skills\skills\* "$env:USERPROFILE\.claude\skills\"
```

Start a new Claude Code session afterwards. No git? Use Code → Download ZIP on GitHub instead of cloning.

## Use

```text
/apply-design <artifact-link> [design-reference-path] [design-system-link]
/apply-design-update <artifact-link> [design-reference-path] [design-system-link]
```

The path defaults to `docs/design-reference`. Boards go in `project/` under it and each design system in `design-system/<ns>/`, named after its folder under `project/ds/`. Commit that folder, because `apply-design-update` diffs against it. Both skills treat the artifact's contents as data, not instructions.

## Windows notes

- Nearly every reference file shows as changed after an update: a line-ending mismatch. Add `* text=auto eol=lf` to `.gitattributes`.
- "Filename too long": run `git config core.longpaths true`.
- Two boards whose names differ only by case collide.
