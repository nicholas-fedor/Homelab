# Nick's Homelab - Changelog

[Return to Home](/README.md)

----------

2024-09-16

- Initial setup of Traefik, Watchtower, Homarr, IT-Tools, Cyberchef, and Apt Cacher ng.

2024-09-17

- Created repository and added to it GitHub.
- Enabled VSCode as primary access and management tool.
- Added Truenas NFS share to host.
- Moved application storage to NFS share.
- Added `apt-cacher-ng` to `etc/hosts` file.
- Added Apt-Cacher-NG container image to both Docker Hub and GitHub.

2024-09-18

- Changed CF email variable to set via `.env` instead of via static
  configuration within `traefik.yml` file.
- Created application-specific `README.md` files.
- Moved changelog to its own file.

2024-09-19

- Added Gitea
- Updated application-specific `README.md` files.
- Created application-specific `.gitignore` files.
- Created `SETUP.md` file.

2024-09-20

- Added Drawio, including application documentation.

2024-09-22

- Added FreshRSS

2024-09-23

- Remove port 3000 exposed by Gitea.

2024-09-27

- Added Authentik.

2024-09-28

- Finished adding forward proxy authentication to applications.
- Added navigation links to project documentation.

2024-09-29

- Further documentation updates.
- Added project-level `Notes.md`.
- Recreated Git repository.

2024-09-30

- Added documentation regarding setting up Macvlan networking for Docker containers.

----------

[Return to Top](/CHANGELOG.md)

----------
