# Nick's Homelab - SearXNG

[Return to Home](/README.md)

## Description

Private metasearch engine.

## URL

<https://searxng.nickfedor.dev/>

## Documentation

### Source Website

<https://github.com/searxng/searxng>

### Image Source

<https://hub.docker.com/r/searxng/searxng>

### Supplemental Repository

<https://github.com/searxng/searxng-docker>

## Integrations

### Traefik

- Forwarding port 8080
- Applying SSL certificate
- Enabling Authentik middleware

### Authentik

- Forward auth via Traefik middleware

## Notes

- Using Traefik, so the suggested compose file that includes Caddy is amended
  accordingly.
- I am running into a timeout issue during searches. Temporarily switching over
  to using a SearXNG instance hosted via TrueNAS until this is resolved.

----------
