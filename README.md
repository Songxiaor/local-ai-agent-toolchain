# Local AI Agent Toolchain Automation

License: MIT

这是一个本地 AI 工具链自动化工作流，用来解决多平台 Agent 能力割裂、MCP 工具不可用、安装配置重复、历史记录和技能资产分散的问题。

核心思路不是为每个客户端重复迁移配置，而是让 Agent 先读取本机真实环境，再制定修复方案，并直接完成配置、脚本、依赖和验证工作。

## 已落地成果

- 统一 Claude、Codex、Gemini、OpenCode 等客户端的 Skill 来源。
- 使用符号链接让多端共享同一份 Skill 目录，避免重复复制和迁移。
- 提供桌面双击入口，降低日常同步和检查成本。
- 修复本地 MCP 工具接入问题，例如区分 HTTP MCP 与 stdio MCP，并用 initialize/tools-list 验证。
- 排查 macOS GUI 应用无法识别 CLI 的 PATH 问题，使用绝对路径 wrapper 提高稳定性。
- 处理 Claude Desktop 历史记录恢复、会话索引与应用数据目录不一致的问题。
- 支持把 GitHub Release 应用、Skill、WeRSS/微信日报等本地工具纳入 Agent 辅助安装和排障流程。

## 架构

```text
~/.cc-switch/
  skills -> /Users/song/AI Skills
  claude-commands/

~/.local/bin/
  sync-ai-skills

~/.claude/skills        -> shared skill source
~/.codex/skills         -> shared skill source
~/.gemini/skills        -> shared skill source
~/.config/opencode/skills -> shared skill source

~/Desktop/AI工具/
  同步AI技能.command
  检查AI技能状态.command
```

## 工作流

1. Agent 检查本机真实目录和配置，例如 `~/.cc-switch`、`~/.claude`、`~/.codex`、`~/.gemini`、`~/.config/opencode`。
2. 选择一个共享 Skill 源作为事实标准。
3. 用同步脚本为不同客户端创建或更新符号链接。
4. 保留桌面 `.command` 入口，方便不用终端也能运行同步和状态检查。
5. 对 MCP 工具先确认传输类型，再分别按 stdio 或 HTTP 配置。
6. 每次修复后从目标客户端视角验证，而不是只看当前终端是否正常。

## 快速验证

```bash
~/.local/bin/sync-ai-skills status
ls -la ~/.cc-switch/skills
ls -la ~/.claude/skills ~/.codex/skills ~/.gemini/skills ~/.config/opencode/skills
```

如果需要验证 stdio MCP，可以使用类似方式手动初始化：

```bash
python3 ~/.local/bin/wbe_search_mcp.py
```

实际验证时应使用 MCP initialize 请求，确认服务器返回协议版本和能力列表。

## 证明材料

可截图位置见 [docs/evidence-guide.zh-CN.md](docs/evidence-guide.zh-CN.md)。

申请表可粘贴版本见 [docs/application-answer.zh-CN.md](docs/application-answer.zh-CN.md)。

脱敏工作流示例见 [examples/agent-maintenance-workflow.md](examples/agent-maintenance-workflow.md)。

## 参与维护

贡献和维护流程见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 安全说明

本仓库只放操作流程、脱敏模板和可复用脚本，不上传真实 token、OAuth 文件、私有数据库、完整应用日志或含账号隐私的配置文件。
