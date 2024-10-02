# Nick's Homelab - Calibre

[Return to Home](/README.md)

## Description

Ebook manager

## URLs

Calibre: <https://calibre.nickfedor.dev/>  
Calibre-Web: <https://calibre-web.nickfedor.dev/>

## Project Website

<https://calibre-ebook.com/>

## Project Documentation

<https://manual.calibre-ebook.com/>

## Source Respositories

Calibre: <https://github.com/kovidgoyal/calibre>  
Calibre-Web: <https://github.com/janeczku/calibre-web>

## Setup

This application has two components:

1) Calibre

   <https://hub.docker.com/r/linuxserver/calibre>

2) Calibre-Web

   <https://hub.docker.com/r/linuxserver/calibre-web>

## Integrations

### Traefik

Using the HTTP endpoints for Traefik to add SSL certs and proxy.
LinuxServer's Docker image comes with a SSL cert, if needed.

### Authentik

Using the forward proxy provider.
Links via Traefik middleware label.

## Notes

- Opted to use LinuxServer's Docker images to keep things "simple".
  I might eventually switch over to building my own.

- The `./data/calibre/Books` and `./data/calibre/Downloads` directories are NFS
  shares mounted to `/mnt/` and then symlinked accordingly.

----------
