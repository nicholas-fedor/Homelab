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

## Setup

- If using Traefik as a forward proxy, copy the files over from the relevant
  portion of my GitHub.

  > <https://github.com/nicholas-fedor/Homelab/tree/main/searxng>

  Otherwise, you can always reference the "Official" Docker repo:

  ```console
  git pull https://github.com/searxng/searxng-docker.git searxng
  ```

- Enter the `searxng` directory that was just pulled:

  ```console
  cd searxng
  ```

- Update the `SEARXNG_HOSTNAME` field in the `.env` file with the host's FQDN

- Generate and add a `secret_key` to the `settings.yml` file:

  ```console
  openssl rand -hex 32
  ```

- If using my repo as a reference, then these things should be straightforward.

- Run the Docker Compose file to start:

  ```console
  docker compose up -d
  ```

- If you're having issues, you can always look at the logs to help assist with
  troubleshooting:

  ```console
  docker compose logs
  ```

## Integrations

### Traefik

- Removes need for Caddy
- Forwarding port 8080
- Applying SSL certificate

## Notes

- Using Traefik, so the suggested compose file that includes Caddy is amended
  accordingly.

- See my [note](../Notes.md#searxng-timeouts) regarding a persistent issue with timeouts that I was facing.

----------
