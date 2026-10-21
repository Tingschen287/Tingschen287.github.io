# 交接：Margin 个人网站

> 以下划线开头，GitHub Pages 不发布这个文件，只在仓库里可见。仓库是公开的，这里不写任何私密信息。

停点：2026-10-21，项目暂停（迁移系统），网站在线、可正常更新。

## 现状

| 项 | 值 |
|---|---|
| 网址 | https://tingschen287.github.io/ |
| 仓库 | https://github.com/Tingschen287/Tingschen287.github.io（公开，`main`） |
| Pages | 来源 `main` 分支 `/`（root），legacy 构建（Jekyll），强制 HTTPS |
| 最近提交 | `71be006` 外观切换改为三档图标按钮 |
| 本机位置（旧机） | `~/ai/05.code/github/Tingschen287/Tingschen287.github.io` |

## 已定的决策（不用再讨论）

- GitHub Pages 纯静态，一个统一的用户站点仓库，无构建、无 npm、无 CDN、无外部字体。
- 内容型个人网站，不是简历。分类只有 文章 / 项目 / 分享。
- 视觉：克制版苹果液态玻璃，主题色荧光绿 `#cdf545`（否决过苹果蓝、Anthropic 陶土橙）。
- 站名 Margin，称呼 Joy。联系邮箱和 GitHub 链接已填。
- 暂用 `github.io` 默认域名。
- 外观：默认跟随系统浅/深色；导航右侧图标按钮三档循环 自动◐ → 浅色☀ → 深色☾，手动选择存 `localStorage`，切回自动即跟随系统。

## 来历

设计在 claude.ai 网页会话里做的，最终版是 artifact「个人网站 内容型主页」（单页）。
网页会话交接文档里描述的拆分文件没有落到本机，所以本仓库是以该 artifact 为准拆出来的：
CSS 原样搬进 `assets/site.css`，模板和三个示例页是重写的，首页 `posts` 从 6 条减为 3 条（另 3 条指向不存在的页面）。

## 结构与机制

```
index.html                首页：搜索、最新卡片、按类型筛选；内容清单是 JS 数组 var posts=[...]
assets/site.css           全站共用样式（末尾追加了内容页排版和主题按钮样式）
posts/_template.html      文章/项目/分享通用模板（不发布）
posts/hello.html          示例文章
projects/tool/index.html  示例项目（字数统计小工具）
shares/tools.html         示例分享
```

- `posts` 每条：`{type, title, desc, date, url, tags}`，`type` 只能是 `文章`/`项目`/`分享`，按日期倒序渲染并自动出统计数字。
- 一律相对路径：根目录 `assets/site.css`，二级 `../`，三级 `../../`。不要改成 `/` 开头。
- 不要在根目录加 `.nojekyll`，否则模板等下划线文件会被公开。
- 主题切换脚本在每个页面内联（`<head>` 里一行提前应用已存的选择，避免闪烁；页尾一段负责按钮）。改它要五个页面一起改，模板也要改。

## 更新内容

1. 复制 `posts/_template.html`，改名，改标题、类型、日期、标签、正文。文章放 `posts/`，分享放 `shares/`，项目放 `projects/<名字>/index.html`（此时把模板里所有 `../` 改成 `../../`）。
2. 在 `index.html` 的 `posts` 数组加一行，`url` 填新页面路径。
3. `git add . && git commit -m "add: 标题" && git push`，一两分钟后线上生效。

## 验收方法

用 Playwright（无头 Chromium）跑过：所有页面 200、样式加载、首页 3 条内容、筛选/搜索/空结果、三档主题循环与记忆、子页跳转与返回首页、390px 手机宽度无横向溢出、控制台零报错。改了样式或脚本后建议照此再跑一遍。

## 新机器上继续

1. `gh auth login`（不要把 token 写进任何文件）。
2. 按本机约定克隆到 `05.code/github/Tingschen287/`：`git clone https://github.com/Tingschen287/Tingschen287.github.io`
3. 先读本文件。

## 后续可选（未开始，需用户决定）

- 用真实内容替换三个示例页（用户说先留着）。
- 自定义域名。
- 国内访问 `github.io` 可能不稳：可套 Cloudflare，或改用 Cloudflare Pages / Vercel。不要主动迁移。
- favicon、404 页、分享卡片 meta（OG 标签）目前都没有。
