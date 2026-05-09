# Setup Guide — Knowledge Vault

Follow these steps to set up your own knowledge vault from scratch. The whole process takes about 20–30 minutes.

---

## Step 1: Create Your Private GitHub Vault Repository

1. Go to [github.com](https://github.com) and log in (or create a free account)
2. Click **New repository** (top right `+` icon)
3. Name it something like `my-knowledge-vault` or `ai-memory`
4. Set it to **Private** — this is your personal data, keep it private
5. Tick **Add a README file**
6. Click **Create repository**

---

## Step 2: Set Up the Vault Structure

Inside your new repo, create the following files and folders. You can do this directly in the GitHub web interface (click **Add file → Create new file**) or by cloning and working locally.

### Required: `_index.md` (Master Map)

Create a file called `_index.md` in the root of your repo. This is the master index — your AI tools will always read this first to navigate the vault.

```markdown
# Knowledge Vault Index

## Projects
- [[project-one]] — Short description of what this project is
- [[project-two]] — Short description

## Knowledge
- [[knowledge]] — General learnings, frameworks, mental models

## Personal
- [[personal]] — Personal context, preferences, goals

## Last updated: [DATE]
```

Replace the example topics with your own. Each `[[topic]]` corresponds to a hub file and folder you'll create next.

### Required: Hub Files

For each major topic in your life/work, create:
- A **hub file** in the root: e.g., `project-one.md`
- A **folder** with the same name: e.g., `project-one/`

The hub file should be a short overview:

```markdown
# Project One

## What it is
One or two sentences describing this project.

## Current status
What stage is it at right now?

## Key decisions made
- Decision 1
- Decision 2

## Links to sub-notes
- [[project-one/notes-on-x]]
- [[project-one/decisions-log]]
```

Then inside the folder, create as many detailed notes as you need.

### Recommended starter structure:

```
your-vault/
├── _index.md
├── work.md           ← your job / research / career
├── work/
├── projects.md       ← active projects you're working on
├── projects/
├── knowledge.md      ← frameworks, learnings, book notes
├── knowledge/
└── personal.md       ← personal context AI tools should know about you
    personal/
```

---

## Step 3: Choose Your AI Tool(s)

### → Option A: Claude

Claude needs a **GitHub Personal Access Token (PAT)** to read and write your vault via the API.

#### 3A-1: Create a GitHub PAT

1. Go to GitHub → **Settings → Developer settings → Personal access tokens → Fine-grained tokens**
2. Click **Generate new token**
3. Set:
   - **Token name**: `claude-vault-access`
   - **Expiration**: 1 year (or no expiration if you prefer)
   - **Repository access**: Select your vault repo only
   - **Permissions → Contents**: Read and Write
4. Click **Generate token**
5. **Copy the token immediately** — you won't see it again

#### 3A-2: Edit the Claude Skill Files

Download all four files from the [`claude/`](./claude/) folder in this repo:
- `vault-read.md`
- `vault-write.md`
- `vault-sync.md`
- `vault-tidy.md`

Open each file and replace:
- `[YOUR_GITHUB_PAT]` → paste your PAT from the step above
- `[YOUR_GITHUB_USERNAME]` → your GitHub username (e.g., `janedoe`)
- `[YOUR_REPO_NAME]` → your vault repo name (e.g., `my-knowledge-vault`)

#### 3A-3: Upload to Claude

1. Go to [claude.ai](https://claude.ai) and open (or create) a **Project**
2. In the project, go to **Project Knowledge**
3. Upload each of the four `.md` files you just edited
4. Claude will now recognise the vault commands in your conversations

**Test it:** Type `vault-read` in a conversation inside that project. Claude should fetch your vault index.

---

### → Option B: ChatGPT

ChatGPT uses its **GitHub integration** (OAuth) — no PAT needed. You just need to connect your GitHub account once.

#### 3B-1: Connect GitHub to ChatGPT

1. Open ChatGPT and go to **Settings → Connected apps** (or **Integrations**)
2. Connect your GitHub account — ChatGPT will ask for OAuth permission
3. Grant access to your vault repo

#### 3B-2: Edit the ChatGPT Instruction File

Download [`chatgpt/knowledge-vault-instructions.md`](./chatgpt/knowledge-vault-instructions.md) from this repo.

Open it and replace:
- `[YOUR_GITHUB_USERNAME]` → your GitHub username
- `[YOUR_REPO_NAME]` → your vault repo name

#### 3B-3: Upload to a ChatGPT Project

1. In ChatGPT, create or open a **Project**
2. Go to the project's **Sources** or **Files** section
3. Upload `knowledge-vault-instructions.md`
4. ChatGPT will now reference these instructions when you use vault commands

**Test it:** Type `read the vault` in a conversation inside that project. ChatGPT should navigate to your repo and read the index.

---

## Step 4: (Optional) Visualise Your Vault in Obsidian

[Obsidian](https://obsidian.md/) is a free, open-source note-taking app that can open your vault as a local folder and display it as an interactive knowledge graph. It's entirely optional, but it makes the vault feel much more alive — you can see how your notes connect, spot gaps, and browse everything without an AI.

### 4-1: Clone your vault to your computer

Open your terminal and run:

```bash
git clone https://github.com/[YOUR_GITHUB_USERNAME]/[YOUR_REPO_NAME].git
```

This creates a local copy of your vault on your computer.

### 4-2: Open in Obsidian

1. Download Obsidian from [obsidian.md](https://obsidian.md/) — it's free and runs on Mac, Windows, Linux, iOS, and Android
2. Open Obsidian → click **Open folder as vault**
3. Select the folder you just cloned
4. Press `Ctrl/Cmd + G` to open **Graph View** — you'll see all your notes as connected nodes

### 4-3: Keep Obsidian in sync with GitHub

Your AI tools write to GitHub. To see those changes in Obsidian, pull the latest version:

```bash
# Navigate to your vault folder first
cd [YOUR_REPO_NAME]

# Pull the latest changes from GitHub (made by AI tools)
git pull origin main
```

If you also edit notes locally in Obsidian and want to push them back to GitHub:

```bash
git add .
git commit -m "local edits from Obsidian"
git push origin main
```

**Tip:** Install the **Obsidian Git** community plugin (free, inside Obsidian → Settings → Community plugins) to automate this. It can auto-pull and auto-push on a schedule, so syncing becomes invisible.

---

## Step 5: Populate Your Vault

Start by writing a few hub files. You don't need everything at once — the vault grows over time. A good first session:

1. Write `_index.md` with your 3–5 main topics
2. Write a hub file for each topic (just 5–10 lines each)
3. Ask your AI tool to `vault-read` — verify it can see everything
4. After any important AI conversation, ask it to `vault-write` the key insights

---

## Maintenance

| Task | How Often | Command |
|---|---|---|
| Write new knowledge | After any meaningful AI session | `vault-write` |
| Sync a project conversation | After a long working session | `vault-sync` |
| Tidy up the vault | Every few weeks when it gets messy | `vault-tidy` |

---

## Tips

- **Keep hub files short** — they should be scannable in 30 seconds. Detail goes in sub-files.
- **Use consistent naming** — lowercase, hyphens, no spaces (e.g., `market-research.md`)
- **Don't over-engineer it at the start** — start with 3 topics and expand
- **Let the AI tidy it** — `vault-tidy` will reorganise and update the index for you
- **Rotate your PAT annually** — GitHub PATs expire; update the skill files when you renew

---

## Security Notes

- Your vault repo should be **Private** — never public if it contains personal information
- Your GitHub PAT gives write access to the vault — treat it like a password
- The Claude skill files contain your PAT — do not share those files with anyone
- ChatGPT uses OAuth, which is safer (no token stored in files)

---

*Questions or issues? Open an issue in this repo or reach out on LinkedIn.*
