# Codex Token Skills

两个专为 **DeepSeek V4 Pro** 优化的 Codex skill，大幅降低 token 消耗并提升缓存命中率。

## 为什么需要？

DeepSeek V4 Pro 的缓存机制依赖前缀匹配。如果你的 SKILL.md / AGENTS.md 文件频繁变动，缓存会失效，每次对话都要重新处理，浪费大量 token。

这两个 skill 的设计原则：
- **内容冻结**：skill 文件写好后不再修改，最大化缓存命中
- **极简输出**：强制 Codex 减少废话，输出越短越省钱
- **持久记忆**：用文件替代上下文，跨对话保持记忆

## Skill 列表

### 1. token-saver

极致省 token。分两档：
- **简单任务**（修 bug、改配置）：禁止 preamble、禁止计划、禁止解释、改完只说路径+done
- **复杂任务**（vibecoding、数据分析）：允许简短交流，但仍严格控制

预计省 60-80% token。

### 2. memory

全局持久记忆。上下文被压缩后，下次对话自动从 MEMORY.md 恢复关键信息（偏好、项目结构、决策等）。

固定 ~800 token/次对话。

## 安装

```bash
# 复制到 Codex skills 目录
cp -r skills/* ~/.codex/skills/

# 重启 Codex
```

或通过 skill-installer 从 GitHub 安装。

## 缓存优化原理

DeepSeek V4 Pro 前缀缓存：
```
[system prompt] + [AGENTS.md] + [skill SKILL.md] + [user message]
                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
                   这部分不变 -> 缓存命中 -> 省 50%+ token
```

关键：skill 文件冻结后不再修改。项目级动态内容放项目 AGENTS.md，不放 skill 里。

## 搭配建议

- token-saver + memory 一起用，效果最好
- 在你的 ~/.codex/AGENTS.md 中加上自动激活规则
