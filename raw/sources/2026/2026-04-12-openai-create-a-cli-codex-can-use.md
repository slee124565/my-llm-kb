# Create a CLI Codex can use

URL: https://developers.openai.com/codex/use-cases/agent-friendly-clis
Source: OpenAI Developers
Captured at: 2026-04-12
Capture note: supporting source fetched from the linked web page in `blog/2026-04-12-bespoke-clis-for-codex/2026-04-12-bespoke-clis-for-codex.md`

## Page Metadata

- Title: Create a CLI Codex can use | Codex use cases
- Description: Ask Codex to create a composable CLI it can run from any folder, combine with repo scripts, use to download files, and remember through a companion skill.
- Estimated duration shown on page: 1h

## Best For

- repeated work where Codex needs to search, read, download from, or safely write to the same service, export, local archive, or repo script
- agent tools that need paged search, exact reads by ID, predictable JSON, downloaded files, local indexes, or draft-before-write commands

## Core Framing

- When Codex keeps using the same API, log source, export, local database, or team script, give that work a composable interface it can run from any folder and combine with `git`, `gh`, `rg`, tests, and repo scripts.
- Add a companion skill that records when Codex should use the CLI, what to run first, how to keep output small, where downloaded files land, and which write commands need approval.
- Use `$cli-creator` to build the CLI and `$skill-creator` to create the reusable companion skill.

## Recommended CLI Jobs

- download failed CI logs from a build URL
- search support exports and read one ticket by ID
- query an admin API
- read a local database
- run one step from an existing team script

## Recommended Command Surface Patterns

- start from the job to be done, not from the implementation technology
- prefer discovery/list/search commands plus exact read commands by stable ID
- keep large payloads in files and return paths instead of dumping huge blobs inline
- separate setup, discovery, download, draft, upload, poll, and live write into distinct commands
- make auth failure obvious without pasting secrets into the thread

## Verification Expectations

- the installed command should work from outside the CLI source folder
- `--help` should explain the main commands
- setup and auth checks should run successfully
- at least one safe discovery or search command should work
- at least one exact read command should work using an ID from discovery
- any large payload should write to a file and return the path
- live write commands should not run without explicit approval
