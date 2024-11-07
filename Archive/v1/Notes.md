# Nick's Homelab - Notes

General notes regarding the configuration and maintenance of this homelab.

## Docker Compose File Structure

When reviewing various documentation sources, there's very little that I could
find pertaining to a formal structure for Docker Compose files.

Docker does provide a reference here: <https://docs.docker.com/reference/compose-file/>

In most Docker Compose files that are provided by application developers, the
top-level elements do follow a common layout.

Here is a basic Docker Compose example from Traefik's [documentation](https://doc.traefik.io/traefik/user-guides/docker-compose/basic-example/):

```yaml
version: "3.3"

services:

  traefik:
    image: "traefik:v3.1"
    container_name: "traefik"
    command:
      #- "--log.level=DEBUG"
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entryPoints.web.address=:80"
    ports:
      - "80:80"
      - "8080:8080"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock:ro"

  whoami:
    image: "traefik/whoami"
    container_name: "simple-service"
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.whoami.rule=Host(`whoami.localhost`)"
      - "traefik.http.routers.whoami.entrypoints=web"
```

Interestingly, the `version` top-level element is now considered obsolete
despite still being commonly used.  
It is something that I am currently opting to forego within my own compose files.

The `name` top-level element is not something that is normally seen as being
explicitly declared. Per Docker's [documentation](https://docs.docker.com/compose/how-tos/project-name/), it is typically derived from
the base name of the project directory.

## Images and Tags

The various applications that I am running have various sources, including
Docker, GitHub, and Gitea.

Images sourced from Docker may often be tagged with `Latest` and/or a version
number; however, this is often not the case for GitHub-based images, which may
only have the latter.

It may also be necessary to ensure stability by explicitly declaring certain
image versions, instead of simply referencing the `Latest` tag.

I am still deciding the best course of action on this for my homelab; however, I
do also have `Watchtower` running, which enables automatic checking and updating
of container images. This functionality can be customized in a variety of ways,
including specifying particular services for Watchtower to include or exclude.

I have yet to experiment with this further.

## Docker Environment Variables vs Secrets

When creating workloads in Docker using Docker Compose, it's possible to specify
sensitive and/or repeated configuration items using environment variables.

Docker's
[documentation](https://docs.docker.com/compose/how-tos/environment-variables/)
on environment variables sheds some light on the subject; however, the tl;dr is
that you can place a `.env` file within the same directory as the
`docker-compose.yml` file and pass variables when running the `docker compose up
-d` command.

This is useful for referencing variables within the Docker Compose file;
however, Docker Secrets are not something that can be referenced directly as
variables for the Docker Compose file to use. Rather, they are intended, as
expected, to be used within the containers themselves.

Docker Secrets
[documentation](https://docs.docker.com/reference/compose-file/secrets/)
references a [How-To
Guide](https://docs.docker.com/compose/how-tos/use-secrets/) for their usage.

The nuanaces between the usage of either are more apparent when working with
workloads outside of the small-scale, internal-only deployments of a homelab.

## Authentication

Upon starting this project, I did not initially configure an authentication
provider.
I attempted to utilize Authelia; however, upon attempting to setup TOTP
authentication, it was annoying me about adding SMTP settings.
As an alternative, I turned to Authentik, which has proven to work well for
enabling TOTP.

Setup was easy enough by following Christian Lempa's YouTube tutorial.

Unfortunately, during the course of trying to use it for OIDC authentication
with other container-based applications, I have uncovered a DNS configuration
issue that prevents containers from resolving URI's, such as
`authentik.nickfedor.dev`.

I suspect that switching over to using macvlan networking, where each container
can be assigned its own IP address, will help resolve this issue.

## Resource Usage

Upon starting to use Calibre to manage my collection of ebooks, I have
encountered the service utilizing 20GB+ of memory usage and heavy CPU usage
while importing and converting media.

This has led me to move the Docker VM to a separate workstation that I've
repurposed into a Proxmox server.

I am eager to find a more permanent solution, such as converting my TrueNAS
server to another Proxmox node with TrueNAS virtualized instead of running it
on bare metal.

## Internal and External Networks

When setting up applications that require additional containers to run backend
services, such as storage or caching, it is common to utilize a separate
network. As this is an internal network, when configuring via Docker Compose,
it's important to set the `External` option to `false` under the `Network`
top-level element.

## Directory Permissions

This homelab uses a NFS share on my TrueNAS NAS for data storage.
The NFS share is mounted to the Docker host and an `/home/Nick/Apps` directory is
symbolically linked to the `/mnt/TrueNAS/Apps` directory.

When it comes to NFS shares and datasets on TrueNAS, it's important to remember
that a NFS share for a parent dataset will behave differently from its child
datasets' own NFS shares. In addition, it's important to remember that while
Docker itself often runs as root, the applications running within containers may
also have their own users and groups that their processes run as.

tl;dr - Things can easily become messy when running Docker on a host that's
using an NFS share for data storage.

To help solve this problem, there are a few important items:

- The TrueNAS dataset needs to be owned by the same user that the NFS share's
  clients are mapped to.
- As previously mentioned, the `Mapall User` advanced NFS Share setting needs to
  match the dataset owner.
- That dataset owner/user must have `full control` permissions set via TrueNAS.

There's also the option for Docker containers to be provided PUID and GUID
settings via environment variables; however, I have had limited luck with this.

As an aside, Docker does has the option to mount volumes as NFS shares; however,
I've had limited experience in setting this up.
I briefly looked at doing this for my Traefik container; however, this was put
on hold when trying to determine an appropriate way to migrate from my current structure.

Overall, this is something I'm still trying to learn and master. I'll need to
document this further once I have a final way to securely accomplish this.

## SearXNG Timeouts

This is a nice application for pooling a variety of search engine data and
getting away from the enshittification of most major search engine UI's.
Unfortunately, I have found the application a bit of a nightmare to setup.
The SearXNG documentation is painful to work with. This is largely in part to
the formatting decision to use underscores "_" for every blank space. Annoying.
It also tends to skip around a bunch when it comes to setting things up.
The Docker repo is the easiest path to go; however, it requires mudding through
stripping away Caddy when using Traefik.
As to the timeout issue. After spending the time to set things up, it's highly
probable that DNS issues may occur. I suspect my host system's DNS settings
might be causing some of the problems; however, I was seeing timeouts on other
hosts as well.
In the end, I found that I needed to go through and explicitly set the
container's DNS to use Cloudflare (1.1.1.1) to remedy things.
In addition, the blocking of certain country's via Unifi's country blocker was
also a culprit in some of the errors.
I'm hopeful that this issue is resolved now.

---
