# P256 Verifier

**Verify passkey signatures on Ethereum mainnet — now live with Fusaka.**

[Live Demo](https://your-deployed-url.vercel.app) · [EIP-7212](https://eips.ethereum.org/EIPS/eip-7212)

---

## What This Proves

With Fusaka (Dec 3, 2025), Ethereum gained native P-256 signature verification at `0x0100`. This demo shows the full flow:

1. **Generate** — Mint a P-256 keypair using Web Crypto (same curve as Face ID, YubiKeys)
2. **Sign** — ECDSA-sign any message you type
3. **Verify** — Call the precompile on mainnet and get a result in ~3,450 gas

Before Fusaka, this cost **200,000+ gas** in Solidity. Now it's a single precompile call.

## Why It Matters

| Use Case | Benefit |
|----------|---------|
| **Passkey Wallets** | Smart accounts can verify Face ID / Touch ID signatures on-chain |
| **WebAuthn Login** | Seedless authentication becomes gas-efficient |
| **Hardware Keys** | YubiKey and FIDO2 devices work natively with Ethereum |

## Quickstart

```bash
git clone https://github.com/omarespejel/p256-verifier

cd p256-verifier/frontend

bun install

bun run dev
```

Requires [Bun](https://bun.sh) 1.1+ and a secure context (HTTPS or `localhost`).

## Configuration

Override the default RPC endpoints via environment variables:

```bash
VITE_RPC_MAINNET=https://eth.llamarpc.com

VITE_RPC_SEPOLIA=https://rpc.sepolia.org

VITE_RPC_HOLESKY=https://ethereum-holesky.publicnode.com
```

## Deploy

```bash
bun run build
```

Ship `frontend/dist/` to Vercel, Netlify, or any static host.

## Reuse the Helpers

`src/p256.ts` exports everything you need:

```ts
import { verifyOnChain, buildCalldata } from './p256'

const result = await verifyOnChain({
  messageHash: '0x...',
  r: '0x...', s: '0x...',
  pubX: '0x...', pubY: '0x...'
})

console.log(result.valid, result.gasUsed) // true, 3450n
```

## References

- [EIP-7212: Precompile for secp256r1](https://eips.ethereum.org/EIPS/eip-7212)
- [Fusaka Upgrade](https://ethereum.org/roadmap/fusaka/)
- [WebAuthn Spec](https://www.w3.org/TR/webauthn/)

---

Built by [@espejelomar](https://x.com/espejelomar), Developer Advocate at [Starknet Foundation](https://starknet.io).

If this helps you, ⭐ the repo or follow on X!

