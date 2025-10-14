## BSC Sandwich Bot

A professional-grade sandwiching bot targeting the BNB Smart Chain (BSC). It monitors the mempool via WebSocket, evaluates profitable opportunities, and attempts atomic sandwich trades using configurable risk/return parameters. Optional Telegram notifications keep you informed in real time.

---

### Features
- Real-time transaction stream via WSS
- Configurable profit/slippage/gas parameters
- PancakeSwap router integration
- Telegram bot notifications with whitelisting
- TypeScript client; Foundry-based smart contracts

---

### Repository Structure
```
./
  client/           # TypeScript bot/runner and Telegram integration
  contracts/        # Foundry (Solidity) contracts, scripts, and tests
  LICENSE
  README.md
```

Key client modules:
- `client/src/config/config.ts` – centralized runtime configuration
- `client/src/index.ts` – app entrypoint
- `client/src/core/*` – trading/core logic
- `client/src/helpers/*` – utilities and helpers

---

### Requirements
- Node.js ≥ 18
- Yarn or npm
- A BSC RPC endpoint (HTTPS and WSS)
- A funded private key (for mainnet; use with extreme caution)
- (Optional) Telegram bot token and chat IDs
- For contracts: Foundry (`forge`) installed

---

### Quick Start
1) Clone and install dependencies
```bash
git clone <this-repo-url>
cd sandwicher/client
yarn install   # or: npm install
```

2) Create a `.env` file in `client/`
```bash
# Required
PRIVATE_KEY=0x...
JSON_RPC=https://bsc-dataseed.binance.org
WSS_URL=wss://bsc-ws-node.nariox.org:443

# Optional but recommended
BOT_TOKEN=123456:ABCDEF...         # Telegram bot token
MIN_PROFIT_THRESHOLD=0.003         # 0.3% default if unset
```

3) Configure additional options in `client/src/config/config.ts` if needed:
- `CONTRACT_ADDRESS` – on-chain contract the bot references
- `STABLE_TOKENS` – addresses for tokens considered stable
- `EXPLORER_URL` – chain explorer base URL
- `WHITELISTED_USERS` – Telegram user IDs permitted to receive alerts
- `DEFAULT_GAS_LIMIT`, `GAS_FACTOR`, `MIN_SLIPPAGE_THRESHOLD`, etc.

4) Run the bot (development)
```bash
yarn start   # or: npm run start
```

Tests (client)
```bash
yarn test    # or: npm test
```

---

### Environment Variables (client)
These are read in `client/src/config/config.ts`:
- `PRIVATE_KEY` (required): EOA private key used to sign transactions
- `JSON_RPC` (required): HTTPS RPC endpoint URL
- `WSS_URL` (required): WebSocket endpoint URL for mempool/blocks
- `BOT_TOKEN` (optional): Telegram bot token for notifications
- `MIN_PROFIT_THRESHOLD` (optional): minimum profit ratio; default `0.003`

Security tips:
- Prefer using separate, minimally funded keys
- Consider RPCs with rate limits and IP allowlists
- Never commit `.env`

---

### Contracts (Foundry)
Location: `contracts/`

Prerequisites: Install Foundry. See the official guide.

Common commands (run from `contracts/`):
```bash
forge build
forge test
forge script script/SandWicher.s.sol --rpc-url $JSON_RPC --broadcast --private-key $PRIVATE_KEY
```

Configuration is in `contracts/foundry.toml`.

---

### Development Notes
- The client uses `ethers@5` and `ethereum-multicall`
- Telegram via `telegraf`
- TypeScript build tooling: `ts-node-dev`, `ts-jest` for tests

Scripts (from `client/package.json`):
```bash
yarn start   # ts-node-dev src/index.ts
yarn test    # jest
```

---

### Troubleshooting
- Ensure WSS endpoint is valid and supports mempool subscriptions
- Check the account has enough BNB for gas
- Validate addresses in `config.ts` (WBNB, Router, target contracts)
- Increase `GAS_FACTOR` cautiously if front-running fails
- Inspect logs and Telegram alerts for error details

---

### Contact

| Platform | Link |
|----------|------|
| 📱 Telegram | [t.me/novustch](https://t.me/novustch) |
| 📲 WhatsApp | [wa.me/14105015750](https://wa.me/14105015750) |
| 💬 Discord | [discordapp.com/users/985432160498491473](https://discordapp.com/users/985432160498491473)

<div align="center">
    <a href="https://t.me/novustch" target="_blank"><img alt="Telegram"
        src="https://img.shields.io/badge/Telegram-26A5E4?style=for-the-badge&logo=telegram&logoColor=white"/></a>
    <a href="https://wa.me/14105015750" target="_blank"><img alt="WhatsApp"
        src="https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white"/></a>
    <a href="https://discordapp.com/users/985432160498491473" target="_blank"><img alt="Discord"
        src="https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white"/></a>
</div>

Feel free to reach out for implementation assistance or integration support.

---

### Disclaimer
This software is provided “AS IS”, without warranty of any kind. Use at your own risk. The authors and contributors are not responsible for losses or damages arising from the use of this software.


