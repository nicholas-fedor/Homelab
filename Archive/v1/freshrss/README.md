# Nick's Homelab - FreshRSS

[Return to Home](/README.md)

## Description

RSS feed aggregator and reader

## URL

<https://freshrss.nickfedor.dev/>

## Documentation

### Source GitHub Repository

<https://github.com/FreshRSS/FreshRSS>

### Source Docker Repository

<https://hub.docker.com/r/freshrss/freshrss>

### Forked GitHub Repository

<https://github.com/nicholas-fedor/FreshRSS>

### Nick's Docker Image

<https://hub.docker.com/r/nickfedor/freshrss>

## Build Instructions

The included `Makefile` in my fork of the source repository builds and uploads
the image to Docker Hub, GitHub, and Gitea.

To manually build an image:

```console
docker build --tag=nicholas-fedor/freshrss:latest -f Docker/Dockerfile .
```

## Run instructions

From the `freshrss` directory:

```console
docker compose up -d
```

This will also create a `data` directory for persistance.

## Notes

- This is an application that's intended to be run via a Docker container. It's
developer is currently actively maintaining it, so creating my own image isn't
necessary; however, good practice for homelab purposes.

- I have opted to utilize the built-in SQLite database; however, if this were
being heavily used, then an external database is likely preferrable.

- Authentik is setup as middleware between Traefik and FreshRSS. FreshRSS does
  have the ability to handle OIDC auth; however, attempts to configure it using
  both the documentation from [Authentik](https://docs.goauthentik.io/integrations/services/freshrss/) and [FreshRSS](https://freshrss.github.io/FreshRSS/en/admins/16_OpenID-Connect-Authentik.html) were not fruitful.

----------
