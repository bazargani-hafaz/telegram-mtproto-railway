# Telegram MTProto Proxy on Railway

A minimal Docker-based MTProto proxy deployment for Railway using the official Telegram MTProxy image.

## Deploy on Railway

1. Create a new Railway project.
2. Choose **Deploy from GitHub Repo** and select this repository.
3. Deploy the service.
4. Add a Railway Volume mounted at `/data` so the generated proxy secret persists across redeploys.
5. Configure the service to expose a TCP port. Use the public TCP endpoint/port assigned by Railway.

## Environment variables

No secret needs to be committed to GitHub. The official image can generate its configuration/secret on first startup and persist it in `/data` when a volume is attached.

If you prefer to provide a secret explicitly, configure it as a Railway environment variable according to the current MTProxy image documentation rather than committing it to this repository.

## Important Railway note

MTProto is a TCP proxy. A normal Railway HTTP public domain is not a substitute for a TCP endpoint. The Telegram client must use the public TCP host and port exposed by Railway.

## Telegram proxy link

After deployment, inspect the service logs for the generated secret/configuration. Build the Telegram link using:

`tg://proxy?server=YOUR_TCP_HOST&port=YOUR_TCP_PORT&secret=YOUR_SECRET`

Do not publish the secret publicly. Anyone who has the proxy secret and endpoint can use the proxy.

## Image

This project uses:

`telegrammessenger/proxy:latest`

For production use, consider pinning a specific image tag/digest after testing.
