# Agent Maintenance Workflow Example

这个示例展示一次脱敏后的本地 AI Agent 工具链维护流程。它可以作为公开证据，说明仓库中的脚本、模板和操作方法如何被实际使用。

## 场景

用户同时使用 Claude、Codex、Gemini 和 OpenCode。某个 Skill 在 Claude 中可用，但 Codex 和 OpenCode 中不可见。目标是让多个客户端共享同一份 Skill 来源，并确认同步结果。

## 输入

```text
帮我检查为什么新安装的 Skill 只有 Claude 能看到，Codex 和 OpenCode 看不到。
```

## Agent 操作链

1. 检查共享源：

```bash
ls -la ~/.cc-switch
ls -la ~/.cc-switch/skills
```

2. 检查各客户端目标目录：

```bash
ls -la ~/.claude/skills
ls -la ~/.codex/skills
ls -la ~/.gemini/skills
ls -la ~/.config/opencode/skills
```

3. 运行同步脚本：

```bash
~/.local/bin/sync-ai-skills sync
```

4. 读取状态：

```bash
~/.local/bin/sync-ai-skills status
```

## 示例输出

```text
== /Users/example/.claude/skills ==
ok      /Users/example/.claude/skills/resume-session
ok      /Users/example/.claude/skills/web-access

== /Users/example/.codex/skills ==
ok      /Users/example/.codex/skills/resume-session
ok      /Users/example/.codex/skills/web-access

== /Users/example/.gemini/skills ==
ok      /Users/example/.gemini/skills/resume-session
ok      /Users/example/.gemini/skills/web-access

== /Users/example/.config/opencode/skills ==
ok      /Users/example/.config/opencode/skills/resume-session
ok      /Users/example/.config/opencode/skills/web-access
```

## 判断标准

- `ok` 表示目标客户端中的 Skill 链接正确指向共享源。
- `missing` 表示目标客户端缺少链接，可以重新运行 `sync`。
- `blocked` 表示目标位置已有真实目录或文件，脚本不会覆盖，需要人工确认迁移。
- `mismatch` 表示目标位置是符号链接，但指向了错误来源，需要检查旧配置。

## 可公开展示的证据

- `scripts/sync-ai-skills`：同步逻辑。
- `examples/shared-skills-layout.txt`：目录结构。
- `examples/codex-mcp-stdio-template.toml`：MCP stdio 配置模板。
- 本文件：一次脱敏的实际维护流程示例。

## 隐私处理

公开材料只展示目录结构、脚本行为和脱敏输出，不展示 token、OAuth 文件、私有聊天记录、真实企业路径或用户账号隐私。
