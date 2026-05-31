# 截图在哪里看

下面这些位置适合做申请表第 05 题的证明材料。截图前建议只展示路径、目录结构和命令输出，不展示 token、OAuth、cookie、私有数据库内容。

## 1. 桌面入口

Finder 打开：

```text
/Users/song/Desktop/AI工具
```

可以截图：

- `同步AI技能.command`
- `检查AI技能状态.command`
- 其他本地 AI 工作流启动器

## 2. 共享 Skill 源

Finder 打开：

```text
/Users/song/AI Skills
```

或终端运行：

```bash
ls -la ~/.cc-switch
ls -la ~/.cc-switch/skills
```

重点展示：

```text
~/.cc-switch/skills -> /Users/song/AI Skills
```

## 3. 同步脚本

Finder 打开：

```text
/Users/song/.local/bin
```

或终端运行：

```bash
ls -la ~/.local/bin/sync-ai-skills
~/.local/bin/sync-ai-skills status
```

截图重点是 `sync-ai-skills status` 输出里的 `ok`、`missing`、`blocked` 状态。

## 4. 多客户端 Skill 目录

终端运行：

```bash
ls -la ~/.claude/skills
ls -la ~/.codex/skills
ls -la ~/.gemini/skills
ls -la ~/.config/opencode/skills
```

截图重点是这些目录中的 Skill 项是否指向共享源。

## 5. MCP 配置和验证

不要截图真实 token。可截图脱敏模板：

```text
examples/codex-mcp-stdio-template.toml
```

如需展示真实验证，终端运行你实际 MCP 的 initialize/tools-list 测试，截图返回协议版本、工具列表或成功状态即可。

## 6. Claude Desktop 历史恢复证据

Finder 可以看：

```text
/Users/song/.claude/projects
/Users/song/Library/Application Support/Claude
```

截图时只展示目录层级，不展示聊天内容。

## 7. GitHub 仓库证明

本仓库推送后，直接把 GitHub 仓库首页截图上传即可。链接栏填写仓库 URL。

## 8. 脱敏工作流示例

如果不想上传本机截图，可以使用公开仓库里的脱敏示例作为辅助证明：

```text
examples/agent-maintenance-workflow.md
```

这个文件展示了从发现问题、检查本地路径、运行同步脚本到读取状态输出的完整维护链路，同时避免公开 token、私有路径和聊天记录。
