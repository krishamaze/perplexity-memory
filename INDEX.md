# 🧠 Perplexity Memory Graph
> Version-controlled stateful memory for Perplexity AI sessions

## Meta
- **Owner:** krishamaze (Krishnakumar)
- **Location:** Valparai, Tamil Nadu, IN
- **Role:** Solo Founder / Full-Stack Developer / AI Systems Engineer
- **Company:** Finetune Techcraft
- **Last Updated:** 2026-04-29

## Active Projects
| Node | Topic | Last Updated |
|---|---|---|
| [user-profile.md](nodes/user-profile.md) | Identity, preferences, stack | 2026-04-29 |
| [projects.md](nodes/projects.md) | Active builds & status | 2026-04-29 |
| [tech-stack.md](nodes/tech-stack.md) | Languages, tools, infra | 2026-04-29 |
| [conversations.md](nodes/conversations.md) | Session log & decisions | 2026-04-29 |
| [tasks.md](nodes/tasks.md) | TODOs, blockers, next steps | 2026-04-29 |

## Graph Links
- user-profile → projects (1:many)
- projects → tech-stack (many:many)
- conversations → all nodes (references)

## Session Loop Instructions
```
TURN START:
  1. git clone or git pull krishamaze/perplexity-memory
  2. cat INDEX.md  → identify relevant nodes
  3. cat nodes/<relevant>.md → load context

TURN END:
  1. Append findings to relevant node(s)
  2. Update INDEX.md last-updated timestamps
  3. git add . && git commit -m "session: <topic> [<date>]"
  4. git push origin main
```
