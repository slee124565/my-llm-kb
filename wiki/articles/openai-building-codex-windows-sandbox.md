# Building a Safe, Effective Sandbox to Enable Codex on Windows

## Source

- URL: https://openai.com/index/building-codex-windows-sandbox/
- Author: David Wiesen, OpenAI
- Published: 2026-05-13
- Captured: 2026-05-17
- Raw file: `raw/sources/2026/2026-05-13-openai-building-codex-windows-sandbox.md`

## Main Claims

- Codex on Windows needed an OS-enforced sandbox because the default product contract lets the agent read broadly, write inside the workspace, and block internet access unless explicitly enabled.
- Existing Windows primitives did not map cleanly to "agent operates like a developer": AppContainer was too narrow, Windows Sandbox was too detached from the user's real checkout and unavailable on Windows Home, and MIC labels changed the trust semantics of the real workspace too broadly.
- The unelevated prototype used synthetic SIDs plus write-restricted tokens to make writes pass both the normal user check and a sandbox-specific ACL check, but its network suppression was only advisory.
- Strong network blocking required moving from environment-variable suppression to Windows Firewall rules, which in turn required commands to run as a separate Windows principal.
- The final elevated sandbox composes multiple pieces: setup binary, dedicated online/offline sandbox users, DPAPI-protected local credentials, firewall rules, read ACL preparation, command-runner binary, restricted tokens, and child process execution.
- The key design lesson is that coding-agent security is not classic app sandboxing; the sandbox must enforce real boundaries while preserving enough compatibility for arbitrary developer workflows.

## Why It Matters

This article gives a concrete implementation-level view of what "sandboxed coding agent" actually means on a developer laptop. It turns Codex security from a product phrase into a set of OS-level contracts: process tree containment, filesystem write boundaries, network suppression, user/principal separation, setup-time privilege crossing, and command-runner responsibility.

For this KB, the most useful point is the tradeoff shape: safe autonomous coding agents need boundaries that are enforced by the host OS, but those boundaries cannot be so detached from the real checkout and toolchain that the agent stops being useful.

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Codex Workflows](../maps/codex-workflows.md)
- [Introducing Codex](introducing-codex.md)
- [Running Codex safely at OpenAI](https://openai.com/index/running-codex-safely/)

## Tensions Or Disagreements

- The final Windows design improves enforcement but reintroduces an elevated setup step, dedicated local users, credentials, asynchronous ACL work, and multiple binaries; the safety boundary is stronger, but operational complexity becomes part of the product surface.
- The article frames ACL installation and read-access preparation as necessary for usefulness, but this also means local setup state becomes harder to audit than a disposable VM boundary.
- The sandbox is built around developer-machine compatibility. That is appropriate for Codex CLI / IDE / desktop workflows, but the same design may not transfer cleanly to hosted, remote, or browser-operated agent surfaces.

## Open Questions

- How should Codex expose the state and health of Windows sandbox setup so users can understand whether firewall rules, sandbox users, and ACL preparation are still correct?
- Which sandbox setup artifacts should be repairable automatically, and which should require explicit human approval because they touch host security state?
- Can repo-local agent workflows define a portable sandbox contract that abstracts over Seatbelt, seccomp/bubblewrap, and this Windows-specific design without hiding important security differences?
- How should local sandbox logs, setup receipts, and command-runner evidence be preserved for debugging without becoming another sensitive local state surface?

## Merge Candidates

- Coding-agent sandboxes need OS-enforced process-tree boundaries, not only model policy or environment-variable conventions.
- "Safe enough" for coding agents means both containment and developer-workflow compatibility; isolation that cannot touch the real checkout is often the wrong product shape.
- Windows forced Codex to split sandboxing into setup, principal selection, command running, filesystem write ACLs, and firewall enforcement.
- Network suppression is load-bearing: advisory proxy poisoning can reduce accidental access, but adversarial or socket-level traffic requires stronger enforcement.
- Sandbox setup is its own runtime surface and should not be hidden inside the normal agent harness binary.
