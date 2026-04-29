# Tasks & Next Steps

## Active TODOs
- [ ] Set up a GitHub PAT with `repo` scope for API writes
- [ ] Add PAT to Perplexity custom instructions (as a variable)
- [ ] Test first real session using the loop
- [ ] Build optional FastAPI relay for auto push/pull

## Blockers
- Perplexity cannot natively run git — use GitHub REST API instead:
  a) GET /contents/<file> to read (no auth needed for public repo)
  b) PUT /contents/<file> to write (needs PAT with `repo` scope)

## Ideas
- Build a tiny FastAPI relay: Perplexity POSTs findings → relay commits to GitHub
- Use GitHub Actions to auto-format/lint nodes on push
- Add a search index for fast keyword lookup
- Create a weekly summary node: nodes/weekly-YYYY-WXX.md

## ── Append New Tasks Below ──
