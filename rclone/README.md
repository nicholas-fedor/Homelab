# Nick's Homelab - Rclone

[Return to Home](/README.md)

## Description
File management program that I'm using for more efficiently grabbing OS ISOs.

## Web URL

<https://rclone.nickfedor.dev>

## Publisher's Website
<https://rclone.org/>

## Published Docker Image
<https://hub.docker.com/r/rclone/rclone>

## Commands Reference
<https://rclone.org/commands/rclone/>

## Syncing the following ISOs
Ubuntu Daily Live Server

- <https://cdimage.ubuntu.com/ubuntu-server/daily-live/current/oracular-live-server-amd64.iso>  
- <https://cdimage.ubuntu.com/ubuntu-server/noble/daily-live/current/noble-live-server-amd64.iso>

Debian Full Release Version

- <https://cdimage.debian.org/cdimage/release/current/amd64/iso-dvd/debian-12.7.0-amd64-DVD-1.iso>

Debian Net Installer Release Version

- <https://cdimage.debian.org/cdimage/release/current/amd64/iso-cd/debian-12.7.0-amd64-netinst.iso>

Debian Daily Version

- <https://cdimage.debian.org/cdimage/daily-builds/daily/current/amd64/iso-cd/debian-testing-amd64-netinst.iso>

Debian Daily Cloud Image QCOW

- <https://cdimage.debian.org/cdimage/cloud/bookworm/daily/latest/debian-12-generic-amd64-daily.qcow2>

Debian Daily Cloud Image RAW

- <https://cdimage.debian.org/cdimage/cloud/bookworm/daily/latest/debian-12-generic-amd64-daily.raw>  

## Host Setup

- Added `/etc/fstab` NFS configuration to the TrueNAS NFS share
- Sym-linked the `/mnt/TrueNAS/ISOs` share to the `./rclone/isos` directory

## Docker Setup

- Persisting the configuration
- The `/data` container directory used for access to the NFS share.
- There is an option within Rclone to setup a SMB share instead; however, I have
  yet to play with that.
- The individual directories for each of the ISOs referenced above are
  configured separately and available via the GUI's `Explorer`
- Authentik is added in front of the application to provide a little more
  protection

## Notes

- I was hoping for something that I can use for automating the downloads of
  ISOs. Rclone hasn't accomplished the task just yet; however, it's an
  improvement over manually going to the download sites and/or using the Proxmox
  GUI for the downloads.
  
----------
