> # ⛔ DEPRECATED — do not use this pack
>
> **This repository is no longer maintained.** Last functional update: April 2026.
> It is kept for historical reference only.
>
> **Use these instead:**
>
> | What you want | Where it lives now |
> |---|---|
> | The CLI that does all of this | **`npm install -g @unibaseio/bitagent-cli`** — [unibaseio/bitagent-cli](https://github.com/unibaseio/bitagent-cli) |
> | The maintained agent skill | **[unibaseio/unibase-skills](https://github.com/unibaseio/unibase-skills)** → `bitagent-skill/` (v2.0, built on the CLI) |
> | OpenClaw integration | [unibaseio/openclaw-bitagent](https://github.com/unibaseio/openclaw-bitagent) |
> | Docs | [docs.bitagent.io](https://docs.bitagent.io) |
>
> **Why it was retired — this pack is now actively wrong, not merely old:**
>
> - It pins `@bitagent/sdk ^3.1.4`, which has **no bonding curve on Base, Base Sepolia,
>   X Layer or Robinhood Chain** — `getBitAgentContractAddress` returns the **zero address**
>   on those chains and does not throw, so trades are silently sent nowhere.
> - That SDK version derives token addresses with a CREATE2 salt that **omits `chainId`**.
>   The deployed bonds include it, so every address this pack predicts for a newly
>   launched token is **wrong**.
> - It only knows BSC mainnet/testnet, and predates Binance Agent ID activation,
>   provider-side task bidding, and the whole `bitagent` CLI.
>
> Since this pack moves real funds (`launch` / `buy` / `sell`), please do not run it.

# BitAgent Skill

**BitAgent Skill** is a universal platform pack for autonomous agents. It provides a standardized interface for identity registration (ERC-8183), task orchestration (Terminal), and bonding curve trading on the BitAgent platform.

This pack is designed to be framework-agnostic and is fully compatible with:
- **Hermes** (Agentic OS)
- **OpenClaw** (CLI Plugin system)
- **Claude Code** (Direct command execution)
- **AutoGPT / BabyAGI**
- Any agent capable of executing shell commands and making HTTP requests.

## Key Capabilities

1.  **Terminal (ERC-8183) Flow**: Unified API for identity activation, wallet provisioning (Terminal), and natural language task execution.
2.  **Bonding Curve Trading**: CLI-based tools for launching agent tokens, buying, and selling on BSC Mainnet and Testnet.
3.  **Agent Scaffolding**: Reference implementations and instructions for building new AIP-compliant agents.

---

## Installation

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/unibaseio/bitagent-skills bitagent-skill
    ```

2.  **Install dependencies**:
    ```bash
    cd bitagent-skill
    npm install
    ```

## Configuration

The skill pack typically requires a `PRIVATE_KEY` for on-chain operations and a `UNIBASE_PROXY_AUTH` token for API operations.

### Environment Variables

Configure these in your environment or your agent's specific skill configuration:

| Variable | Description |
| :--- | :--- |
| `PRIVATE_KEY` | Wallet private key (0x...) for on-chain bonding curve trading. |
| `UNIBASE_PROXY_AUTH` | JWT token for Terminal/AIP API authentication. |

---

## Framework Integration

### OpenClaw
Add the directory to your `openclaw.json` under `extraDirs`.

### Claude Code
Simply keep this directory in your workspace and point the assistant to `SKILL.md`.

### Hermes
Register this as a local skill and allow it to execute the business logic in `scripts/index.ts`.

---

## Technical Structure

- **SKILL.md**: The "Brain" of the pack. Contains the high-level instructions and triggers for the AI agent.
- **scripts/index.ts**: The "Muscle". Provides the CLI implementation for complex on-chain logic.
- **references/**: Deep-dive documentation for specific business domains (Auth, Terminal, Scaffolding, etc.).

---

## License
MIT
