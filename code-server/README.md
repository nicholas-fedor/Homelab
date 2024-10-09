# Nick's Homelab - VSCode Server

[Return to Home](/README.md)

## Description

VSCode via the browser.

## URL

<https://code.nickfedor.dev/>

## Documentation

### Source Website

<https://coder.com/docs/code-server>

### Image Source

<https://hub.docker.com/r/codercom/code-server>

### Image GitHub Respository

<https://github.com/coder/code-server>

## Integrations

### Traefik

- Forwarding port 8080
- Applying SSL certificate
- Enabling Authentik middleware

### Authentik

- Forward auth via Traefik middleware

## Notes

- On first start, webUI access protected by a generated password that can be found
  via the `./data/config/code-server/config.yaml` file.

- The container includes access to the `Apps` directory for editing of
  configurations.

- While it is possible to enable host access to the Docker daemon, it's a
  significant security lapse without a secured proxy.

----------
