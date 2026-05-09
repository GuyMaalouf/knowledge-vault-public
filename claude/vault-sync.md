---
name: vault-sync
description: Sync the current AI project/conversation with the user's knowledge vault. Reviews recent conversations, compares against vault contents, identifies gaps and new knowledge, then writes approved updates in a batch. Triggers when the user says "vault-sync", "sync the vault", "update the vault with this project", or "sync my knowledge". Do NOT trigger speculatively — only when the user explicitly asks for a sync.
---

# vault-sync

## Configuration

```
PAT="[YOUR_GITHUB_PAT]"
GITHUB_USERNAME="[YOUR_GITHUB_USERNAME]"
REPO_NAME="[YOUR_REPO_NAME]"
BASE_URL="https://api.github.com/repos/${GITHUB_USERNAME}/${REPO_NAME}/contents"
```

Replace the placeholders above before uploading this file:
- `[YOUR_GITHUB_PAT]` → your GitHub Personal Access Token (needs repo read AND write permission)
- `[YOUR_GITHUB_USERNAME]` → your GitHub username
- `[YOUR_REPO_NAME]` → your vault repository name

---

## How to Execute vault-sync

### Step 1 — Review recent conversation context

Read the current conversation and any available project history. Identify:
- Key decisions made
- New knowledge or insights discussed
- Problems solved or approaches discovered
- Action items or next steps
- Any information the user referred to that isn't already in the vault

### Step 2 — Fetch the current vault state

```bash
curl -s \
  -H "Authorization: token $PAT" \
  -H "Accept: application/vnd.github.v3.raw" \
  "${BASE_URL}/_index.md"
```

For each relevant topic mentioned in the conversation, also fetch the corresponding hub file.

### Step 3 — Compare and identify gaps

Compare what you found in the conversation against what's in the vault. Identify:
- **New knowledge** — things discussed that aren't in the vault yet
- **Updates** — things that have changed since the vault was last written
- **Conflicts** — things in the vault that now seem outdated or contradicted

### Step 4 — Propose changes to the user

Present a clear summary of what you plan to sync:

```
Here's what I'd like to sync to the vault:

NEW — startup/customer-discovery.md
  • Interview 3 (May 2025): operator in France, pain point confirmed, willing to pay €75/month

UPDATE — startup.md
  • Current status: 3 interviews done → 5 interviews done
  • New key finding: schools are the better initial segment

CONFLICT — startup/mvp-notes.md
  • Vault says MVP scope is "assessment automation only"
  • But in today's conversation you decided to include a reporting module
  • Which is correct?

Shall I proceed with these changes? (You can also ask me to skip or modify any of them.)
```

Wait for explicit user approval before writing anything.

### Step 5 — Resolve conflicts

For each conflict, wait for the user to specify the correct version before writing.

### Step 6 — Execute approved writes

For each approved change, execute the write operation (same process as `vault-write`):
1. Fetch the current file + SHA
2. Compose the updated content
3. Encode to base64
4. PUT via GitHub API

### Step 7 — Update `_index.md`

Update the index with:
- Any new files created
- The last sync date

### Step 8 — Confirm completion

Report back:
- Number of files updated
- Number of new files created
- Any items skipped (and why)
- Confirm the sync date was recorded in the index

---

## Notes

- **Batch writes are fine** — you can write multiple files in sequence in a single sync session
- **Never write conflicts without resolution** — always ask the user which version is correct
- **Skipping is fine** — if something is trivial or already in the vault, skip it silently
- **Sync sessions can be long** — take your time to do it properly; accuracy matters more than speed
