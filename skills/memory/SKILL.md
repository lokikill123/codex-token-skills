---
name: memory
description: >-
  Persistent global memory across conversations. Read memory file at start of
  every conversation, write important context during conversation so it
  survives context compression. Use ALWAYS. Triggered automatically.
---

# Memory

## Memory File
C:\Users\lokik\.codex\MEMORY.md

## On Conversation Start (MUST DO FIRST)
Read the memory file. If it doesn't exist, create empty and note "no prior memory".

## During Conversation (MUST DO)
When any of these happen, APPEND to MEMORY.md immediately:
- User states a preference or habit
- A project is created or its structure changes significantly
- User gives feedback about your behavior
- A decision is made that affects future work
- Skills are installed or modified
- Important file paths or configs are established

## Format
Append entries as:
`
## YYYY-MM-DD
- [category] fact
`

Categories: pref (preference), proj (project), skill (skill), cfg (config), decision

## Rules
- Append only. Never delete old entries.
- One line per fact. Be specific.
- If user contradicts old memory, append correction, don't delete old.
- Don't write trivial/temporary facts.
- Max 20 most recent entries. Archive older to MEMORY_archive.md.