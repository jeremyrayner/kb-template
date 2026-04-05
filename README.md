# LLM Knowledge Base Template

A ready-to-use template repo to fork - for building LLM-maintained knowledge bases with Obsidian based on the LLM knowledge base pattern created by [Andrej Karpathy](https://github.com/karpathy).

## Design principles

**Explicit.** Your knowledge is stored as a navigable wiki — you can see exactly what the AI knows and doesn't know. The memory artifact is inspectable and manageable, not implicit and hidden inside some AI provider's system.

**Yours.** Everything lives on your local machine as plain files. Your data is not locked into any particular AI provider. You're in full control of your information.

**File over app.** The entire knowledge base is markdown and images — universal formats that work with any tool. Obsidian, VS Code, vim, grep, the full Unix toolkit, any future tool that reads files. Data in, data out, no vendor lock-in. (See Steph Ango's [File over app](https://stephango.com/file-over-app) philosophy.)

**BYOAI.** Use whatever AI agent you want — Claude Code, OpenAI Codex, OpenCode, or anything else. The schema file (`CLAUDE.md`) tells the agent how to maintain the wiki; rename it to match your tool's convention (e.g. `AGENTS.md` for Codex). You could even fine-tune an open-source model on your wiki so it knows your knowledge in its weights, not just via context.

## Quick start

1. Fork this repo, or copy or unzip this folder and rename it to your topic (e.g. `kb-my-topic/)
2. Run `git init` in the folder (if not already forked) — the wiki is just markdown files, so you get version history for free
3. If not using Claude Code, rename `CLAUDE.md` to match your agent (e.g. `AGENTS.md` for Codex)
4. Open the folder as an Obsidian vault (wikilinks and attachment path are pre-configured in `.obsidian/app.json`)
5. Install community plugins: **Marp Slides**, **Dataview**, **Breadcrumbs**, **Excalidraw** (all optional)
6. Install the **Obsidian Web Clipper** browser extension and configure it to save to `raw/articles/`
7. Set up image downloading: in Obsidian Settings → Hotkeys, search for "Download attachments for current file" and bind it to a hotkey (e.g. Ctrl+Shift+D). After clipping an article, hit the hotkey to download all images to `raw/assets/` for local access.
8. Start clipping sources into `raw/`, then use your LLM agent to compile the wiki

## Structure

```
raw/              ← Your source documents (immutable, LLM never modifies)
  articles/       ← Web-clipped articles
  papers/         ← Academic papers, whitepapers
  images/         ← Diagrams, figures
  assets/         ← Downloaded image attachments
wiki/             ← LLM-generated knowledge base (LLM owns this entirely)
  sources/        ← Per-source summary pages
output/           ← Generated artifacts
  reports/        ← Q&A reports and lint reports
  slides/         ← Marp-format slide decks
  charts/         ← Generated charts and visualizations
_prompts/         ← Reusable prompt templates
docs/             ← Usage guide and founding documents
CLAUDE.md         ← Schema file — tells the LLM how to maintain the wiki
```

## How it works

The LLM reads sources from `raw/`, compiles them into interlinked wiki pages in `wiki/`, and maintains everything — summaries, cross-references, indexes. You curate sources, ask questions, and direct the analysis. The LLM does the bookkeeping.

See `CLAUDE.md` for the full schema, conventions, and workflows.
See `_prompts/` for the compilation and update prompts.
See `docs/` for the usage guide and founding documents.

## Attribution

This project is based on the LLM knowledge base pattern created by [Andrej Karpathy](https://github.com/karpathy). The core idea — using LLMs to incrementally compile and maintain a persistent wiki from raw source documents — originates from his work and writings on the topic. The founding documents in `docs/` capture his original vision; this template packages it into a ready-to-use structure.

## License

MIT License — see [LICENSE](LICENSE) for details.
