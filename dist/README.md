# Prebuilt skills (dist)

Precompiled, ready-to-install skill packages. Each `.skill` is a zip archive of the skill directory.

| File | Skill | Contents |
|------|-------|----------|
| `strategy-os.skill` | `strategy-os` | 6-phase engagement orchestrator + 4 method playbooks |
| `market-research.skill` | `market-research` | MBB pyramid research with verification gate + PPTX |

## Install

A `.skill` file is a zip archive. Extract it into a Claude Code skills directory:

```bash
# Personal (all projects) — unzip treats .skill as a zip:
unzip strategy-os.skill -d ~/.claude/skills/
unzip market-research.skill -d ~/.claude/skills/
```

Then restart Claude Code. Install both for the full Strategy OS engagement (`strategy-os` hands off to `market-research` for Phase 2).

> Rebuild: `python3 ~/.claude/commands/skills/scripts/package_skill.py <skill-dir> dist` then rename the resulting `.zip` to `.skill`.
