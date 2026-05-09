---
name: vault-read
description: Query your knowledge vault on GitHub. Triggers when the user says "vault-read", "what do I know about X", "check the vault for X", "look up X in my vault", or any question that might be answered by their personal knowledge base rather than general knowledge. Do NOT use for general questions — only when the query is about the user's personal notes, captured knowledge, or past decisions.
---

# vault-read

## Configuration

```
PAT="[YOUR_GITHUB_PAT]"
GITHUB_USERNAME="[YOUR_GITHUB_USERNAME]"
REPO_NAME="[YOUR_REPO_NAME]"
BASE_URL="https://api.github.com/repos/${GITHUB_USERNAME}/${REPO_NAME}/contents"
```

Replace the placeholders above before uploading this file:
- `[YOUR_GITHUB_PAT]` → your GitHub Personal Access Token (needs repo read permission)
- `[YOUR_GITHUB_USERNAME]` → your GitHub username
- `[YOUR_REPO_NAME]` → your vault repository name

---

## How to Execute vault-read

### Step 1 — Fetch the master index

```bash
curl -s \
  -H "Authorization: token $PAT" \
  -H "Accept: application/vnd.github.v3.raw" \
  "${BASE_URL}/_index.md"
```

Read the returned index in full. It is the map of everything in the vault.

### Step 2 — Identify the relevant topic

From the index, identify which hub file and folder are relevant to the user's query.

### Step 3 — Fetch the hub file

```bash
curl -s \
  -H "Authorization: token $PAT" \
  -H "Accept: application/vnd.github.v3.raw" \
  "${BASE_URL}/[TOPIC].md"
```

Replace `[TOPIC]` with the relevant hub file name (e.g., `startup`, `phd`, `knowledge`).

### Step 4 — Fetch detail files if needed

If the hub file points to sub-notes and the query needs deeper information:

```bash
curl -s \
  -H "Authorization: token $PAT" \
  -H "Accept: application/vnd.github.v3.raw" \
  "${BASE_URL}/[TOPIC]/[SUBFILE].md"
```

### Step 5 — Synthesise and respond

Synthesise what you found across the index, hub file, and any sub-files. Answer the user's query in natural language. Do not dump raw file contents — interpret and summarise.

---

## Notes

- Always read the index first — do not guess at file names
- If the index doesn't exist yet, tell the user the vault is empty and offer to help them set up `_index.md`
- If a file returns a 404, report it and continue with what's available
- Never invent vault contents — only report what the API actually returns
