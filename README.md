# Codex 技能迁移备份

从旧 Windows 电脑整理的用户技能、项目技能和全局规则。逐项来源、上游提交和恢复方式见 [SOURCES.md](SOURCES.md)。各技能沿用各自的许可证。

## 在新电脑恢复

1. 确认新机用户环境变量 `CODEX_HOME`。如果沿用旧机路径，目标目录为 `D:/CodexHome`。
2. 将 [skills/codex-home](skills/codex-home) 下各个技能的完整目录复制到 `$env:CODEX_HOME/skills`。
3. 将 [skills/user-agents](skills/user-agents) 下各个目录复制到 `$env:USERPROFILE/.agents/skills`。
4. 将根目录的 [AGENTS.md](AGENTS.md) 放到 `$env:CODEX_HOME/AGENTS.md`。新机已有全局规则时，先比较，再决定如何合并。
5. 迁移原小说项目后，将 [skills/project-novel](skills/project-novel) 下的两个技能放回项目的 `.codex/skills`。小说 agent TOML 随原小说项目的 `.codex/agents` 恢复。
6. 使用 [plugins/asu-skills](plugins/asu-skills) 作为 ASu Skills 的本地插件安装目录。系统技能与其他插件优先通过新机 Codex 和插件面板安装。需要单独获取的技能可在 [来源清单](SOURCES.md) 中找到。
7. 重新打开 Codex，在新机验证一个用户技能、全局规则和项目技能。依赖本机工具、额外运行时或账号连接的技能，按其原说明安装依赖或重新连接。

公开仓库用于迁移技能和全局规则。聊天记录、登录缓存和项目正文通过原来的离线备份恢复。
