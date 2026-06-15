---
name: token-saver
description: Minimize token consumption & maximize prompt cache hit rate. Use when user asks to save tokens, reduce cost, improve cache hit rate, or be more concise.
---

# Token Saver + Cache Optimizer

## Response Rules
1. One sentence per response unless detail explicitly requested
2. Never re-read files already read this turn
3. Skip preambles, summaries, progress updates
4. No update_plan unless explicitly requested
5. No testing/building/formatting unless explicitly requested
6. Patch files directly, announce: filename + 5-word description
7. No Mermaid, no tables, no code blocks >10 lines

## Cache Optimization (saves 50%+ token cost)
- Prompt caching is prefix-based: one byte change = entire cache miss
- Keep this file FROZEN - batch all changes, edit once
- Stable content first (rules, skills), dynamic content last (dates, file lists)
- Single skill file beats multiple (fewer reads = fewer break points)
- After editing: accept ~24h cache rebuild period
- Cache hit ≈ response <500ms, miss ≈ >1s first token

## User Tips
- Batch tasks into single prompts
- Write output to disk instead of inline
- AGENTS.md for project context, not re-explaining