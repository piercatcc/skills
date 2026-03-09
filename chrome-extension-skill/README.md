# Chrome Extension Builder Skill

This package is a distribution-friendly version of a general-purpose Chrome extension skill.

## Recommended file roles

- `SKILL.md`: machine-facing entry file used by the agent/runtime
- `README.md`: English human-facing guide
- `README.zh-CN.md`: Chinese human-facing guide
- `docs/SKILL_zh.md`: optional Chinese mirror of the skill content for readers

## Recommended structure

```text
chrome-extension-skill/
  SKILL.md
  README.md
  README.zh-CN.md
  docs/
    SKILL_zh.md
  examples/
    request-example.md
    output-example.md
    frontmatter-bilingual-example.md
  templates/
    minimal-manifest.json
    minimal-project-tree.txt
```

## Best practice

Keep `SKILL.md` as the entry file even if your audience is Chinese-speaking. If you want a Chinese version for readers, add `README.zh-CN.md` or `docs/SKILL_zh.md` instead of renaming the entry file.

## Typical use cases

- generate a new Chrome extension from scratch
- review extension architecture
- migrate MV2 to MV3-style structure
- tighten permissions
- debug popup/content/background separation
- debug scripting, messaging, or SPA compatibility issues
