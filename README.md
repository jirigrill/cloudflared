# Cloudflare Tunnel Docker Setup

This project provides a Docker-based setup for running a Cloudflare Tunnel, allowing you to securely expose your local services to the internet without opening inbound ports.

## Prerequisites

- Docker and Docker Compose installed on your system
- A Cloudflare account
- A valid Cloudflare Tunnel token

## Project Structure

```
.
├── .env                    # Environment variables file containing the tunnel token
└── docker-compose.yml      # Docker Compose configuration file
```

## Configuration

### Environment Variables

Create a `.env` file in the project root with your Cloudflare Tunnel token:

```env
CLOUDFLARE_TUNNEL_TOKEN=your-tunnel-token
```

⚠️ **Security Note**: Keep your tunnel token secure and never commit it to version control.

### Docker Compose

The `docker-compose.yml` file configures the Cloudflare tunnel service:

```yaml
version: '3'

services:
  cloudflared:
    image: cloudflare/cloudflared:latest
    command: tunnel --no-autoupdate run --token ${CLOUDFLARE_TUNNEL_TOKEN}
    restart: unless-stopped
```

## Usage

1. Start the tunnel:
   ```bash
   docker-compose up -d
   ```

2. Check the tunnel status:
   ```bash
   docker-compose logs cloudflared
   ```

3. Stop the tunnel:
   ```bash
   docker-compose down
   ```

## Features

- Automatic tunnel reconnection with `restart: unless-stopped`
- No manual port forwarding required
- Secure connection using Cloudflare's network
- Auto-updates disabled for stability

## Troubleshooting

If you encounter issues:

1. Verify your tunnel token is correct
2. Check the container logs for errors
3. Ensure your Cloudflare account has the necessary permissions
4. Confirm Docker and Docker Compose are properly installed

## Security Considerations

- Store the `.env` file securely and add it to `.gitignore`
- Regularly rotate your tunnel token
- Monitor tunnel access logs for suspicious activity
- Keep the cloudflared image updated for security patches

## License

This project configuration is released under the MIT License. The Cloudflare tunnel software has its own licensing terms.
