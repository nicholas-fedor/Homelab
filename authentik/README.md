# Nick's Homelab - Authentik

[Return to Home](/README.md)

## Description

Authentication provider to secure the homelab behind both password and TOTP authentication.

## URL

<https://authentik.nickfedor.dev>

## Source Repository

<https://github.com/goauthentik/authentik>

## Documentation

<https://docs.goauthentik.io/docs/>

## Setup

- Used [Christian Lempa's YouTube
  Tutorial](https://www.youtube.com/watch?v=N5unsATNpJk)

- Used the developer's recommendation of starting with their baseline Docker
  Compose file, obtained via:

  ```console
  wget https://goauthentik.io/docker-compose.yml
  ```

### Environment Variables

See the `.env.sample` file.

To generate a password and secret key, the [documentation](https://docs.goauthentik.io/docs/installation/docker-compose) references the
following commands:

```console
echo "PG_PASS=$(openssl rand -base64 36 | tr -d '\n')" >> .env
echo "AUTHENTIK_SECRET_KEY=$(openssl rand -base64 60 | tr -d '\n')" >> .env
```

## Integrations

### Proxmox VE

- Link: <https://docs.goauthentik.io/integrations/services/proxmox-ve/>

- Documentation advises to use the url:port combination; however, I opted to use
the Traefik proxy url without issue.

### [Gitea](https://docs.goauthentik.io/integrations/services/gitea/)

- Link: <https://docs.goauthentik.io/integrations/services/gitea/>

- Currently unable to implement due to a DNS-related issue.

> The container is unable to resolve `https://authentik.nickfedor.dev`; however,
  is able to find `authentik-server:9000` when attempting to obtain the `OpenID
  Connect Auto Discovery URL`.

- Opting to use the forward auth provider for the time being and Gitea's
  built-in auth.

### [FreshRSS](https://docs.goauthentik.io/integrations/services/freshrss/)

- Link: <https://docs.goauthentik.io/integrations/services/freshrss/>

- I suspect the same DNS-related issue is preventing me from implementing OIDC
  integration.
- Using forward auth for the time being.

## Notes

- Deployment includes the addition of a middleware for Traefik. The file is
  named `authentik.yml`.
- As detailed above, there is a DNS-related issue that's creating some issues
  with containers resolving `authentik.nickfedor.dev`.  
  I have yet to determine a suitable solution to this, such as possibly adding a
  DNS-related option within the Docker Compose file.
- I am interested in trying to get Docker secrets to work for the `.env`
  configuration items.
  This is something that I will delve into at a later time.

----------
