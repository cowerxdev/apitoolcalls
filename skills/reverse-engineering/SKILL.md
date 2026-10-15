---
name: reverse-engineering
description: "Describes how to read the structure of a file the user owns or has the right to inspect with the API Tool Calls MCP tools inspect_binary, extract_strings, inspect_apk and har_to_openapi and their browser pages: Windows, Linux and Mac program files, Android APKs, readable strings in any file, and HAR network captures turned into an OpenAPI description. Applies when asked what a program or app contains, which servers it talks to, what it may access, or how a service's API is shaped."
---

# Reverse engineering with [API Tool Calls](https://apitoolcalls.com)

Four MCP tools at `https://apitoolcalls.com/mcp` read a file's structure. They never run, patch or rebuild it.
Each also has a browser page that does the same work on the user's device, for any file size.

## Scope

- Only a file the user owns or has the right to inspect: their own builds, an app they audit with permission,
  a capture of their own browser session. Ask when it is unclear.
- No help bypassing DRM, licence or activation checks, anti-cheat, or a service's access controls, and no cracking.
  Say so and stop when that is the goal.
- Signatures and certificates are reported as present and described, never verified. Do not call one valid.

## Tools

| Tool | Give it | Gets back |
| --- | --- | --- |
| `inspect_binary` | `file`: an EXE, DLL, ELF or Mach-O as base64; `arch` picks a slice of a Mac universal binary | format, architecture, entry point, sections with entropy, imports, exports, PE resources, signature present, .NET |
| `extract_strings` | `file`: any file as base64; `min_length`, `encodings`, `kinds`, `contains`, `limit` | every ASCII and UTF-16LE string (UTF-8 on request) with offsets, labelled URL, email, IP, path, key or other, with counts per kind |
| `inspect_apk` | `file`: an .apk as base64 | package, versions, SDKs, permissions by group, components and whether each is exported, URLs and hosts in the code, signer certificate |
| `har_to_openapi` | `har`: a HAR file's JSON text | an OpenAPI 3.1 document of the API calls; cookies and secret values are removed before reading |

`file` takes base64 or a base64 data URL, at most 2,000,000 bytes decoded; `har` at most 2,000,000 characters.
The file travels in the call and is read in memory, not kept. For a bigger file, or one the user wants kept on
their device, point them to the page: `https://apitoolcalls.com/binary-inspector/`, `/strings/`, `/apk-inspector/`,
`/har-to-openapi/`, `/har-viewer/` (filter and clean a capture), `/hex-viewer/` (bytes and an entropy chart) and
`/asar-viewer/` (the files inside an Electron app's app.asar).

## Ways to combine them

1. A program file: `inspect_binary` first. Read the format, architecture, `signature_present` and `dotnet`. Imports
   name the libraries and functions it uses (sockets, HTTP, crypto, registry). A section near 8 bits per byte is
   compressed or encrypted, so expect few strings from it. Then `extract_strings` with `kinds: ["url", "ip", "email"]`
   to list the addresses written into it, and `kinds: ["key"]` for strings shaped like keys or tokens.
2. An Android app: `inspect_apk`. Permissions show what it may reach and which ones Android asks the person about;
   components with `exported: true` can be started by other apps; `urls_by_host` lists the servers named in its code
   (hosts with `common: true` are XML namespaces found in most apps). Compare the signer's SHA-256 with a known
   release to tell two builds apart.
3. A web or desktop app's API: have the user record their own session in the browser's developer tools (Network,
   save all as HAR), then `har_to_openapi`. For an Electron desktop app, the ASAR page shows its JavaScript and the
   addresses in it.
4. Report what was read, with offsets, section names or hosts. Say that string kinds are guesses from shape.

## Limits

Free with no key: 20 calls a day per IP, shared across tools. Lists in a result stop at 2,000 rows and give counts
of the rest; narrow `extract_strings` with `kinds` or `contains`.
