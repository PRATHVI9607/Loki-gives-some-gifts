# Setup Guides + Workflows

## Claude skill setup (generic)

1. Open: https://claude.ai/customize/skills
2. Click `+` to create a skill.
3. Add name + description.
4. Paste skill instructions (`SKILL.md` content).
5. Save and invoke with the skill command in chat.

## Example: Caveman skill setup

- Skill source: https://raw.githubusercontent.com/JuliusBrussee/caveman/refs/heads/main/caveman/SKILL.md
- Steps:
  1. Open the link and copy full content.
  2. Create a new Claude skill at `https://claude.ai/customize/skills`.
  3. Set `Name: Caveman`.
  4. Paste content into instructions and save.

## Browser add-on workflow (Claude Counter from source notes)

### Chrome / Edge / Chromium

1. Open `chrome://extensions`.
2. Enable Developer Mode.
3. Drag-and-drop the `claude-counter` zip package.

### Firefox

1. Drag-and-drop the `claude-counter` `.xpi` package into Firefox.
2. Confirm install.

## Suggested environment setup order

1. Start with one official skill/plugin from `01-official-claude-and-anthropic.md`.
2. Add one proven skills repo from `02-skills-and-plugin-collections.md`.
3. Add one MCP/open-source tool from `03-open-source-agents-and-tooling.md`.
4. Add optional creative/marketing tools from `04-creative-marketing-and-growth.md`.
5. Keep your own tested stack in a separate personal checklist.

## More open-source skills (recommended)

- Anthropic official skills: https://github.com/anthropics/skills
- Awesome Agent Skills: https://github.com/VoltAgent/awesome-agent-skills
- Awesome Claude Skills: https://github.com/ComposioHQ/awesome-claude-skills
- Claude skills collection: https://github.com/alirezarezvani/claude-skills
- Awesome Claude Code subagents: https://github.com/VoltAgent/awesome-claude-code-subagents
- Superpowers: https://github.com/obra/superpowers
- Antigravity awesome skills: https://github.com/sickn3/antigravity-awesome-skills

## More open-source MCP links

- MCP servers (official collection): https://github.com/modelcontextprotocol/servers
- MCP TypeScript SDK: https://github.com/modelcontextprotocol/typescript-sdk
- MCP Python SDK: https://github.com/modelcontextprotocol/python-sdk
- MCP Inspector: https://github.com/modelcontextprotocol/inspector
- Google APIs MCP toolbox: https://github.com/googleapis/mcp-toolbox
- Excel MCP server: https://github.com/haris-musa/excel-mcp-server

## Practical workflow packs

### Workflow A: Skill-first coding setup (fastest)

1. Install 1 core skill from `anthropics/skills`.
2. Add 1 quality skill from `obra/superpowers`.
3. Add 1 review skill from `awesome-claude-skills`.
4. Keep a small personal set (3–5 skills max to start).

### Workflow B: MCP-first integration setup

1. Start from `modelcontextprotocol/servers` examples.
2. Pick SDK (`typescript-sdk` or `python-sdk`) for your stack.
3. Validate with `modelcontextprotocol/inspector`.
4. Add domain server(s) like `googleapis/mcp-toolbox` or `excel-mcp-server`.

### Workflow C: Agent + command productivity setup

1. Add one agent framework from your tooling list.
2. Add reusable command packs: https://github.com/wshobson/commands
3. Add Claude command suite: https://github.com/qdhenry/Claude-Command-Suite
4. Review and prune monthly to keep only high-signal tools.

## Maintenance workflow (monthly)

1. Remove broken/unused skills and servers.
2. Pin your top tools in a personal "gold stack" document.
3. Track version changes in your key repos.
4. Re-test end-to-end flows after major updates.

## Workflow D: Local + private stack (self-hosted)

1. Start local model runtime with `Ollama`.
2. Add a local UI with `Open WebUI`.
3. Route providers with `LiteLLM` when needed.
4. Add one MCP server for your highest-value integration.

Useful links:

- Ollama: https://github.com/ollama/ollama
- Open WebUI: https://github.com/open-webui/open-webui
- LiteLLM: https://github.com/BerriAI/litellm

## Workflow E: Evaluation + tracing before scale

1. Write 10 to 30 representative prompts/tasks.
2. Add automatic eval checks (quality + regressions).
3. Add tracing/observability to inspect failures.
4. Run evals before changing prompts, skills, or MCP wiring.

Useful links:

- Promptfoo: https://github.com/promptfoo/promptfoo
- DeepEval: https://github.com/confident-ai/deepeval
- Langfuse: https://github.com/langfuse/langfuse
- OpenLLMetry: https://github.com/traceloop/openllmetry

## Workflow F: Security-first setup

1. Keep secrets in environment variables (never hardcode).
2. Limit MCP/tool permissions to least privilege.
3. Use dependency and secret scanning on every repo.
4. Review prompt injection and data exfiltration risks regularly.

Useful links:

- OWASP Top 10: https://owasp.org/www-project-top-ten/
- Trivy: https://github.com/aquasecurity/trivy
- Gitleaks: https://github.com/gitleaks/gitleaks

## Workflow G: Multi-tool coding stack (Claude Code + OpenCode + KiloCode + Copilot CLI)

1. Keep one primary coding assistant and use others as secondary reviewers.
2. Use a shared environment file for provider keys.
3. Standardize your dev loop: search → plan → edit → test → diff.
4. Benchmark token and latency on one representative task weekly.

Useful links:

- Claude Code docs: https://docs.anthropic.com/en/docs/claude-code/overview
- OpenCode: https://github.com/sst/opencode
- KiloCode: https://github.com/Kilo-Org/kilocode
- GitHub Copilot CLI: https://github.com/github/gh-copilot
- OpenRouter: https://openrouter.ai
- OpenRouter docs: https://openrouter.ai/docs

## Workflow H: Community packs (legal/public)

1. Prefer official and public repos over private/leaked prompt dumps.
2. Pin the exact repo commit/release for reproducibility.
3. Test every imported skill/command in a sandbox repo first.

Useful links:

- Anthropic skills (official): https://github.com/anthropics/skills
- GodMode (popular public repo): https://github.com/smol-ai/GodMode
- Everything Claude Code: https://github.com/affaan-m/everything-claude-code
- Awesome Claude skills: https://github.com/ComposioHQ/awesome-claude-skills

## Workflow I: Community Claude Code CLI setup

If you want to test a community CLI quickly:

1. Clone repository: `git clone https://github.com/beita6969/claude-code.git && cd claude-code`
2. Install dependencies: `bun install`
3. Run a basic prompt: `bun src/main.tsx -p "hello" --output-format text`

Also useful:

- Everything Claude Code: https://github.com/affaan-m/everything-claude-code
- Awesome Claude Code: https://github.com/hesreallyhim/awesome-claude-code

## Workflow J: Curated repo stack from shared list

1. Start with one planning framework: `paul`.
2. Add one memory layer: `claude-mem`.
3. Add one task board workflow: `vibe-kanban`.
4. Add one context-optimization stack: `OpenSpace` or `CLI-Anything`.

Useful links:

- OpenSpace: https://github.com/HKUDS/OpenSpace
- CLI-Anything: https://github.com/HKUDS/CLI-Anything
- PAUL: https://github.com/ChristopherKahler/paul
- claude-mem (thedotmack): https://github.com/thedotmack/claude-mem
- Vibe Kanban: https://github.com/BloopAI/vibe-kanban
