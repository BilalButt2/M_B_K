# Jarvis memory

This directory is Jarvis's persistent memory. Claude Code sessions are
ephemeral containers — nothing survives in them once the session ends
unless it's committed here.

- **tasks.md** — the standing task list. Three sections: Inbox (new,
  untriaged), In Progress, Done. Keep entries one line each; link out to
  detail (an artifact, a PR, a doc) instead of writing detail here.
- **journal.md** — a dated append-only log. One entry per session that did
  something worth remembering: what happened, what was decided, and why —
  not a transcript.

Update both before ending a session that changed anything. A future
session (yours or Bilal's) should be able to read these two files and
know where things stand without re-reading the whole conversation history.
