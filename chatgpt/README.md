# ChatGPT Setup

ChatGPT accesses your vault via its **GitHub integration** — no Personal Access Token (PAT) required. Instead, you connect your GitHub account once via OAuth, and ChatGPT can read and write your vault directly.

---

## Prerequisites

- A ChatGPT Plus, Team, or Enterprise account (Projects and GitHub integration require a paid plan)
- Your vault repo created and set up (see [SETUP.md](../SETUP.md))
- GitHub integration connected in ChatGPT settings

---

## Before You Upload

Open `knowledge-vault-instructions.md` and replace:

| Placeholder | Replace with |
|---|---|
| `[YOUR_GITHUB_USERNAME]` | Your GitHub username |
| `[YOUR_REPO_NAME]` | Your vault repo name |

---

## How to Upload

1. In ChatGPT, open or create a **Project**
2. Go to the **Sources** section of the project
3. Upload `knowledge-vault-instructions.md`
4. Start a conversation and test with: `read the vault`

---

## How to Use

```
read the vault              → ChatGPT fetches your index and navigates to relevant topics
what do I know about X      → ChatGPT searches the vault for topic X
save this to the vault      → ChatGPT saves conversation insights to the vault
sync the vault              → ChatGPT reviews recent chats and syncs new knowledge
tidy the vault              → ChatGPT reorganises the vault structure
```

---

## Note on GitHub Integration

ChatGPT uses OAuth to access GitHub — it will ask for permission to read/write the specific repo. This is more secure than a PAT because:
- No token stored in files
- You can revoke access any time from GitHub settings
- Permissions are scoped through your GitHub account settings
