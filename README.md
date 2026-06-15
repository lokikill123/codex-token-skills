# ⚡ Codex Token Skills

> 专为 **DeepSeek V4 Pro** 优化的 Codex skill，大幅降低 token 消耗并提升前缀缓存命中率。

[![Codex](https://img.shields.io/badge/Codex-CLI-blue)](https://github.com/openai/codex)
[![Skills](https://img.shields.io/badge/skills-2-green)]()
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

---

## 为什么需要？

DeepSeek V4 Pro 的前缀缓存机制：**系统提示词 + 上下文文件越稳定，缓存命中率越高**。如果你的 SKILL.md / AGENTS.md 频繁变动，每次对话都要重新处理全部上下文，浪费大量 token。

这两个 skill 的核心思路：

| 问题 | 解决方案 |
|------|---------|
| 上下文频繁变动 → 缓存失效 | Skill 文件写好后**冻结不动** |
| Codex 输出冗长 → token 浪费 | 强制**极简输出**，改完只说路径+done |
| 上下文压缩 → 丢失记忆 | 用文件做**持久记忆**，跨对话恢复 |

---

## Skill 列表

### 🔧 token-saver — 强制省 token

Smart 双模式：

- **简单任务**（修 bug、改配置、装东西）：禁止 preamble、禁止计划、禁止解释、禁止验证
- **复杂任务**（vibecoding、数据分析、架构设计）：允许简短交流，但严格控制

> 实测预计省 **60-80%** token。

### 🧠 memory — 全局持久记忆

上下文窗口被压缩后，下次对话自动从 `MEMORY.md` 恢复：
- 用户偏好与习惯
- 项目结构与关键路径
- 已做决策与反馈

> 每次仅消耗 `~800 token`，换来跨对话一致性。

---

## 快速安装

```bash
# 克隆到 Codex skills 目录
git clone https://github.com/lokikill123/codex-token-skills.git
cp -r codex-token-skills/skills/* ~/.codex/skills/

# 重启 Codex 即可生效
```

或通过 skill-installer：
```
install-skill --repo lokikill123/codex-token-skills --path skills/token-saver
install-skill --repo lokikill123/codex-token-skills --path skills/memory
```

---

## 缓存优化原理

```
[system prompt] + [AGENTS.md] + [各 skill SKILL.md] + [user message]
 ^^^^^^^^^^^^   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
 系统固定       这部分 skill 文件冻结不变 → 前缀缓存命中 → 省 50%+ token
```

**关键原则**：Skill 文件一次写定，永不修改。项目级动态内容放项目目录的 AGENTS.md，不放 skill 里。

---

## 搭配建议

- `token-saver` + `memory` 同时激活，效果最大化
- 在 `~/.codex/AGENTS.md` 中配置自动激活
- 如需 UI 开发配合，可搭配 mac-style-ui skill（见作者其他 repo）

---

## License

MIT
