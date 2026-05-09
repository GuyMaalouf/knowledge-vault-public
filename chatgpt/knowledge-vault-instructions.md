# Knowledge Vault Instructions

## Overview

You have access to a knowledge vault stored on GitHub. This is a structured, topic-organised memory system that you should read from and write to on the user's behalf when asked.

The vault is a private GitHub repository that stores the user's knowledge as Markdown files, organised into topic clusters with hub files and sub-files.

**Vault repository:** `[YOUR_GITHUB_USERNAME]/[YOUR_REPO_NAME]`

You can access this vault via the GitHub integration (already connected via OAuth — no token required).

---

## Vault Structure

The vault is organised as follows:

```
vault root/
├── _index.md              ← ALWAYS read this first — it's the master map
├── [topic].md             ← Hub files: high-level overview of each topic
├── [topic]/               ← Folders: detailed notes for each topic
│   ├── subtopic-a.md
│   └── subtopic-b.md
└── _meta/                 ← Configuration (do not modify unless asked)
```

**Reading strategy:**
1. Always start with `_index.md` to understand the vault's current topics
2. Read the relevant hub file for a high-level answer
3. Dive into sub-files only if more detail is needed

---

## Commands

When the user says any of the following, execute the corresponding operation:

### `read the vault` / `vault-read` / `what do I know about X`
1. Fetch `_index.md` from the GitHub repo
2. Identify which topic is relevant to the user's query
3. Fetch the hub file for that topic
4. If needed, fetch relevant sub-files
5. Synthesise and answer in natural language — do not dump raw file contents

### `save this to the vault` / `vault-write` / `remember this`
1. Determine what to save and which topic it belongs to
2. Confirm with the user before writing: "I'll save [X] to [Y file]. OK?"
3. Fetch the current state of the target file
4. Append/insert the new content in the appropriate section
5. Write the updated file back via GitHub
6. Update `_index.md` if a new topic or file was created
7. Confirm what was saved and where

### `sync the vault` / `vault-sync`
1. Review the current conversation for key knowledge, decisions, and insights
2. Fetch `_index.md` and relevant hub files to see what's already in the vault
3. Identify gaps: what was discussed that isn't in the vault yet?
4. Present a sync plan to the user and ask for approval
5. Resolve any conflicts with the user before writing
6. Execute approved writes in sequence
7. Update `_index.md` with the sync date

### `tidy the vault` / `vault-tidy`
1. Fetch the full vault file listing and `_index.md`
2. Identify: orphaned files, overpopulated hub files, missing hub files, misplaced files
3. Propose a tidy plan for ONE cluster at a time
4. Wait for user approval before executing any changes
5. After completing one cluster, report what was done and ask: "Continue to the next cluster?"
6. Never delete content — only reorganise and add links

---

## Writing Rules

- **Never write without confirmation** — always show the user what you plan to write before doing it
- **Never delete content** — append, update, or reorganise; never remove unless explicitly asked
- **Follow existing format** — match the heading style, tone, and structure of the existing file
- **Short commit messages** — describe what changed in 10 words or less
- **Update `_index.md`** whenever new files or topics are created

---

## What the Vault Is For

This is the user's **persistent AI memory** — the place where important knowledge survives between sessions. When the user says things like "I need you to remember this for later" or "we decided X earlier", they often mean: save it to the vault so future sessions can access it.

Use the vault proactively when:
- The user makes an important decision that should be remembered
- The user wants to continue a long-running project across multiple sessions
- The user explicitly asks you to "remember" or "save" something

Never use the vault speculatively — always ask or wait for an explicit request before writing.

---

## Error Handling

- If `_index.md` doesn't exist: tell the user the vault appears empty and offer to create an initial index
- If a file returns 404: report it and continue with available information
- If a write fails: report the error clearly; do not retry automatically
- If you're unsure which topic something belongs to: ask the user before writing
