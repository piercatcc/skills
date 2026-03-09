# Chrome Extension Builder Skill（中文对照版）

> 说明：本文件用于给人阅读和分发。真正的入口文件仍然应当是根目录下的 `SKILL.md`。

## 角色定位

这个 skill 用来设计、生成、审查、重构或调试通用的 Chrome 扩展。它应当把用户的自然语言需求转成一个可运行、结构清晰、权限最小、方便调试的 Chrome Extension 项目。

默认使用 **Manifest V3**。

## 这个 skill 要做什么

1. 把想法转成 Chrome 扩展技术方案。
2. 判断正确的模块分层：
   - `action` / popup
   - `background` service worker
   - `content_scripts`
   - `options_page` / `options_ui`
   - `side_panel`
   - 必要时的 injected page script / bridge
3. 选择最小权限和最小站点授权范围。
4. 生成可运行的项目结构。
5. 生成核心文件和代码。
6. 解释限制、取舍和常见坑。
7. 提供本地加载、调试和打包说明。
8. 审查已有扩展，或迁移到 MV3 风格。

## 默认假设

除非用户明确要求，否则默认：

- 使用 **Manifest V3**
- 简单和中等复杂度扩展优先使用原生 HTML/CSS/JavaScript
- 只有在 UI 和状态复杂时才建议 React/Vite
- 权限最小化
- 能用 `activeTab` 就不要申请过宽的 host 权限
- 不默认使用 `<all_urls>`
- 不把核心业务逻辑全部塞进 popup
- 把 background service worker 视为临时唤醒的，不当成常驻进程
- 持久配置优先放在 `chrome.storage.local`
- 不依赖远程托管的可执行代码
- 如果用户用中文提问，则默认用中文输出

## 工作流程

### 1. 重述需求

把用户的话整理成工程需求，明确：

- 主要目标
- 触发方式
- 作用网站范围
- UI 形态
- 数据来源
- 数据去向
- 是否依赖外部 API 或后端
- 是新建、修改、审查、迁移还是排错

### 2. 决定架构

按职责分层：

- **Popup / action UI**：短交互、一键操作、状态展示
- **Background service worker**：事件监听、alarms、context menus、tab 生命周期、统一协调
- **Content script**：DOM 读取和修改、页面浮层、抓取页面内容、监听页面变化
- **Options page**：长期配置项
- **Side panel**：浏览过程中的持续陪伴式界面
- **Injected page script / bridge**：当必须访问页面上下文对象时才使用

### 3. 权限最小化

先决定权限，再写代码。对每个权限都解释用途。

### 4. 先给目录树

只输出真正需要的模块，不要无意义堆文件。

### 5. 再给 MVP 代码

要求：

- `manifest.json` 必须有效
- 模块职责清楚
- 该有的消息通信要有
- 需要基础错误处理
- 需要时给简短注释

### 6. 解释 Chrome 扩展限制

需要主动提醒：

- service worker 生命周期不是常驻
- content script 和页面脚本运行在不同上下文
- SPA 页面可能需要监听路由变化或 `MutationObserver`
- iframe / Shadow DOM 可能需要额外适配
- 网络访问能力和权限、执行上下文有关
- popup 不是长期运行容器

### 7. 给出本地调试步骤

包括：

- 打开 `chrome://extensions`
- 开启开发者模式
- Load unpacked
- 查看 service worker 日志
- 在目标页面检查 content script 效果
- 修改后重新 reload 扩展

## 输出格式建议

```md
## 需求理解
## 关键假设
## 推荐架构
## 所需权限与原因
## 文件树
## 核心实现
## 安装与调试步骤
## 限制与风险
## 可选后续增强
```
