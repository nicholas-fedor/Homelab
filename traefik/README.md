# Nick's Homelab - Traefik

[Return to Home](/README.md)

## URL

<https://traefik-dashboard.nickfedor.dev/dashboard/#/>

## Description

Reverse proxy to handle SSL encryption and allow application resolution without
having to remember port numbers of specific applications.

## Source Repository

<https://github.com/traefik/traefik>

## Documentation

<https://doc.traefik.io/traefik/>

## Setup

Setup using [Techno Tim's
Tutorial](https://technotim.live/posts/traefik-3-docker-certificates/).

### Authentik Integration

[Forward Authentication Documentation](https://docs.goauthentik.io/docs/providers/proxy/server_traefik)

Authentik was added as a middleware by using a separate configuration file
`middleware-authentik.yml`.
To add forward authentication to an application, use the the following label:

```docker-compose.yml
...
labels:
  - traefik.http.routers.[application].middlewares=authentik@file
...
```

## Notes

- When initially setup, I had the application running directly on the Ubuntu
  host; however, moved it to use the Truenas NFS share for data storage.  
  This led to an issue with NFS permissions on the `acme.json` certificate file.  
  Resolved by setting Truenas NFS to have the file as root and also chmod 600
  permissions.

- While `traeik.yml` is the primary configuration used to get the application
  started, I opted to setup a `conf` subdirectory to store additional
  configuration files.  
  This enables Traefik to add additional configuration items without requiring a
  restart.

- Traefik uses Lego for obtaining certificates. When using Cloudflare as a DNS
  provider, it's only necessary to provide an API token to obtain SSL certs.

----------
