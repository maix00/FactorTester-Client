# FactorTester Client

This history-clean public repository contains the remote FactorTester CLI,
optional research Agent Harness, macOS application, and signed local adapter
contracts. It does not contain the FactorTester server, data access,
backtesting implementation, database repositories, or private factor source.

## Install

Download the client wheel and release profile from the latest GitHub Release.
Then inspect the signed installation plan before applying it:

```bash
python -m pip install factortester-0.1.2-py3-none-any.whl
factortester client bootstrap --profile client-profile.json --dry-run --json
factortester client bootstrap --profile client-profile.json --json
```

The release profile contains only a manifest URL and local install path. The
trusted ECDSA public key is fixed inside the wheel. Every downloaded artifact
is bound to its size, SHA-256 digest, source revision, and compatible protocol
range.

See [installation, update, and recovery](docs/client-release.md).

## Use

Configure a FactorTester server, then log in interactively:

```bash
factortester configure --base-url https://factor.example
factortester login --username <account> --keep-login
factortester protocol negotiate
```

`--keep-login` lets later local Agent processes reuse the authenticated
session. `factortester logout` removes it.

The macOS SwiftUI client uses the same release and profile contracts. It embeds
server pages and signed local-adapter Web interfaces with `WKWebView`.
Vibe-Trading remains a separate loopback process managed by the local adapter
manager; no service port is hardcoded in SwiftUI.

## Local research Agents

The optional Harness follows CLI-Anything conventions and progressively loads
research capability descriptions. Skill bodies are loaded only when needed,
and Skill execution still requires the applicable approval. Local audit
records identify the actual Skill used without creating a server-side Skill
registry.

The settings UI manages the human profile and provider-neutral Agent profiles,
but does not perform approvals. Research, Skill, graph-change, and backend-gap
approvals remain in the corresponding Agent conversation.

## Privacy

Client reinstall and rollback touch only versioned paths named in the signed
release receipt. They do not delete or upload databases, market data, factor
workspaces, Keychain items, research memory, source code, formulas, or
expression trees.

The public artifacts are tested to exclude server modules, developer paths,
private identifiers, source data, backend execution code, and Harness tests.

## Build

Generate the Xcode project and verify a macOS Release build:

```bash
./script/build_and_run.sh --verify
```

Python packages are defined by `tools/cli/pyproject.toml` and
`tools/cli/agent-harness/pyproject.toml`. Release signing is intentionally
performed in the private server release environment; no private signing key or
release-author tooling exists in this repository.
