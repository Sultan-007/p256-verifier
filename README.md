## P256 Verifier

A lean Bun + Vite app that proves the Fusaka precompile works. It:

- Mints a fresh P-256 keypair with Web Crypto.
- Hashes and signs any sentence you type.
- Builds the `hash || r || s || x || y` calldata required by `0x0100`.
- Calls mainnet through viem and reports gas, block, and latency.

### Requirements
- [Bun](https://bun.sh) 1.1+
- Node.js 22.12+ (`.nvmrc` is included)
- A secure-context browser (HTTPS or `http://localhost`)

### Quickstart
```bash
git clone https://github.com/espejelomar/eip-7951-demo
cd eip-7951-demo/frontend
bun install
bun run dev
```

### Configure RPCs
Public endpoints are baked in, but you can override them:
```
VITE_RPC_MAINNET=https://mainnet.example.org
VITE_RPC_SEPOLIA=https://sepolia.example.org
VITE_RPC_HOLESKY=https://holesky.example.org
```

### Build and Deploy
```bash
bun run build
```
Ship `frontend/dist/` to Vercel, Netlify, or any static host.

### Notes
- Web Crypto needs HTTPS. On insecure origins the “Generate Signature” button stays disabled.
- `src/p256.ts` exports `verifyOnChain` and the calldata helpers if you want to reuse them elsewhere.

Issues and PRs welcome—especially if you want more tests, different copy, or a CLI sidecar again.

Built by [@espejelomar](https://x.com/espejelomar) / [omarespejel](https://github.com/omarespejel). If it helps you, please star the repo or follow on X.

