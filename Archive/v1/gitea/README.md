# Nick's Homelab - Gitea

[Return to Home](/README.md)

## Official Documentation

<https://docs.gitea.com/>

### Installation

<https://docs.gitea.com/installation/install-with-docker-rootless>

## My setup

Used the suggested `docker-compose.yml` settings; however, included
configuration for Traefik to handle the web frontend (port 3000).

Decided to also expose the ports, especially port 2222, which is used for ssh
connectivity.

## Notes

- Port 3000 does not need to be directly exposed and instead is ok to fully keep
  behind the Traefik reverse proxy.

----------
