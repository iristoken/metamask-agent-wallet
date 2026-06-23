# MetaMask Agent Wallet

> A self-custodial wallet that lets AI agents trade onchain — inside guardrails you control.

[![Status](https://img.shields.io/badge/status-early%20access-orange)]()
[![License](https://img.shields.io/badge/license-MIT-blue)]()
[![Chains](https://img.shields.io/badge/chains-25%2B%20EVM%20%2B%20Hyperliquid-purple)]()
[![Built by](https://img.shields.io/badge/built%20by-Consensys-black)]()

MetaMask Agent Wallet is a self-custodial AI trading wallet that lets an AI agent execute DeFi
transactions — swaps, perpetual futures, prediction markets, staking, and liquidity provision —
across EVM-compatible chains, while every transaction passes through a mandatory security pipeline.
You keep custody of your keys and define the rules; the agent operates strictly within them.


## Why this exists

AI agents are increasingly trading and managing capital on behalf of their users. Most existing
options force a tradeoff: centralized-exchange agent wallets often hold your keys and keep your
agent locked to a single venue, while many self-custody agent wallets treat transaction security
as optional.

MetaMask Agent Wallet aims to be the wallet that is **self-custodial, multi-chain,
framework-agnostic, and ships with mandatory transaction security on every move** — reusing the
same security stack that has been production-tested across millions of human MetaMask transactions.

---

## Key features

- **Self-custodial.** You control the secret recovery phrase. Export it once and walk away at any time.
- **Multi-chain.** One wallet and one CLI for trades across 25+ EVM chains and Hyperliquid.
- **Framework-agnostic.** Output is structured JSON that any LLM can parse. Plugs into existing agent setups without changing your core toolset.
- **Guardrails you set.** Daily spend limits, allowlisted protocols, and a risk profile, defined at setup.
- **Mandatory security pipeline.** Every supported transaction is simulated, threat-scanned, and MEV-protected before it can execute.
- **Human-in-the-loop.** Transactions that fall outside policy or get flagged as malicious are routed to you for approval via email or mobile push (2FA).
- **Transaction Protection.** Eligible safe transactions are covered up to **$10,000/month** against losses (subject to program terms and conditions).

---

## Operating modes

You choose how much friction the agent runs with:

| Mode | What it does | Best for |
| --- | --- | --- |
| **Guard Mode** (default) | Trades only with allowlisted protocols, enforces daily spend limits, requires 2FA on anything outside policy. | Most users; tighter control. |
| **Beast Mode** (opt-in) | Reduces approval prompts for faster execution, but still routes potentially malicious transactions to human review. | Experienced traders who want speed. |

In both modes, permissions are built on MetaMask's Advanced Permissions / delegation system, letting
you define asset, amount, and time-window limits per agent — with wallet-native approval and
revocation at any time.

---

## The security pipeline

Every supported transaction the agent initiates passes through three steps before execution:

1. **Transaction simulation** — surfaces what the transaction will actually do (balance changes, approvals, gas route) before signing.
2. **Threat scanning** — powered by Blockaid; malicious transactions are auto-rejected.
3. **MEV protection** — via Smart Transactions, to reduce value lost to front-running and sandwiching.

> **Note:** Blockaid threat scanning applies to supported chains, including Ethereum, Linea,
> Arbitrum, Avalanche, Optimism, Base, Polygon, BNB Chain, and Sei. Coverage may differ by chain.

---

## Supported agent frameworks

MetaMask Agent Wallet is designed to fit into the tools you already use:

- Claude Code
- OpenAI Codex
- OpenClaw
- Nous Research Hermes Agent
- OpenCode
- Cursor

Because the wallet returns structured JSON, any LLM-based framework that can parse JSON can
integrate with it.

---

## Getting started

> The exact setup flow depends on the early-access onboarding and your chosen framework. The
> high-level flow is the same across integrations.

1. **Request early access.** Apply through the [MetaMask Agent Wallet site](https://metamask.io/agent-wallet).
2. **Install the CLI and the skill** for your preferred agent framework.
3. **Configure your guardrails** — daily spend limits, allowlisted protocols, and risk profile.
4. **Pick a mode** — Guard Mode or Beast Mode.
5. **Hand the work to your agent** — ask it to research opportunities and execute trades. MetaMask simulates, scans, and MEV-protects every transaction along the way.

### Example: install the OpenClaw skill

```bash
openclaw skill install metamask-agent-wallet-skill
```

Once installed, the skill is available in your OpenClaw conversations automatically — describe what
you want to do and the agent invokes it when relevant.

### Example: configuring guardrails (illustrative)

```jsonc
{
  "mode": "guard",
  "dailySpendLimitUsd": 500,
  "allowlistedProtocols": ["uniswap", "aave", "hyperliquid"],
  "riskProfile": "conservative",
  "approval": {
    "channel": "push",        // or "email"
    "require2faOutsidePolicy": true
  }
}
```

> This config snippet is illustrative — check the official docs for the current schema and CLI flags.

---

## How it differs from other agent wallets

| | MetaMask Agent Wallet | CEX-based agent wallets | Other self-custody agent wallets |
| --- | --- | --- | --- |
| Custody | You hold the keys | Exchange holds keys | You hold the keys |
| Chains | 25+ EVM + Hyperliquid | Usually single venue | Varies |
| Framework support | Agnostic (JSON output) | Limited | Varies |
| Transaction security | Mandatory on every move | Varies | Often optional |

---

## FAQ

**Is it really self-custodial?**
Yes. You control the secret recovery phrase and can export it at any time.

**What happens to a risky transaction?**
Malicious transactions are auto-rejected. Legitimate edge cases that fall outside your policy are
routed to you for approval via email or mobile push.

**Which chains get threat scanning?**
Blockaid-supported chains, including Ethereum, Linea, Arbitrum, Avalanche, Optimism, Base, Polygon,
BNB Chain, and Sei. Other supported EVM chains can still be traded, but scanning coverage varies.

**Is the $10,000 protection guaranteed?**
Coverage of up to $10,000/month applies to eligible safe transactions and is subject to the
Transaction Protection program's terms and conditions.

---

## Disclaimer

This README is an unofficial, community-style overview of MetaMask Agent Wallet for documentation
purposes. It is **not** financial or investment advice. Trading digital assets — especially via
autonomous agents — carries real risk, including total loss of funds. Always review transactions and
program terms yourself. Verify all details against the official MetaMask documentation, as features
in early access can change.

## Links

- Official page: https://metamask.io/agent-wallet
- MetaMask developer docs: https://docs.metamask.io
