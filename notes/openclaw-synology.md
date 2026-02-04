# OpenClaw on Synology NAS

## Setup Summary

- **Host**: 192.168.0.100 (Synology NAS)
- **SSH**: flapsi84@192.168.0.100
- **Path**: /volume2/docker/openclaw/
- **Telegram Bot**: @claw22982bot
- **AI Provider**: Groq (free tier)
- **Model**: groq/llama-3.3-70b-versatile
- **Gateway URL**: https://192.168.0.100:18789

## Key Files

- `/volume2/docker/openclaw/data/Dockerfile` - Custom build with Playwright skip
- `/volume2/docker/openclaw/data/docker-compose.yml` - Service definitions
- `/volume2/docker/openclaw/data/.env` - Environment variables
- `/volume2/docker/openclaw/config/openclaw.json` - OpenClaw state/config

## Important Notes

1. **Playwright Skip**: Added `ENV PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD=1` to Dockerfile (line 23)
2. **Permissions**: Config dir must be owned by UID 1000 (node user)
3. **TLS**: Self-signed certificate enabled for HTTPS
4. **Auth Mode**: Token-based authentication

## Useful Commands

```bash
# View logs
sudo docker-compose logs -f openclaw-gateway

# Restart services
sudo docker-compose down && sudo docker-compose up -d

# Run CLI commands
sudo docker-compose exec openclaw-gateway npx openclaw <command>

# Check config
sudo docker-compose exec openclaw-gateway npx openclaw config get

# Approve Telegram pairing
sudo docker-compose exec openclaw-gateway npx openclaw pairing approve telegram <CODE>
```

## Available Groq Models

- groq/llama-3.3-70b-versatile (current)
- groq/llama-4-maverick-17b
- groq/llama-4-scout-17b
- groq/deepseek-r1-distill-llama-70b
- groq/qwen-qwq-32b
