# Listing preparation — local draft

[API Tool Calls](https://apitoolcalls.com): connect once to one small MCP door at https://apitoolcalls.com/mcp. Its 3 meta tools find, describe and call any of our 89 tools, with under 1k tokens of definitions at connection time however many tools ship. Directory scanners and clients that need the full tool listing can read https://apitoolcalls.com/mcp?tools=all.

Research date: **2026-09-29**. The steps below describe a future submission;
none were executed. Every row distinguishes documented behavior from missing
information. No public GitHub repository, claimed namespace or listing is assumed.

Prepared metadata: name **[API Tool Calls](https://apitoolcalls.com)**, slug **apitoolcalls**, version **0.1.0**,
homepage `https://apitoolcalls.com/agent.html`, remote URL
`https://apitoolcalls.com/mcp`, transport `streamable-http`.
Short description: “89 tools, one small door: home costs, fitness, QR, barcodes, Markdown, SEO, recalls.”
Full-list scanner URL: `https://apitoolcalls.com/mcp?tools=all`. Authentication: none for 20 calls/day/IP;
optional `Authorization: Bearer ot_live_...` for an existing subscription key.
The skill entry point is `apitoolcalls/SKILL.md`; registry metadata is `server.json`.

| Directory | Submission route | Account / identity | Cost documented | Review documented | Human login |
| --- | --- | --- | --- | --- | --- |
| [MCP Registry](https://modelcontextprotocol.io/registry/quickstart) | `mcp-publisher`, local `server.json` | [GitHub cowerxdev user or authorized org identity](https://modelcontextprotocol.io/registry/authentication) | No submission fee stated in cited docs | [Namespace/schema validation](https://github.com/modelcontextprotocol/registry/blob/main/docs/reference/server-json/official-registry-requirements.md) | GitHub device authorization for interactive route |
| [Smithery](https://smithery.ai/docs/build/publish) | URL publishing at `/new` | [Smithery account and owned namespace](https://smithery.ai/docs/concepts/namespaces) | Hobby free, 3 namespaces; publishing fee not separately stated | Automatic metadata scan | [Yes, `/new` redirects to sign-in](https://smithery.ai/new) |
| [Glama](https://glama.ai/mcp/faq) | Add MCP Server → Connector | Glama account for ownership; domain or matching GitHub identity | No submission fee stated in cited docs | Reachability/health gate | Yes for claim; initial submission gate undocumented |
| [mcp.so](https://mcp.so/submit?type=remote-server) | Remote Server form | [Email/password account offered](https://mcp.so/sign-in) | $39 one-time | Paid form says immediate publication without review | Sign-in available; requirement before payment unverified |
| [ClawHub](https://docs.openclaw.ai/clawhub/publishing) | `clawhub skill publish` | [GitHub login and authorized publisher handle](https://docs.openclaw.ai/clawhub/cli) | No submission fee stated; published skills free, no per-skill pricing | Metadata/file validation + automated security checks; release may wait for review | Device approval; existing token can replace interactive login |
| [Hermes Skills Hub](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills) | GitHub repo/path or custom tap | GitHub repository owner; no separate hub signup for a tap | No hub fee stated in cited docs | Security scan at install; official optional skills use maintained repo | GitHub authorization to publish; no separate hub login |

## MCP Registry

1. Install `mcp-publisher` using the [quickstart](https://modelcontextprotocol.io/registry/quickstart) (Homebrew example: `brew install mcp-publisher`). Work from the directory containing this draft's `server.json`.
2. Run `mcp-publisher login github`; open the displayed GitHub device URL, enter the displayed code, and authorize the application. Identity must permit `io.github.cowerxdev/apitoolcalls`; the [authentication guide](https://modelcontextprotocol.io/registry/authentication) supports both user and organization namespaces.
3. Run `mcp-publisher publish` from that directory. The [remote-server guide](https://modelcontextprotocol.io/registry/remote-servers) requires a publicly accessible endpoint and supports remotes without a package, so no npm/PyPI release is needed.

The [official requirements](https://github.com/modelcontextprotocol/registry/blob/main/docs/reference/server-json/official-registry-requirements.md) describe automated namespace and metadata checks. They do not specify a manual approval queue or submission fee. The [schema](https://static.modelcontextprotocol.io/schemas/2025-12-11/server.schema.json) defines `headers` as input objects; this draft sets Authorization to optional/secret and uses a placeholder, with no key embedded. Interactive GitHub device authorization requires a person. [Authentication guide](https://modelcontextprotocol.io/registry/authentication).

## Smithery

1. Sign in at [smithery.ai/new](https://smithery.ai/new); the public entry point redirects to account login.
2. Use an owned namespace (proposed `cowerxdev`, availability unverified), with server slug `apitoolcalls`. [Namespaces](https://smithery.ai/docs/concepts/namespaces) documents ownership and the free Hobby allowance of three namespaces.
3. Enter `https://apitoolcalls.com/mcp?tools=all` as the public HTTPS MCP URL and complete the URL publishing flow. Smithery scans tools/prompts/resources automatically for public servers. [Publishing guide](https://smithery.ai/docs/build/publish).

That guide requires Streamable HTTP and OAuth when authentication is required.
The public free mode of [API Tool Calls](https://apitoolcalls.com) fits the documented URL route; optional static-key
forwarding through Smithery is unverified. The guide documents automatic scans
and an optional vendor-verification checklist, with no manual-review timing or
separate submission price. No deployment to Smithery is required for the URL route.
[Publishing guide](https://smithery.ai/docs/build/publish).

## Glama

1. On [Glama connectors](https://glama.ai/mcp/connectors), choose Add Server / Add MCP Server → Connector.
2. Enter [API Tool Calls](https://apitoolcalls.com), the description, and `https://apitoolcalls.com/mcp?tools=all` as the HTTPS Streamable HTTP URL. Test credentials are optional. Only healthy connectors are indexed. [Glama FAQ](https://glama.ai/mcp/faq).
3. Choose Claim ownership and sign in. Verify the domain with the displayed TXT record at `_glama-claim.<domain>` or JSON at `/.well-known/glama.json`. A Registry-linked `io.github.cowerxdev` identity can use GitHub verification; an org also needs the Glama GitHub App installed. [Glama FAQ](https://glama.ai/mcp/faq).

The FAQ does not state a submission fee or the initial form's login requirement.
Claiming requires login.
[Glama FAQ](https://glama.ai/mcp/faq).

## mcp.so

1. Open the [Remote Server submission form](https://mcp.so/submit?type=remote-server).
2. Enter `https://apitoolcalls.com/mcp` in Remote endpoint URL and [API Tool Calls](https://apitoolcalls.com) in Name; both fields are required.
3. The current form's action is **Pay and submit automatically**, with a $39 one-time fee and immediate publication without review. This is a paid route; no free option is shown on this form. [Submission form](https://mcp.so/submit?type=remote-server).

The site's [sign-in page](https://mcp.so/sign-in) offers email/password login and
signup. Whether checkout requires that login is not established by the public
form. No payment, account creation or submission was attempted.

## ClawHub

1. Install the ClawHub CLI (`npm i -g clawhub`). Run `clawhub login`, visit its printed verification URL and approve after GitHub sign-in. An existing API token is also supported. [CLI guide](https://docs.openclaw.ai/clawhub/cli).
2. Prepare this pack's `apitoolcalls/` folder. ClawHub accepts `SKILL.md`, extracts the description, uses semver, and distributes published skills under MIT-0. It permits external paid-service integrations when instructions explain the cost/account; optional variables must be declared optional if added. [Skill format](https://docs.openclaw.ai/clawhub/skill-format).
3. From the pack directory, submit with `clawhub skill publish ./apitoolcalls --slug apitoolcalls --name "API Tool Calls" --version 0.1.0`. Add `--owner cowerxdev` only if that publisher handle exists and the login has access. [Publishing guide](https://docs.openclaw.ai/clawhub/publishing).

Publication validates owner access, metadata and files, then starts automated
security checks; releases can remain unavailable during review. No review SLA
or submission fee is stated there. Skills have no per-skill pricing; this does
not change the external [API Tool Calls](https://apitoolcalls.com) subscription. [Publishing](https://docs.openclaw.ai/clawhub/publishing),
[CLI](https://docs.openclaw.ai/clawhub/cli).

## Hermes Skills Hub

1. Establish a public GitHub skill repository with `apitoolcalls/SKILL.md` and standard frontmatter. [Creating Skills](https://hermes-agent.nousresearch.com/docs/developer-guide/creating-skills).
2. The documented publishing command is `hermes skills publish ./apitoolcalls --to github --repo cowerxdev/apitoolcalls`. [Creating Skills](https://hermes-agent.nousresearch.com/docs/developer-guide/creating-skills).
3. Users install by path: `hermes skills install cowerxdev/apitoolcalls/apitoolcalls`. For a tap, place skills under `skills/` and use `hermes skills tap add cowerxdev/apitoolcalls`; nondefault paths need a tap entry edit. [Skills System](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills).

Installs are security-scanned; dangerous verdicts block installation. Official
optional skills are maintained separately in the Hermes repo. No hub fee is
stated. GitHub publishing needs repository authorization; custom taps need no
separate hub signup. [Skills System](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills),
[Creating Skills](https://hermes-agent.nousresearch.com/docs/developer-guide/creating-skills).
