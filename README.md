# 🧠 Knowledge Vault — AI-Powered Shared Memory

> A topic-organised, graph-structured knowledge base that gives ChatGPT, Claude, and other AI tools a shared, persistent, navigable memory — stored on GitHub and owned by you.

---

## What Is the Knowledge Vault?

Most AI tools (ChatGPT, Claude, Gemini) have built-in memory, but it works like a flat text dump: everything stored in one long stream, hard to navigate, impossible to organise, and completely siloed between tools.

The **Knowledge Vault** is a different approach. It's a private GitHub repository that acts as your **external AI memory** — structured, topic-based, and accessible by any AI tool you connect it to.

Think of it as a **personal knowledge graph** that lives on GitHub, and your AI tools can read, write, and reorganise it on your behalf.

### Why It Works Better Than Default AI Memory

| Feature | Default AI Memory | Knowledge Vault |
|---|---|---|
| Structure | Flat text | Topic folders + hub files |
| Navigation | Linear search | Graph-like traversal |
| Cross-tool access | Siloed per tool | Shared across Claude, ChatGPT, etc. |
| You own the data | No | Yes (your GitHub repo) |
| Organised by project | No | Yes — each project has its own branch |
| Searchable | Partially | Fully, with an index file |
| Tidying/reorganising | Manual | AI-assisted (`vault-tidy`) |

---

## How It Works

The vault is a GitHub repo with a specific structure:

```
your-knowledge-vault/
├── _index.md              ← Master map of everything in the vault
├── _meta/                 ← Configuration & AI skill instructions
├── phd.md                 ← Hub file: overview of your PhD project
├── phd/                   ← Detail files: notes, papers, decisions
│   ├── methodology.md
│   └── literature.md
├── startup.md             ← Hub file: overview of your startup
├── startup/
│   ├── market-research.md
│   └── mvp-notes.md
├── knowledge.md           ← Hub file: general learnings
├── knowledge/
│   └── ...
└── personal.md            ← Hub file: personal context
```

**Hub files** (`phd.md`, `startup.md`, etc.) give AI tools a fast, high-level overview of each topic. When more detail is needed, the AI dives into the sub-files inside the corresponding folder. This two-level structure means:

- Fast answers: AI reads the hub first (cheap, quick)
- Deep answers: AI reads the sub-files when needed (richer context)
- Better recall: related notes stay together, not scattered in a flat text blob

---

## What You Can Do With It

Once set up, you can tell your AI tools to:

| Command | What It Does |
|---|---|
| `vault-read` | AI fetches the index and reads the relevant topic |
| `vault-write` | AI saves new notes, decisions, or learnings to the vault |
| `vault-sync` | AI reviews your recent conversations and syncs key info to the vault |
| `vault-tidy` | AI reorganises the vault into better clusters and updates the index |

These work in **Claude** (via project skill files) and **ChatGPT** (via project sources + GitHub integration).

---

## Who This Is For

Anyone who:
- Uses AI tools heavily for work, research, or creative projects
- Gets frustrated that AI tools "forget" everything between sessions
- Wants to maintain a long-running knowledge base across multiple AI tools
- Likes their information organised, not scattered
- Wants to own their AI memory — not have it locked inside a proprietary system

---

## Quick Start

1. **Create your private GitHub vault repo** → [See SETUP.md](./SETUP.md)
2. **Download the files for your AI tool(s)**:
   - Claude → [claude/](./claude/)
   - ChatGPT → [chatgpt/](./chatgpt/)
3. **Edit the placeholder fields** (your GitHub username, repo name, and — for Claude — your GitHub PAT)
4. **Upload to your AI tool** and start using it

---

## About This Project

This system was designed and built by [Guy Maalouf](https://www.linkedin.com/in/guymaalouf/) — a drone researcher and engineer who uses AI tools daily across research, writing, and product development. The vault is how he ensures nothing important gets lost across sessions, tools, or projects.

The files in this repo are the public templates. You can adapt them to your own topics, workflow, and AI tools.

---

## Files in This Repo

| File / Folder | Description |
|---|---|
| `README.md` | This file — overview of the system |
| `SETUP.md` | Step-by-step setup guide |
| `vault-structure/example-vault.md` | An example vault structure to copy |
| `claude/` | Claude skill files (vault-read, vault-write, vault-sync, vault-tidy) |
| `chatgpt/` | ChatGPT source instruction file |

---

*Built with obsession for organised thinking and AI-native workflows.*
