# Documentation sources

All sources below were read on **2026-09-29**. Only public documentation and
webpages were read. No client setup, login, publication, or directory/registry
API operation was performed. Snippets are checked against documentation, not
live client execution. Undocumented prices or login gates remain unconfirmed.

| Format / fact checked | Documentation URL | Date read |
| --- | --- | --- |
| Agent Skills folder, frontmatter, name and description constraints | [Agent Skills specification](https://agentskills.io/specification) | 2026-09-29 |
| Claude Code HTTP CLI and header flag | [Claude Code MCP](https://code.claude.com/docs/en/mcp) | 2026-09-29 |
| Claude.ai/Desktop remote connector UI and OAuth settings | [Claude custom connectors](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp) | 2026-09-29 |
| Codex TOML, token environment variable, shared host configuration | [OpenAI MCP](https://developers.openai.com/codex/mcp/) | 2026-09-29 |
| ChatGPT web developer-mode app and authentication modes | [ChatGPT Developer mode](https://developers.openai.com/api/docs/guides/developer-mode) | 2026-09-29 |
| Hermes MCP YAML, headers, environment substitution and reload | [Hermes MCP](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp) | 2026-09-29 |
| Hermes skill location, GitHub paths, taps and install scanning | [Hermes Skills System](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills) | 2026-09-29 |
| Hermes publication syntax and optional/community skill placement | [Hermes Creating Skills](https://hermes-agent.nousresearch.com/docs/developer-guide/creating-skills) | 2026-09-29 |
| OpenClaw local skill install | [OpenClaw Skills](https://docs.openclaw.ai/tools/skills) | 2026-09-29 |
| OpenClaw outbound HTTP MCP CLI | [Connect MCP servers](https://docs.openclaw.ai/tools/mcp) | 2026-09-29 |
| ClawHub SKILL.md, optional environment metadata, semver, MIT-0 | [ClawHub skill format](https://docs.openclaw.ai/clawhub/skill-format) | 2026-09-29 |
| ClawHub publish CLI, owners and automated review | [ClawHub publishing](https://docs.openclaw.ai/clawhub/publishing) | 2026-09-29 |
| ClawHub GitHub/device login and token option | [ClawHub CLI](https://docs.openclaw.ai/clawhub/cli) | 2026-09-29 |
| Registry's current server schema, including optional secret header input | [Server schema 2025-12-11](https://static.modelcontextprotocol.io/schemas/2025-12-11/server.schema.json) | 2026-09-29 |
| Registry remotes and streamable-http header list | [Publishing remote servers](https://modelcontextprotocol.io/registry/remote-servers) | 2026-09-29 |
| Registry publisher install/login/publish steps | [Registry quickstart](https://modelcontextprotocol.io/registry/quickstart) | 2026-09-29 |
| Registry GitHub user/org namespace identity | [Registry authentication](https://modelcontextprotocol.io/registry/authentication) | 2026-09-29 |
| Registry automated validation requirements | [Official Registry requirements](https://github.com/modelcontextprotocol/registry/blob/main/docs/reference/server-json/official-registry-requirements.md) | 2026-09-29 |
| Smithery URL submission and scanning | [Smithery publishing](https://smithery.ai/docs/build/publish) | 2026-09-29 |
| Smithery namespace ownership and free Hobby allowance | [Smithery namespaces](https://smithery.ai/docs/concepts/namespaces) | 2026-09-29 |
| Smithery publishing page login gate (redirect observed) | [Smithery new server](https://smithery.ai/new) | 2026-09-29 |
| Glama remote submission, health checks and identity claims | [Glama MCP FAQ](https://glama.ai/mcp/faq) | 2026-09-29 |
| Glama remote listing entry point | [Glama connectors](https://glama.ai/mcp/connectors) | 2026-09-29 |
| mcp.so remote form fields, $39 fee and review wording | [mcp.so remote submission](https://mcp.so/submit?type=remote-server) | 2026-09-29 |
| mcp.so account login fields | [mcp.so sign in](https://mcp.so/sign-in) | 2026-09-29 |

Tool behavior was checked locally in `app/__init__.py` (`TOOLS`, validation,
quota and error handling), `app/transcript.py`, `app/resume.py`, and
`site/agent.html`. Domain constraints came from `CLAUDE.md`; scope came from
`issues/06-skill-pack-and-listings.md` and the task instructions. These local
sources were also read on 2026-09-29.
