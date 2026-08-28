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

Follow-up: real voice recognition turned out not to work inside the
claude.ai artifact sandbox at all (it blocks the network call speech-to-
text needs, no matter mic permission). Fix: saved the same page as
`console/jarvis.html` in this repo and had him enable GitHub Pages
(Settings → Pages → deploy `claude/jarvis-pbifdm` branch, root folder) —
now live at https://bilalbutt2.github.io/M_B_K/console/jarvis.html,
where voice genuinely works since it's outside claude.ai's sandbox.
Tradeoff to remember: the GitHub Pages copy has no bridge back to Claude
or to connected accounts (no `sample`, no `mcp`), so live answers and
real Gmail only work on the claude.ai link, not the voice-capable one.
Both copies are kept in sync in `console/jarvis.html` going forward.

Added since: Always Listening (continuous recognition, auto-restarts,
pauses during Jarvis's own spoken replies to avoid a feedback loop) and
Clap to Wake (a volume-spike detector over the raw mic stream). Visual
pass toward a more authentic HUD (reticle corner brackets, tick-marked
ring, rotating radar sweep).

Bilal connected his Gmail account (claude.ai Settings → Connectors).
Wired real inbox lookup on the claude.ai link via the `mcp` capability
(`search_threads`, observed the real response shape firsthand before
coding against it, per the artifact-capabilities rule against guessing
tool shapes) — "check gmail" / "kiski email aayi hai" now opens Gmail
and reads back real sender + subject. Replaced the old per-site regex
routes with one NAME_TO_KEY/KEY_INFO dispatcher that recognizes a
system by name in English or Roman Urdu and infers open-vs-close from
whether "close"/"band" appears anywhere in the sentence, instead of
requiring an exact phrase — this is what was actually breaking his
"gmail band karo" requests before (no close handling existed at all, so
it fell through to a web-search fallback that looked like "opening
something random"). Open-ended questions via `sample` now get a system
prompt telling Claude to reply in whichever language/mix Bilal used.
