---
name: vault-tidy
description: Reorganise the user's knowledge vault into well-structured topic clusters with hub files, for better navigation and AI retrieval efficiency. Triggers when the user says "vault-tidy", "tidy the vault", "tidy up my vault", "reorganise my vault", or "clean up the vault". Do NOT trigger speculatively — only when the user explicitly asks for a tidy. Preserves all content — only reorganises structure and adds links.
---

# vault-tidy

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

## How to Execute vault-tidy

> ⚠️ **vault-tidy is self-iterating.** Process one cluster at a time, report what was done, then ask the user "Continue to the next cluster?" before proceeding. Never chain multiple clusters without explicit consent. Stop when all clusters are tidy or when the user says stop.

### Step 1 — Inventory the vault

Fetch the full vault contents listing:

```bash
curl -s \
  -H "Authorization: token $PAT" \
  -H "Accept: application/vnd.github.v3+json" \
  "${BASE_URL}/"
```

Also fetch `_index.md`:

```bash
curl -s \
  -H "Authorization: token $PAT" \
  -H "Accept: application/vnd.github.v3.raw" \
  "${BASE_URL}/_index.md"
```

List all files and folders you find. Identify:
- Orphaned files (files not referenced in the index)
- Overpopulated hub files (hub files that have too many sub-topics to stay clear)
- Empty folders (folders with no files)
- Misplaced files (files that belong in a different topic cluster)
- Missing hub files (a folder exists but no corresponding `.md` hub file)

### Step 2 — Propose one cluster's tidy plan

Choose the messiest cluster and present a plan:

```
I'll start with the `startup` cluster. Here's what I propose:

1. SPLIT: startup.md is getting long — I'll move "decisions log" to startup/decisions-log.md and link it from the hub
2. MOVE: customer-discovery-interview-3.md is in the root — I'll move it to startup/customer-discovery.md
3. CREATE: startup/decisions-log.md doesn't exist yet — I'll create it from the content currently in startup.md
4. UPDATE: _index.md → add the new link under [[startup]]

No content will be deleted. All moves are additions + links.

Shall I proceed with the startup cluster?
```

Wait for the user to say yes (or modify the plan) before executing.

### Step 3 — Execute the approved tidy operations

For each approved operation:

**Creating a new file:**
```bash
curl -s -X PUT \
  -H "Authorization: token $PAT" \
  -H "Content-Type: application/json" \
  "${BASE_URL}/[FILEPATH]" \
  -d '{
    "message": "vault-tidy: created [FILEPATH]",
    "content": "[BASE64_ENCODED_CONTENT]"
  }'
```

**Updating an existing file (fetch SHA first, then PUT with sha):**
```bash
# First fetch SHA
curl -s -H "Authorization: token $PAT" "${BASE_URL}/[FILEPATH]" | python3 -c "import sys,json; print(json.load(sys.stdin)['sha'])"

# Then write
curl -s -X PUT \
  -H "Authorization: token $PAT" \
  -H "Content-Type: application/json" \
  "${BASE_URL}/[FILEPATH]" \
  -d '{
    "message": "vault-tidy: updated [FILEPATH]",
    "content": "[BASE64_ENCODED_CONTENT]",
    "sha": "[FILE_SHA]"
  }'
```

### Step 4 — Update `_index.md`

After completing each cluster, update `_index.md` to reflect:
- New files added
- New links between hub files and sub-files
- Updated `Last tidy` date

### Step 5 — Report and ask to continue

After each cluster:

```
✅ Startup cluster tidy complete.

Done:
- Moved decisions content to startup/decisions-log.md
- Linked from startup.md
- Updated _index.md

Next up: knowledge cluster (3 orphaned notes, 1 missing hub file link).
Continue?
```

### Stop conditions

Stop when:
- All clusters have been reviewed and tidied
- The index accurately reflects the vault's full structure
- No orphaned files remain
- All hub files exist for folders that have content
- The user explicitly says to stop

---

## Notes

- **Never delete content** — if something seems redundant, move it to an archive section, not the bin
- **Ask before merging** — if two notes cover the same thing, propose the merge and wait for approval
- **Small steps** — one cluster per session is intentional; it keeps the user in control
- **Commit messages** should say `vault-tidy: [what changed]` for easy git history reading
