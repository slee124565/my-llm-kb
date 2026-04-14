# Bespoke CLIs for Codex

Source: https://x.com/dotey/status/2042777337398210713
Author: 宝玉 @dotey
Captured at: 2026-04-12T07:28:02+08:00
GitHub issue: #22

OpenAI Codex 团队的 Nick Baumann 分享了一个他日常用 Codex 干活的心得：与其每次把一堆文档、日志、API 输出丢给 AI 去啃，不如给它造几个专用的命令行小工具。
他的逻辑很直接：MCP 连接器（比如 Slack、Linear、Sentry 这些）解决的是“能不能访问”的问题，但很多时候原始数据太大、太杂，AI 拿到手也处理得费劲。这时候更好的做法是把常用操作封装成一个带参数、输出 JSON、有帮助文档的 CLI 命令。Codex 本身就擅长用命令行，它会搜索、会加 flag 筛选、会把上一个命令的结果串到下一个命令里，不需要你教它怎么调。
他自己实际在用三个这样的 CLI：
【1】codex-threads：检索自己以前的 Codex 对话记录
Codex 的会话存档噪音很多，直接让 AI 读原始记录又慢又乱。他做了个工具在本地建索引，可以搜索、定位、读取历史会话。典型用法是找到一次做得好的对话，然后把里面的模式提炼成 skill（可复用的工作指南）。
【2】slack-cli：在 Slack 里精准找信息
场景很具体：有人在某个 Slack 频道讨论过一个技术决策的理由，你知道讨论过但找不到在哪。这个 CLI 可以让 Codex 搜索、定位到具体的消息链、拉上下文、引用关键消息。它底层还是走 Codex 的授权网关，权限没变，只是把交互方式从扔一坨聊天记录变成了一条命令拿到你要的东西。
【3】typefully-cli：写推文和排期发布
他用 Typefully 管理社交内容，但不想每次都让 Codex 重新学一遍 Typefully 的 API。于是让 Codex 读 API 文档，编译出一个 Rust 写的小 CLI，只暴露他常用的几个操作。配套的 skill 里还写了一条规矩：不许自动发布、排期或删除内容，除非他明确要求。
他把整个方法论总结成了一篇教程发到 OpenAI 开发者文档上，还配了一个 cli-creator skill 帮你用 Codex 自己造 CLI。
这个思路对用 Claude Code 的人同样适用。核心就一句话：如果你发现自己反复在给 AI 喂同一类乱糟糟的数据，那就别再解释了，给它造个命令。
Codex 团队还提供了一个 `cli-creator` skill，可配合这篇 OpenAI Developers 文档继续延伸：
https://developers.openai.com/codex/use-cases/agent-friendly-clis
