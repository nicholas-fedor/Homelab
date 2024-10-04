# Things To Do

[Return to Home](/README.md)

## Applications

- Continue transitioning applications from Truenas.
  Expectation is that there are some, such as Plex, that are resource-intensive
  and will be best left on Truenas box.

- Setup use of macvlan networking to enable each container to have its own IP
  address.

- Figure out DNS issue.
  I believe there is a host-specific DNS issue that's resulting in my issues
  with using Authentik as a OIDC auth provider.
  Containers are internally having trouble resolving [app].nickfedor.dev url's.

### AdGuard Home

- Figure out docker-compose configuration to allow for web interface via
  Traefik, but DNS routing direct to application. DoH (Port 443) is the most
  troublesome to figure out. Again, Macvlan networking will help resolve this.

### Future Applications

- Lama Cleaner

- Clipplex

- Overseer

- Plex

- Radarr

- Sonarr

- Lidarr

- Prowlarr

- MKV Cleaner

- MKV Toolnix

- Syncthing

- Filezilla

- Tautulli

- SearxNG

- Metube

- Tube Archivist

- Portainer

- Netbootxyz

- Proxmox Backup Server

- Speedtest Tracker

- Uptimekuma

- Prometheus

- Grafana

----------

[Return to Top](/TODO.md)

----------
