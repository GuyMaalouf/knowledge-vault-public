---
name: vault-write
description: Save knowledge into the user's GitHub vault. Triggers when the user says "vault-write", "save this to the vault", "add to vault", "remember this", "capture this", or when the user explicitly wants to persist something from a conversation into long-term storage. Do NOT trigger speculatively — only write when the user explicitly asks.
---

# vault-write

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

## How to Execute vault-write

### Step 1 — Understand what to save

Before writing, clarify with the user:
- What is the key insight, decision, or knowledge to capture?
- Which topic does it belong to? (Check `_index.md` if unsure)
- Should it go in a hub file, an existing sub-file, or a new sub-file?

If the user says "save this" without specifying, propose a destination and ask for confirmation before writing.

### Step 2 — Fetch the current state of the target file

```bash
curl -s \
  -H "Authorization: token $PAT" \
  -H "Accept: application/vnd.github.v3+json" \
  "${BASE_URL}/[FILEPATH]"
```

This returns JSON. You need two things from it:
- `sha` — the current file's SHA (required for updates)
- `content` — the current file content (base64 encoded)

Decode the content:
```
echo "[BASE64_CONTENT]" | base64 --decode
```

If the file doesn't exist (404), you'll create it instead (no `sha` needed).

### Step 3 — Compose the new content

Take the decoded current content and append or insert the new information in the appropriate section. Follow the existing file's format and heading structure.

### Step 4 — Encode and write

Encode the updated content to base64:
```
echo -n "[NEW_CONTENT]" | base64
```

Write it back via the GitHub API:

```bash
curl -s -X PUT \
  -H "Authorization: token $PAT" \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Content-Type: application/json" \
  "${BASE_URL}/[FILEPATH]" \
  -d '{
    "message": "vault-write: [brief description of what was added]",
    "content": "[BASE64_ENCODED_NEW_CONTENT]",
    "sha": "[CURRENT_FILE_SHA]"
  }'
```

Omit the `"sha"` field if creating a new file.

### Step 5 — Update `_index.md` if needed

If you created a new topic or sub-file that isn't listed in the index, update `_index.md` to reference it. Follow the same fetch → edit → write process.

### Step 6 — Confirm with the user

Tell the user:
- What was saved
- Where it was saved (file path)
- Whether the index was updated

---

## Notes

- **Never write without user consent** — always confirm what you're about to write before executing
- **Preserve existing content** — append or insert; never overwrite unless the user explicitly asks to replace something
- **Commit messages should be descriptive** — `vault-write: added customer discovery synthesis to startup/customer-discovery.md`
- If the write fails (API error), report the error to the user and do not retry automatically
- Keep writes atomic — one logical change per write operation
