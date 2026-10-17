# Slerf Terminal — Solana Meme Coin Trading Terminal

React + TypeScript frontend for a self-custody Solana Mainnet trading terminal. This is an initial working foundation, not a fully completed trading product.

## Implemented in this version

- Dark SlerfTools-inspired responsive desktop-first interface.
- Phantom and Solflare wallet connection through Solana Wallet Adapter.
- Live SOL balance for the connected wallet and live read-only SOL balances for up to seven saved public addresses.
- Jupiter quote request and swap transaction construction.
- Wallet approval required for swaps; transaction status and Solscan link shown in session history.
- Basic slippage selection and pre-swap quote review.
- Settings page with RPC connection test.
- Honest placeholders for token launch, Snipe, bundles, and analytics features not yet integrated.

## Important limitations

- **Only the currently connected wallet can sign a swap.** The seven-address list is read-only. A connected Phantom wallet does not grant authority over other addresses. To trade from each address, connect each wallet individually through a compatible signer flow; no private key import or seed phrase collection is implemented.
- Token launch, Snipe automation, bundles, historical analytics, token holdings and Sell All & Consolidate are not implemented in this first iteration.
- The Overview watchlist prices are clearly marked as illustrative, not live. Never use them for a trade decision.
- Jupiter API access and rate limits can change. Check current Jupiter documentation before production deployment.
- The public Solana RPC is for development and may be rate limited. Configure a dedicated RPC endpoint for serious use.
- A successful wallet submission is not a guarantee of execution; the app waits for confirmation and records failures.
- This client-only app cannot safely hide a secret API key. Do not put server-only credentials into `VITE_*` variables. If a provider requires a secret, use a backend proxy.

## Requirements

- Node.js 20 or newer recommended.
- npm.
- A supported Solana wallet browser extension such as Phantom.
- Internet access for RPC and Jupiter API calls.

## Run locally

1. Unzip the project.
2. Open a terminal in the project folder.
3. Install packages:

   ```bash
   npm install
   ```

4. Copy `.env.example` to `.env.local`.
5. Set `VITE_SOLANA_RPC_URL` to your RPC endpoint. The public Mainnet endpoint is a fallback, but it is not recommended for sustained use.
6. If needed, set `VITE_JUPITER_API_BASE` and `VITE_JUPITER_API_KEY` according to your current Jupiter plan. Do not put a secret credential in the frontend.
7. Start development:

   ```bash
   npm run dev
   ```

8. Open the local URL printed by Vite, usually `http://localhost:5173`.
9. Connect Phantom. Test reads first. For any real swap, verify the token mint, quote, minimum output, fees and the wallet's signing prompt.

## Validate build

```bash
npm run check
npm run build
```

## Upload to GitHub

1. Create an empty repository on GitHub.
2. Extract this ZIP.
3. In the project folder, initialize and push:

   ```bash
   git init
   git add .
   git commit -m "Initial Slerf Terminal foundation"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
   git push -u origin main
   ```

4. Never commit `.env.local`. `.gitignore` excludes it.

## Deployment

This is a Vite static frontend and can be deployed to a static host that supports Node-based builds. Set environment variables in the host's build settings. Remember that all `VITE_*` values are included in browser assets and are public. For private API credentials, add a backend proxy rather than exposing them in the frontend.

## Safety checklist

- Never enter seed phrases or private keys into this application.
- Verify mint addresses using a trusted explorer or issuer source.
- Review every transaction in your wallet before approving it.
- Keep enough SOL for fees and rent.
- Start with small amounts and understand slippage and liquidity risks.
- This software is provided as-is and is not financial advice.
