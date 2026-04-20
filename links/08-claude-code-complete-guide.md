# Claude Code Complete Guide

A practical reference for setting up and using Claude Code productively with minimal token waste.

## 1) Start Here

- Official docs: https://docs.anthropic.com/en/docs/claude-code/overview
- API/docs hub: https://docs.anthropic.com/
- Skills repo (official): https://github.com/anthropics/skills
- Skills customization page: https://claude.ai/customize/skills
- GodMode (popular repo): https://github.com/smol-ai/GodMode
- OpenRouter: https://openrouter.ai
- OpenRouter docs: https://openrouter.ai/docs

## 2) Slash Commands (common patterns)

Command availability can vary by client/version, but these are common high-utility patterns in Claude Code workflows:

- `/help` → Show available commands/help in your environment
- `/plan` → Ask Claude to create a step-by-step implementation plan
- `/search` → Find relevant files/symbols before editing
- `/diff` → Review pending file changes
- `/test` → Run test/build checks in guided flow
- `/commit` → Prepare structured commit messaging workflow

Tip: If your client supports a different command set, run `/help` first and map the equivalent flow.

## 3) Core Features to Use Daily

- Workspace-aware file editing
- Multi-file refactors with staged planning
- Code search and usage tracing
- Terminal-assisted run/build/test checks
- Patch-based edits for safer change review

## 4) Best Workflow (low risk + low token cost)

1. Define exact outcome in one short paragraph.
2. Ask for a small plan (`/plan`) with explicit phases.
3. Run search first, then edit only required files.
4. Validate quickly after each phase (`/test`, targeted checks).
5. Summarize changes and next actions.

## 5) Token Reduction Playbook

- Keep prompts narrow: one outcome per request.
- Provide target files explicitly to avoid broad scans.
- Ask for phased changes instead of giant one-shot edits.
- Reuse concise templates for repeated tasks.
- Request short status updates while work runs.
- Prefer links/files over pasting huge logs.

## 6) Obsidian + Graphify Workflow

### Obsidian skills

- Repo: https://github.com/kepano/obsidian-skills
- Use case: vault organization, linking strategy, note transformation

### Graphify

- Repo: https://github.com/safishamsi/graphify
- Use case: graph-centric knowledge and relationship mapping

Suggested flow:

1. Use Claude to clean and structure notes.
2. Apply Obsidian skill conventions for tags/links.
3. Export/index relationships with Graphify.
4. Iterate weekly with a "top knowledge gaps" review.

## 7) Caveman Skill (minimal style reasoning)

- Skill file: https://raw.githubusercontent.com/JuliusBrussee/caveman/refs/heads/main/caveman/SKILL.md
- Install at: https://claude.ai/customize/skills

Quick setup:

1. Open the SKILL.md link.
2. Copy full instructions.
3. Create a new skill in Claude customize page.
4. Paste instructions and save.
5. Invoke via your configured skill trigger.

## 8) Important Anthropic + Ecosystem Repos

### Official

- Anthropic skills: https://github.com/anthropics/skills
- MCP org: https://github.com/modelcontextprotocol
- MCP servers: https://github.com/modelcontextprotocol/servers
- MCP TypeScript SDK: https://github.com/modelcontextprotocol/typescript-sdk
- MCP Python SDK: https://github.com/modelcontextprotocol/python-sdk

### Useful open-source collections

- Awesome agent skills: https://github.com/VoltAgent/awesome-agent-skills
- Awesome Claude skills: https://github.com/ComposioHQ/awesome-claude-skills
- Superpowers: https://github.com/obra/superpowers
- Everything Claude Code: https://github.com/affaan-m/everything-claude-code

### Agent/dev tools requested

- GodMode: https://github.com/smol-ai/GodMode
- G0DM0D3: https://github.com/elder-plinius/G0DM0D3
- OpenCode: https://github.com/sst/opencode
- Claude Code community CLI: https://github.com/beita6969/claude-code
- KiloCode: https://github.com/Kilo-Org/kilocode
- GitHub Copilot CLI (`gh` extension): https://github.com/github/gh-copilot

### Curated repos from shared list

- OpenSpace: https://github.com/HKUDS/OpenSpace
- CLI-Anything: https://github.com/HKUDS/CLI-Anything
- PAUL: https://github.com/ChristopherKahler/paul
- claude-mem (thedotmack): https://github.com/thedotmack/claude-mem
- Awesome Claude Code: https://github.com/hesreallyhim/awesome-claude-code
- Vibe Kanban: https://github.com/BloopAI/vibe-kanban
- SuperClaude Framework: https://github.com/SuperClaude-Org/SuperClaude_Framework
- Continuous Claude v3: https://github.com/parcadei/Continuous-Claude-v3

## 9) Setup: OpenRouter + coding tools

Use this when a CLI/tool supports OpenAI-compatible providers and custom API base URLs.

1. Create key in OpenRouter dashboard: https://openrouter.ai
2. Read provider docs: https://openrouter.ai/docs
3. Set environment variables in terminal:
	 - `OPENROUTER_API_KEY=...`
	 - `OPENAI_BASE_URL=https://openrouter.ai/api/v1` (for compatible clients)
4. Select your target model in the tool config.

Note: Provider/model wiring differs by tool version. Always check each tool’s README first.

## 10) Setup: OpenCode, KiloCode, Copilot CLI, Claude Code

### Claude Code

- Docs/start: https://docs.anthropic.com/en/docs/claude-code/overview
- Recommended: use official docs + `anthropics/skills` first, then add third-party packs.

### OpenCode

- Repo: https://github.com/sst/opencode
- Steps:
	1. Follow installation instructions from repo README.
	2. Configure model/provider keys (Anthropic/OpenRouter/etc as supported).
	3. Test with a small repo before full migration.

### Community Claude Code CLI

- Repo: https://github.com/beita6969/claude-code
- Quick test:
	1. `git clone https://github.com/beita6969/claude-code.git && cd claude-code`
	2. `bun install`
	3. `bun src/main.tsx -p "hello" --output-format text`

### KiloCode

- Repo: https://github.com/Kilo-Org/kilocode
- Steps:
	1. Install from the official repo instructions.
	2. Configure preferred model provider.
	3. Validate search/edit/test loop on a sample project.

### GitHub Copilot CLI

- Repo: https://github.com/github/gh-copilot
- Typical setup:
	1. Install GitHub CLI (`gh`).
	2. Install extension: `gh extension install github/gh-copilot`
	3. Authenticate with GitHub and test command suggestions.

## 11) About "leaked" prompt/code packs

Avoid leaked or unauthorized dumps. Use trusted public repos and official docs instead:

- Anthropic skills: https://github.com/anthropics/skills
- Everything Claude Code (community index): https://github.com/affaan-m/everything-claude-code
- Awesome Claude skills: https://github.com/ComposioHQ/awesome-claude-skills

## 12) Recommended Minimal Stack (MVP)

If you want fast results without overload, start with:

- 1 official skill set (`anthropics/skills`)
- 1 reliability-focused pack (`obra/superpowers`)
- 1 MCP integration (`modelcontextprotocol/servers`)
- 1 eval tool (`promptfoo` or `deepeval`)

Then expand only when a real workflow requires it.
