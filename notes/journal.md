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

Follow-up same day: Bilal chose "make it global" and also asked for an
Iron-Man-style interactive Jarvis UI.

- Packaged the persona/memory rules from `CLAUDE.md` into a proper
  account-level skill (`jarvis`, description tuned to trigger on "hey
  jarvis" / personal-assistant requests without firing on unrelated repo
  coding questions) and sent him the `.skill` file to install — skipped
  the full skill-creator eval/benchmark pipeline since this is a one-off
  personal skill, not a product with many users.
- Built and published a voice-controlled "Jarvis" HUD console as a Claude
  Artifact: https://claude.ai/code/artifact/888679e3-0c48-4c24-8f06-52707f2a44c8
  — speech in/out (Web Speech API), a command router that opens real
  tools (Gmail, Calendar, this repo's task board, his FFC Delivery Desk
  board, GitHub, web search) in new tabs, and falls back to asking Claude
  directly (the `sample` runtime capability) for anything open-ended.
  Scope boundary communicated to him explicitly: this is a browser page,
  so it can open apps and answer questions, but it cannot reach into his
  OS or click around inside other apps — that stays inside Claude Code
  sessions.
