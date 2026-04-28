# 申请表填写内容

## 04 请描述你使用 Agent 或 AI 驱动构建的具体成果

我主要用 Agent/AI 构建了一套本地 AI 工具链自动化工作流，用来解决多平台 Agent 能力割裂、MCP 工具不可用、安装配置重复、历史记录和技能资产分散的问题。核心成果包括：1）把 Claude/Codex/Gemini/OpenCode 等客户端的 Skill 统一到同一份本地源，通过符号链接和同步脚本实现一次安装、多端可用，并做了桌面双击入口，降低日常使用成本；2）修复本地 MCP 工具接入问题，例如先判断工具实际是 stdio 还是 HTTP，再更新对应客户端配置，并通过 initialize/tools-list 做闭环验证；3）排查 macOS GUI 应用和终端环境不一致导致的 CLI 检测失败问题，用绝对路径 wrapper 提升稳定性；4）用 Agent 协助恢复 Claude Desktop 历史记录，定位真实会话数据、索引文件和应用数据目录之间的不一致；5）将 GitHub Release 应用安装、Skill 安装、微信日报/WeRSS 等本地工具调试纳入 Agent 辅助工作流。

这套工作流的核心逻辑是 Agent 先读取本机真实环境，再制定修复方案，再直接改配置、装依赖、跑验证。它包含长链推理、多客户端配置比对、MCP 协议排错、macOS GUI PATH 问题诊断、代理环境排查、Python 依赖兼容性处理等。它不是一次性的 Prompt，而是已经沉淀成可复用的本地自动化运维方式，能把原本需要反复手工迁移、查文档、改配置、验证日志的流程压缩成一次 Agent 协作任务。该工作流目前已成为我日常 AI 开发和本机工具运维的基础设施，后续会继续扩展到更多 MCP、个人知识库、微信内容处理和跨客户端 Agent 协作场景，因此对高 token plan 和稳定额度有持续需求。

## 05 使用证明与影响力证明

建议上传以下截图或录屏：

1. `~/Desktop/AI工具/` 桌面入口截图。
2. `~/.cc-switch/skills` 指向 `/Users/song/AI Skills` 的共享技能目录截图。
3. `~/.local/bin/sync-ai-skills status` 的终端输出截图。
4. Claude/Codex/Gemini/OpenCode 的 skills 目录符号链接截图。
5. MCP 修复相关截图，例如 stdio/HTTP 配置模板、initialize/tools-list 验证输出。
6. Claude/Codex 对话记录截图，展示 Agent 读环境、改配置、验证结果的过程。
7. GitHub 仓库地址或本仓库 README 页面截图。

链接栏可以填写本仓库地址。
