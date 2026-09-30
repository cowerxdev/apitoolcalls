---
name: apitoolcalls
description: "Describes remote MCP tools and connection settings for API Tool Calls for requests involving SVG QR codes, public YouTube captions, public pages converted to Markdown, data source previews, or résumé skill gaps against Columbus, Ohio job postings. Applies when configuring or calling these tools."
---

# API Tool Calls

Remote MCP endpoint: `https://apitoolcalls.com/mcp`, Streamable HTTP.
The client exposes the tool names below, sometimes with an `apitoolcalls` prefix.

| Tool | Arguments and result |
| --- | --- |
| `make_qr` | Nonempty `text` (text or URL), or `wifi` with nonempty `ssid`, `security` (`WPA`, `WEP`, `nopass`), and `password` for secured networks. `wifi` takes precedence over `text`. Optional `format` is only `svg` (default). Returns SVG and the encoded payload as text. QR capacity limits apply. |
| `get_transcript` | Required `url`: public YouTube URL or 11-character video ID. Optional `lang` defaults to `en`; an unavailable language falls back to English, then an available track. Returns timestamped plain text and track metadata. Existing public captions only; no video or audio. Output is bounded to 200,000 characters including metadata and may say `(truncated)`. |
| `resume_gap` | Required `resume_text`: plain text, 50–50,000 characters. Required `family`: `data analyst`, `software engineer`, or `project manager`. Returns skills Columbus, Ohio postings ask for that the résumé shows (`have`) or lacks (`learn`), posting shares/counts, metro, sample size and date. Résumé text is processed temporarily and removed after the check. |
| `page_to_markdown` | Required `url`: public http or https HTML page URL. Returns Markdown with title, headings, lists, tables and absolute links, plus a source URL. One page, 2 MB HTML maximum, up to five redirects, 10 seconds for fetching and 10 seconds for conversion. No logins, paywalls, cookies or JavaScript rendering; private network addresses are refused. |
| `find_data` | Required `use_case`: nonempty string, at most 500 characters. Returns up to three source names and one plain line each from the Cowerx Data Finder snapshot. Uses web preview defaults (United States, no selected topics, no resale), with geography inferred from text. Runs locally on the server with a 10-second timeout; no live source lookup. |

Without a key: 20 tool calls per IP per UTC day, shared across tools.
An active key: $9.99/month for 1,000 calls per UTC month, shared across tools.
Validated calls can count even if processing fails.

MCP errors arrive as JSON-RPC `error.code` and `error.message`, even with HTTP 200:

| Code | Meaning / typical message |
| --- | --- |
| `-32602` | Invalid arguments; message names the field or unknown tool. |
| `-32000` | Free daily limit reached; the message includes key information. |
| `-32001` | Unknown, invalid or inactive API Tool Calls key. |
| `-32002` | `Monthly key limit reached (1,000 calls this UTC month).` |
| `-32003` | Captions disabled/missing, unavailable video, résumé input/data error, or unreadable/blocked/oversize HTML page; read the message. |
| `-32004` | `YouTube did not answer; try again later`, `Résumé check is unavailable; try again later`, `Could not read this page; try again later`, or `Data Finder is unavailable; try again later`. |

For a key the user already has, add the HTTP header
`Authorization: Bearer ot_live_...` in the client's MCP configuration.
Keep the key in client credentials or environment settings, outside tool arguments.
For free access, omit the header entirely. Key information is at
`https://apitoolcalls.com/key.html`. Client setup is documented in the pack README.
