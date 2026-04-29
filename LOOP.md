# 🔄 The Perplexity Memory Loop

## How It Works

Perplexity is stateless by default. This repo makes it stateful by using GitHub
as a persistent memory store. Every session reads from and writes to this repo.

## TURN START Protocol
```bash
# 1. Pull latest memory
git clone https://github.com/krishamaze/perplexity-memory.git
# or if already cloned:
git pull origin main

# 2. Read the graph root
cat INDEX.md

# 3. Load relevant nodes based on the conversation topic
cat nodes/user-profile.md
cat nodes/projects.md      # if talking about projects
cat nodes/tasks.md         # if asking what to do next
cat nodes/conversations.md # for continuity with past sessions
```

## TURN END Protocol
```bash
# 1. Append findings to relevant node
echo "\n### Finding\n- ..." >> nodes/conversations.md

# 2. Update INDEX.md timestamps
sed -i 's/conversations.md | .*/conversations.md | 2026-04-29/' INDEX.md

# 3. Commit and push
git add .
git commit -m "session: <topic> [$(date +%Y-%m-%d)]"
git push origin main
```

## Node Naming Rules
- Nodes are NEVER deleted — only appended
- New topic = new node file under nodes/
- Each node ends with `## ── Append New Findings Below ──`
- INDEX.md always stays as the root

## Search Pattern
```bash
grep -r "<keyword>" nodes/
```

## Since Perplexity Can't Run Git
Use the **GitHub REST API** to read/write files:

### Read a file
```
GET https://api.github.com/repos/krishamaze/perplexity-memory/contents/nodes/user-profile.md
```
Decode the base64 `content` field.

### Write/Append to a file
```
PUT https://api.github.com/repos/krishamaze/perplexity-memory/contents/nodes/conversations.md
{
  "message": "session: <topic> [date]",
  "content": "<base64 of new full content>",
  "sha": "<current file sha>"
}
```
Requires a GitHub PAT with `repo` scope stored as a custom instruction secret.

## Recommended Custom Instruction (Paste into Perplexity Settings)
```
MEMORY REPO: https://github.com/krishamaze/perplexity-memory

ON TURN START:
1. Fetch INDEX.md from the memory repo via GitHub API
2. Read relevant node files based on conversation topic
3. Use that context to personalize your response

ON TURN END:
1. Summarize key findings/decisions from this session
2. Append to nodes/conversations.md via GitHub API PUT
3. Update any other relevant nodes
4. Never delete node content — append only

SEARCH: GET /repos/krishamaze/perplexity-memory/contents/nodes/<file>
```
