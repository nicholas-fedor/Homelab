# Nick's Homelab - Apt-Cacher-NG

[Return to Home](/README.md)

## Description
Tool for Apt package manager.
Intended to speed up package downloads and save bandwidth across multiple hosts.

## GitHub Repository

<https://github.com/nicholas-fedor/Homelab/tree/main/apt-cacher-ng>

## GitHub Container

<https://github.com/nicholas-fedor/Homelab/pkgs/container/apt-cacher-ng>

## DockerHub

<https://hub.docker.com/r/nickfedor/apt-cacher-ng>

## Official Documentation
<https://apt-cacher-ng.nickfedor.dev/acng-report.html>

## Usage

```console
echo 'Acquire::http::Proxy "http://apt-cacher-ng.nickfedor.dev:3142";' | sudo tee /etc/apt/apt.conf.d/00aptproxy
```

## Development

Build for Docker Hub:

```console
docker build -t nickfedor/apt-cacher-ng .
```

Upload to Docker Hub:

```console
docker push nickfedor/apt-cacher-ng
```

Build for GitHub Container Registry:

```console
docker build . -t ghcr.io/nicholas-fedor/apt-cacher-ng:latest
```

Upload to GitHub Container Registry:

```console
docker push ghcr.io/nicholas-fedor/apt-cacher-ng:latest
```

Build for Gitea Container Registry:

```console
docker build . -t gitea.nickfedor.dev/nick/apt-cacher-ng:latest
```

Upload to Gitea Container Registry:

```console
docker push gitea.nickfedor.dev/nick/apt-cacher-ng:latest
```

## Notes

- Web interface setup behind Traefik; however, port `3142` also exposed directly
  for direct access.

- For the host VM to use it, I had to add `apt-cacher-ng.nickfedor.dev` to the
  `/etc/hosts` file.

- The usage webpage has connection details that may reflect the container's IP
  address.  
  The webpage can be manually edited by navigating to the
  `/usr/lib/apt-cacher-ng/userinfo.html` file and changing the
  `${serverhostport}` variable (for example:
  `192.168.50.224:3142`).  
  As this is an environment variable, it may be possible to set this via the
  Docker Compose file; however, I have yet to test this.

- I have found that the Docker VM hosting the application container may have
  issues connecting. If this is the case, then it's possibly to use the internal
  IP:Port `127.0.0.1:3142` to resolve this.

----------
