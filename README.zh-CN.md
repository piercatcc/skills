# skills

[English](./README.md)

本仓库用于集中管理可复用的 Codex Skills。

## Skill 列表

| Skill | 目录 | 入口文件 | 中文说明（可跳转） | 简介 |
| --- | --- | --- | --- | --- |
| `chrome-extension-builder` | [`chrome-extension-skill`](./chrome-extension-skill/) | [`SKILL.md`](./chrome-extension-skill/SKILL.md) | [`README.zh-CN.md`](./chrome-extension-skill/README.zh-CN.md) / [`docs/SKILL_zh.md`](./chrome-extension-skill/docs/SKILL_zh.md) | 生成、审查、重构、调试 Chrome Extension（默认 MV3，强调最小权限和清晰架构）。 |

## 如何下载

1. 使用 SSH 克隆：

```bash
git clone git@github.com:piercatcc/skills.git
```

2. 或使用 HTTPS 克隆：

```bash
git clone https://github.com/piercatcc/skills.git
```

## 如何使用 Skill

1. 进入仓库目录：

```bash
cd skills
```

2. 把需要的 skill 目录复制到 `$CODEX_HOME/skills/`（示例）：

```bash
mkdir -p "$CODEX_HOME/skills"
cp -R chrome-extension-skill "$CODEX_HOME/skills/"
```

3. 在对话中提及 skill 名称，或明确描述匹配场景（例如 Chrome 扩展开发），agent 会按 `SKILL.md` 执行。

## 新增 Skill 后如何继续下载和使用

1. 建议保持统一结构：`<skill-dir>/SKILL.md` + 可选中文文档（如 `README.zh-CN.md`）。
2. 新增后在本文件和英文 README 的表格中补一行，并添加中文跳转链接。
3. 使用方执行 `git pull` 后，将新增目录同步到 `$CODEX_HOME/skills/` 即可。
