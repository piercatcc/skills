# skills

[简体中文](./README.zh-CN.md)

This repository contains reusable Codex skills.

## Skill List

| Skill | Directory | Entry File | Chinese Docs (Jump Links) | Summary |
| --- | --- | --- | --- | --- |
| `chrome-extension-builder` | [`chrome-extension-skill`](./chrome-extension-skill/) | [`SKILL.md`](./chrome-extension-skill/SKILL.md) | [`README.zh-CN.md`](./chrome-extension-skill/README.zh-CN.md) / [`docs/SKILL_zh.md`](./chrome-extension-skill/docs/SKILL_zh.md) | Build, review, refactor, and debug Chrome extensions (MV3-first, minimal permissions, clear architecture). |

## Download

1. Clone with SSH:

```bash
git clone git@github.com:piercatcc/skills.git
```

2. Or clone with HTTPS:

```bash
git clone https://github.com/piercatcc/skills.git
```

## How To Use A Skill

1. Enter the repository:

```bash
cd skills
```

2. Copy the required skill folder into `$CODEX_HOME/skills/` (example):

```bash
mkdir -p "$CODEX_HOME/skills"
cp -R chrome-extension-skill "$CODEX_HOME/skills/"
```

3. In your prompt, mention the skill name or clearly describe the matching task (for example, Chrome extension development), then the agent will follow `SKILL.md`.

## When New Skills Are Added

1. Keep a consistent structure: `<skill-dir>/SKILL.md` plus optional Chinese docs (for example `README.zh-CN.md`).
2. Add one new row in this README table and include Chinese jump links.
3. Users can run `git pull` and sync the new skill directory into `$CODEX_HOME/skills/`.
