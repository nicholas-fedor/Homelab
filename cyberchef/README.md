# Nick's Homelab - Cyberchef

[Return to Home](/README.md)

## Description

Another Swiss army knife of miscellaneous tools.
This is a simple application to run via Docker compose.

## URL

<https://cyberchef.nickfedor.dev/>

## Source Respository

<https://github.com/gchq/CyberChef>

## Setup

This application is relatively simple to setup via Docker.

## Integrations

### Traefik

Since I am using Traefik as a reverse proxy, I am using labels to add the
routing, TLS certificate, and middleware.

Just be sure to include the `proxy` network to link the two applications together.

### Authentik

CyberChef does not have built-in authentication.  
Use Authentik's forward proxy provider by adding the Authenik middleware to the
Traefik route:

```docker-compose.yml
labels:
...
  - traefik.http.routers.cyberchef.middlewares=authentik@file
...
```

----------
