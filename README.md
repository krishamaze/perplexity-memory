# 🧠 perplexity-memory

> Stateful memory for Perplexity AI using GitHub as a persistent graph store.

## Structure
```
perplexity-memory/
├── INDEX.md              ← Graph root, session loop instructions
├── LOOP.md               ← Detailed protocol documentation
├── README.md             ← This file
├── .gitignore
└── nodes/
    ├── user-profile.md   ← Identity, preferences, communication style
    ├── projects.md       ← Active builds & status
    ├── tech-stack.md     ← Languages, tools, infra
    ├── conversations.md  ← Session log (append-only)
    └── tasks.md          ← TODOs, blockers, next steps
```

## The Loop
1. **TURN START** → `git pull` → read INDEX.md + relevant nodes
2. **Conversation** → Perplexity uses context from nodes
3. **TURN END** → Append findings → `git commit && git push`

## For Perplexity (Since It Can't Run Git)
Use the GitHub REST API to read/write. See [LOOP.md](LOOP.md) for full API patterns.

## Never Delete Nodes
Append or create new ones. History is memory.
