# Journal

## 2026-08-28

Bilal wants a personal assistant ("Jarvis") that helps with his work and
can operate a system on his behalf. Decision: don't build a separate
voice/OS-level agent — build on Claude Code itself, which already runs
commands, edits files, browses the web, and can be scheduled. Set up this
repo as Jarvis's persistent home:

- `CLAUDE.md` — persona and operating rules, auto-loaded for any session
  in this repo.
- `notes/tasks.md`, `notes/journal.md` — durable memory across sessions
  (sessions are ephemeral containers; this repo is not).

Next decisions pending with Bilal: (1) whether to add a daily scheduled
check-in (Routine), (2) whether to make the persona global via a proper
skill instead of scoped to this repo.
