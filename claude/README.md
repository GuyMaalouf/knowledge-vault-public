# Claude Skill Files

These four files are **Claude Project Knowledge** files. When uploaded to a Claude Project, they teach Claude how to read, write, organise, and sync your knowledge vault.

---

## Files in This Folder

| File | What it does |
|---|---|
| `vault-read.md` | Claude reads the vault — fetches the index and navigates to relevant topics |
| `vault-write.md` | Claude writes to the vault — creates or updates notes in the right place |
| `vault-sync.md` | Claude reviews recent conversations and syncs key knowledge to the vault |
| `vault-tidy.md` | Claude reorganises the vault — creates hub files, updates the index |

---

## Before You Upload

You must edit each file before uploading. Look for these placeholders and replace them:

| Placeholder | Replace with |
|---|---|
| `[YOUR_GITHUB_PAT]` | Your GitHub Personal Access Token (see [SETUP.md](../SETUP.md)) |
| `[YOUR_GITHUB_USERNAME]` | Your GitHub username (e.g., `janedoe`) |
| `[YOUR_REPO_NAME]` | Your vault repo name (e.g., `my-knowledge-vault`) |

> ⚠️ **Security**: These files will contain your PAT. Do not share them or make them public. The PAT is what gives Claude write access to your vault.

---

## How to Upload

1. Edit all four `.md` files with your details (see above)
2. Go to [claude.ai](https://claude.ai) → open or create a **Project**
3. Inside the project → **Project Knowledge → Add**
4. Upload each of the four `.md` files
5. Start a conversation in the project and test with: `vault-read`

---

## How to Use

Once uploaded, use natural language commands in any conversation inside that Claude Project:

```
vault-read                    → Claude reads the vault index and navigates to relevant topics
read the vault                → Same as above
what do I know about X        → Claude searches the vault for topic X

vault-write                   → Claude saves current conversation insights to the vault
save this to the vault        → Same as above
remember this                 → Same as above

vault-sync                    → Claude reviews recent project conversations and syncs to vault
sync the vault                → Same as above

vault-tidy                    → Claude reorganises the vault structure
tidy the vault                → Same as above
```

---

## Renewing Your PAT

GitHub PATs expire (typically after 1 year). When yours expires:
1. Generate a new PAT in GitHub settings (same permissions as before)
2. Open each of the four skill files
3. Replace the old PAT with the new one
4. Re-upload the files to your Claude Project
