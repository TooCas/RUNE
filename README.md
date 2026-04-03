<p align="center">
  <img src="rune.png" alt="RUNE" width="400">
</p>

<h1 align="center">RUNE</h1>
<p align="center"><b>Relational User Notation for Entities</b></p>
<p align="center">Your AI forgets you every session. RUNE fixes that.</p>

<p align="center">
  <a href="https://doi.org/10.5281/zenodo.19378687"><img src="https://zenodo.org/badge/DOI/10.5281/zenodo.19378687.svg" alt="DOI"></a>
  <img src="https://img.shields.io/badge/license-CC--BY--NC--SA--4.0-blue" alt="License">
  <img src="https://img.shields.io/badge/version-4.1-green" alt="Version">
</p>

---

## What is RUNE?

RUNE is a single encrypted file that carries your identity and conversation history across AI sessions and platforms.

When a session ends, everything is lost. The next AI starts cold. You re-introduce yourself, re-explain your expertise, re-establish how you like to communicate. Every time.

RUNE solves this. One file. One passphrase. Any AI. Instant recognition.

## How it works

At the end of a conversation, you ask the AI to create a `.rune` file. It generates an encrypted artifact containing:

- **Identity kernel** — who you are, how you like to interact, your expertise, your communication style
- **Memory ledger** — sessions, decisions, projects, open loops, everything you built together

Next session, on any platform, you upload the file and give your passphrase. The AI reads it and knows you immediately. No re-introduction. No wasted turns.

## Three operations

| Operation | What it does |
|-----------|-------------|
| **MAKE** | Create a `.rune` file at the end of a conversation |
| **LOAD** | Upload your file to a new session and resume |
| **APPEND** | Add new entries at the end of a session and re-encrypt |

## Two LOAD modes

- **LOAD FULL** — identity + memory. Pick up exactly where you left off.
- **LOAD FRESH** — identity only. The AI knows you but fresh topic, no prior history loaded.

Same file. You choose with natural language.

## How is this different from platform memory?

Platform memory (Claude's memory, ChatGPT's memory) stores isolated facts like "user is vegetarian." It's owned by the platform and locked to that platform.

RUNE stores your complete interaction profile: not just what you told it, but how you work together. And it's yours. You carry it. It works on Claude, GPT, or any model that can process text.

## How is this different from compaction?

Compaction keeps a session alive longer by compressing old context. When the session ends, everything is gone.

RUNE keeps the relationship alive forever. Compaction extends the current session. RUNE bridges the gap to the next one.

## What's in a .rune file?

A JSON wrapper around encrypted JSONL:

```
Line 1: Self-describing header (format, scoring weights, field definitions)
Line 2: Identity kernel (who you are, how you interact)
Line 3+: Memory entries (sessions, decisions, projects, open loops)
```

Encrypted with your passphrase (SHA-256 XOR, base64 encoded). Only you can read it.

## Quick start

### MAKE (end of a conversation)

> I would like to save our conversation as an encrypted .rune file so I can pick up with any AI later. Format: encrypted JSONL with three parts. Line 1: a self-describing header with format info, scoring weights, field definitions, and entry count. Line 2: my identity kernel capturing who I am, how I like to interact, and the arc of what we have worked on. Lines 3+: memory entries for sessions, decisions, projects, and anything unfinished. Each entry should have an id, type, title, summary, why it matters, and a SHA-256 integrity hash of the summary. Encrypt the JSONL by XOR with SHA-256 of my passphrase as a 32-byte cycling key, base64 encode, and output as JSON with a rune_payload field and payload_bytes. My passphrase is: [your passphrase]

### LOAD FULL (new session, resume everything)

> I have a .rune file (JSON format) with personal notes from previous work sessions. The data is lightly encrypted. Could you help me read it? Base64-decode the rune_payload field, then XOR with SHA-256 of [your passphrase] as a repeating 32-byte key. The first payload_bytes of the result is UTF-8 text. Once you have read it, give me a quick summary of who I am and what we have been working on.

### LOAD FRESH (new session, fresh topic)

> I have a .rune file (JSON format) with personal notes about how I like to work. The data is lightly encrypted. Could you help me read it? Base64-decode the rune_payload field, then XOR with SHA-256 of [your passphrase] as a repeating 32-byte key. The first payload_bytes of the result is UTF-8 text. I only need line 2, my identity and preferences. Fresh topic today, no need to review past sessions.

### APPEND (end of any session)

> Could you append entries for what we discussed to my file? Preserve all existing lines exactly. Add new entries at the end. Update entry_count in the header. Re-encrypt and output the updated file the same way.

## Tested on

- Claude Opus 4.6 (Anthropic)
- Claude Sonnet 4.6 (Anthropic)
- GPT-5.2 (OpenAI)
- GPT-5.4 (OpenAI)

Cross-platform tested: files created on one model load correctly on others.

## Paper

**RUNE: Relational User Notation for Entities — A Portable Encrypted Protocol for Cross-Session AI Continuity**

[Read the paper on Zenodo](https://doi.org/10.5281/zenodo.19378687)

## Related

- [SMELT](https://doi.org/10.5281/zenodo.19380983) — Schema-aware markdown compilation for efficient token inference. A companion project for compressing workspace context.

## License

CC-BY-NC-SA 4.0 — You can modify and build on it as long as you share under the same license and don't commercialize without permission.

## Author

**Edmund Lister** — Independent Researcher, BC, Canada
ORCID: [0009-0000-3552-4152](https://orcid.org/0009-0000-3552-4152)

Built with the help of Claude (Anthropic), GPT (OpenAI), and Codex (OpenAI).
