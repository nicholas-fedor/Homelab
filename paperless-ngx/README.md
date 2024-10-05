# Nick's Homelab - Paperless-ngx

[Return to Home](/README.md)

## Description

Document management system that indexes and archives documents.

## URL

<https://paperless.nickfedor.dev>

## Project Website

<https://docs.paperless-ngx.com/>

## Project Documentation

- [Setup](https://docs.paperless-ngx.com/setup/)
- [Configuration](https://docs.paperless-ngx.com/configuration/)
- [Administration](https://docs.paperless-ngx.com/administration/)

## Source Repository

<https://github.com/paperless-ngx/paperless-ngx>

## Setup

- Used the developer-provided setup script to help generate the
  `docker-compose.yml` file.
  [Link](https://docs.paperless-ngx.com/setup/)
- Paperless is (re)started on system boot, if it was running before shutdown.
- Bind volumes are used for storing data.
- PostgreSQL is used as the database server.
- Apache Tika and Gotenberg servers are started with paperless and paperless
  is configured to use these services. These provide support for consuming
  Office documents (Word, Excel, Power Point and their LibreOffice counter-
  parts.
- `Import` and `Export` directories are mounted via `/etc/fstab` and mounted to the
  project directory for external access.
- Folders for importing and exporting files are created in the same directory
  as this file and mounted to the correct folders inside the container.
- Paperless listens on port 8000, which is not exposed, and is instead bound for
  Traefik to forward.
- Note the use of Docker secrets within the `docker-compose.yml` for setting the
  admin credentials and the secret key.

## Integrations

### Traefik

- The label `traefik.docker.network=proxy` is needed to ensure that the network
  `proxy` is used by Traefik.

### Authentik

- Added as Traefik forward proxy middleware.

## Notes

To install and update paperless with this file, do the following:

- Copy this file as 'docker-compose.yml' and the files 'docker-compose.env'
  and '.env' into a folder.
- Run 'docker compose pull'.
- Run 'docker compose run --rm webserver createsuperuser' to create a user.
- Run 'docker compose up -d'.

For more extensive installation and update instructions, refer to the
documentation.

----------
