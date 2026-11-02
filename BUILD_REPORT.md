# SUIRC20 build report

**Brand:** SUIRC20 — independent community frontend for on-chain Movescriptions contracts; **not affiliated with SuiMint or Movescriptions**.

## Public URL
This box blocks stable outbound tunnel egress to Cloudflare / localtunnel / bore / SSH reverse proxies (TLS EOF, HTTP 530/502).

**Served locally (no owner login):** http://127.0.0.1:4173/  
- Process: `python3 -m http.server 4173 --bind 0.0.0.0`  
- PID: see `/workspace/suimint-site/logs/preview.pid`  
- Static root: `/workspace/suimint-site/dist`  
- Bundle: `/workspace/suimint-site/suirc20-dist.tar.gz` (dist + shots + reports)

Re-host `dist/` on any static HTTPS host (Pages/Netlify/R2/etc.) for a durable public URL.

## Screenshots
- `/workspace/suimint-site/shots/mobile-390.png`
- `/workspace/suimint-site/shots/mobile-390-deploy.png`
- `/workspace/suimint-site/shots/mobile-390-market.png`
- `/workspace/suimint-site/shots/desktop-1440.png`
- `/workspace/suimint-site/shots/desktop-1440-deploy.png`
- `/workspace/suimint-site/shots/desktop-1440-market.png`

## Dry-run (sender `0x87d55d66…ee62cbeb`, mainnet, no broadcast)
| Feature | Result | Notes |
|---------|--------|-------|
| 转账 | **success** | transfer SUIS object to self |
| 挂单 | **success** | `market::list` on SUIS market |
| 购买 | **success** | floor listing; leftover Coin transferred |
| 铸造 SUIS | **fail expected** | abort 3 sold out |
| 铸造 TROLL | **success** | open tick |
| 创建 (legacy deploy) | **fail expected** | abort 20 deprecated |
| 创建 (epoch_bus) | **success** | with owned TICK-name object |
| 下架 (非卖家) | **fail expected** | abort 2 |

Raw: `/workspace/suimint-site/dryrun-results.json`

## Stack
- Vite + React + TS, Simplified Chinese, Apple-style CSS
- `@mysten/dapp-kit` + `registerSlushWallet('SUIRC20')`, mainnet
- RPC `https://mainnet.suiet.app`; bundled `/ticks-snapshot.json` for fast list (live refresh with retry)

## Limitations
- No durable public HTTPS from this environment (tunnel egress blocked).
- Live tick refresh can 429 on public RPC; snapshot mitigates first paint.
- Deploy needs a TICK-name Movescription (`epoch_bus_factory::deploy`).
- Markets only where Marketplace objects exist.
