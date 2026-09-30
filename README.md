# API Tool Calls skill pack

API Tool Calls exposes five tools through remote MCP, Streamable HTTP, at
`https://apitoolcalls.com/mcp`:

| Tool | Function |
| --- | --- |
| `make_qr` | Text, URL or Wi-Fi details → SVG QR code. |
| `get_transcript` | Public YouTube captions → timestamped text; captions only, no video or audio. |
| `resume_gap` | Résumé text + job family → skills shown/missing against Columbus, Ohio postings. Families: data analyst, software engineer, project manager. |
| `page_to_markdown` | Public page URL → clean Markdown with headings, lists, tables and absolute links. No logins, paywalls or JavaScript rendering; 2 MB HTML limit. |
| `find_data` | Data use case → up to three source names and a plain line each from a saved Cowerx Data Finder catalogue. |

See [the skill](apitoolcalls/SKILL.md) for arguments, limits and errors.
Free access needs no account or key: 20 calls per IP per UTC day across all tools.
An optional subscription key costs $9.99/month for 1,000 calls per UTC month;
key information is at [the key page](https://apitoolcalls.com/key.html).
Clients send an existing key as `Authorization: Bearer ot_live_...`.
Cloud connectors may share an outbound IP, so their free allowance can be shared.

The service is live at `https://apitoolcalls.com`. Client setup syntax below was
checked against each client's official documentation on 2026-09-29;
[Sources](SOURCES.md) record the formats used.
Installing the skill supplies documentation; configuring MCP supplies the tools.

## Claude Code

Choose one configuration. Free access:

```sh
claude mcp add --transport http apitoolcalls https://apitoolcalls.com/mcp
```

With an existing key (replace the placeholder):

```sh
claude mcp add --transport http apitoolcalls https://apitoolcalls.com/mcp \
  --header "Authorization: Bearer ot_live_REPLACE_WITH_YOUR_KEY"
```

These use Claude Code's default local scope. `/mcp` shows connection status.
[Claude Code MCP reference](https://code.claude.com/docs/en/mcp).

## Claude.ai / Claude Desktop custom connector

In **Customize → Connectors**, choose **+ → Add custom connector**. Enter
API Tool Calls as the name and `https://apitoolcalls.com/mcp` as the remote server URL,
then Add. Enable the connector through the conversation's **+ → Connectors**.
For Team/Enterprise, an owner first adds the web connector in
**Organization settings → Connectors**.

Use the unauthenticated endpoint. The documented Advanced settings accept OAuth
client credentials and do not document arbitrary bearer headers. The
API Tool Calls subscription key is a static bearer token; paid-key setup through this UI is
unverified. Remote connectors run through Anthropic's cloud, including Desktop.
[Claude custom connector guide](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

## ChatGPT / Codex

Codex uses `~/.codex/config.toml` (or `.codex/config.toml` in a trusted project):

```toml
[mcp_servers.apitoolcalls]
url = "https://apitoolcalls.com/mcp"
```

For an existing key, add this line inside that table:

```toml
bearer_token_env_var = "APITC_API_KEY"
```

Set `APITC_API_KEY=ot_live_...` in the environment of the client process;
the variable contains the token without the `Bearer ` prefix. Omit the setting
for free access. The documented ChatGPT desktop, Codex CLI and IDE clients share
this configuration for the same Codex host.
[OpenAI MCP configuration](https://developers.openai.com/codex/mcp/).

ChatGPT web uses a UI, not this TOML file: enable Developer mode under
**Settings → Security and login**, then create a developer-mode app with the
plus button on the Plugins page. Enter the MCP URL and choose **No Authentication**.
Select the app in the composer's Developer mode tools. The documented web auth
modes are OAuth, No Authentication and Mixed Authentication; a static bearer
header field is not documented, so subscription-key setup there is unverified.
[ChatGPT Developer mode](https://developers.openai.com/api/docs/guides/developer-mode).

## Hermes Agent (Nous Research)

Merge into `~/.hermes/config.yaml`:

```yaml
mcp_servers:
  apitoolcalls:
    url: "https://apitoolcalls.com/mcp"
```

For an existing key, the server entry becomes:

```yaml
mcp_servers:
  apitoolcalls:
    url: "https://apitoolcalls.com/mcp"
    headers:
      Authorization: "Bearer ${APITC_API_KEY}"
```

Set `APITC_API_KEY=ot_live_...` in `~/.hermes/.env`, then restart Hermes
or use `/reload-mcp`. Free mode omits `headers`.
[Hermes MCP guide](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp).

For the skill, copy this pack's `apitoolcalls/` folder to
`~/.hermes/skills/apitoolcalls/`. Hermes accepts a directory with `SKILL.md`, YAML
`name` and `description`, and a Markdown body. Its Skills Hub supports GitHub
repo/path sources and custom taps; install this skill from its public repository with
`hermes skills install cowerxdev/apitoolcalls/apitoolcalls`.
[Hermes Skills System](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills).

## OpenClaw / ClawHub

From a clone of this repository, install the local skill:

```sh
openclaw skills install ./apitoolcalls --as apitoolcalls
```

This installs into the active workspace's `skills/` directory.
[OpenClaw skill installation](https://docs.openclaw.ai/tools/skills).
Configure the free MCP connection separately:

```sh
openclaw mcp add apitoolcalls --url https://apitoolcalls.com/mcp \
  --transport streamable-http
```

[OpenClaw MCP setup](https://docs.openclaw.ai/tools/mcp).
For headers, the documented Settings → MCP scoped editor supports additional
configuration; consult its secret mechanisms before entering a subscription key.

ClawHub accepts a skill folder containing `SKILL.md`. The portable name matches
the folder, uses lowercase letters/digits/hyphens and is 1–64 characters long;
`description` supplies the catalog summary. Publishing creates semver releases.
ClawHub distributes skills under MIT-0 and does not support paid skills. External
service fees belong in the instructions; optional credential variables, if
declared, use `metadata.openclaw.envVars` with `required: false`.
This pack needs no mandatory credential variable or executable helper.
[ClawHub skill format](https://docs.openclaw.ai/clawhub/skill-format).

## Pack contents

- `apitoolcalls/SKILL.md`: portable tool and connection reference.
- `server.json`: official MCP Registry metadata, version 0.1.0.
- `LISTINGS.md`: the directories this pack is submitted to, with their rules.
- `SOURCES.md`: documentation URLs and read dates.

`server.json` has an optional secret Authorization input whose value is the
complete header, including `Bearer `. It has no credential default.
[Registry remote metadata](https://modelcontextprotocol.io/registry/remote-servers).
