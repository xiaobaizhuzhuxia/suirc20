# SUIRC20 hosting

- Static build: `/workspace/suimint-site/dist`
- Local preview: `npx vite preview --host 0.0.0.0 --port 4173` (PID in logs/preview.pid)
- Public URL: Cloudflare quick tunnel `cloudflared tunnel --url http://127.0.0.1:4173`
- URL file: `PUBLIC_URL.txt`

## Persistence limits
- Quick tunnels (`*.trycloudflare.com`) are **ephemeral**: no uptime SLA, URL changes when cloudflared restarts, may idle-disconnect.
- Processes started with `nohup` survive the agent turn but die if the box reboots or processes are killed.
- No owner login required for hosting.

## Brand
Site title/brand: **SUIRC20**. Independent community frontend; not affiliated with SuiMint or Movescriptions.
