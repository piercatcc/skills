# Chrome Extension Builder Skill（中文说明）

这是一个面向 AI 的通用 Chrome 扩展开发 skill 分发包。

## 文件职责建议

- `SKILL.md`：给 agent / runtime 读取的主入口
- `README.md`：英文说明
- `README.zh-CN.md`：中文说明
- `docs/SKILL_zh.md`：给人阅读的中文对照版 skill 内容

## 推荐目录

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

## 关键原则

1. 不要把 `SKILL.md` 改名成 `SKILL_zh.md` 然后删掉原入口。
2. 真正作为 skill 入口的文件，建议始终保留为 `SKILL.md`。
3. 如果主要面向中文用户，可以：
   - 直接把 `SKILL.md` 写成中文；或
   - 保留英文 `name/description`，正文双语；再补一份中文 README。
4. `docs/SKILL_zh.md` 更适合作为“中文对照版”，方便他人阅读、转发和维护。

## 适用场景

- 从 0 生成一个 Chrome 扩展
- 给已有扩展做架构审查
- 把旧扩展迁移到 Manifest V3 风格
- 补全 popup / content script / service worker 分层
- 检查权限是否过大
- 排查脚本注入、消息通信、SPA 页面兼容问题

## 使用建议

把 `SKILL.md` 放进你的 skill 目录，把 `README.zh-CN.md` 和 `docs/SKILL_zh.md` 当作给中文用户的说明文档。
